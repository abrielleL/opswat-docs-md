<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/file-structure-validation/json-schema-validation -->

# JSON schema validation

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [**Overview**](/docs/mdcore/v5.24.1/file-structure-validation/json-schema-validation#overview)

FSV can check JSON files against a JSON Schema that you provide. Before the file is sanitized, the engine validates it against the schema and reports whether it conforms. You choose whether a non-conforming file is only reported or is blocked.

**Applies to:** JSON, HAR, LYRX.

**Schema dialects:** Draft 4, 6, 7, 2019-09 and 2020-12, picked from the schema's `$schema` keyword. A schema without `$schema` is accepted; an unrecognised `$schema` value fails with *Schema error*. `format` keywords (`date-time`, `email`, `uri`, ...) are enforced, not just annotated.

## [**Settings**](/docs/mdcore/v5.24.1/file-structure-validation/json-schema-validation#settings)

In the Core web console: **Workflows** → open the workflow → **File Structure Validation** → **Schemas Validation** → **Schema-based JSON Validation**.

## [**Quick start**](/docs/mdcore/v5.24.1/file-structure-validation/json-schema-validation#quick-start)

1. Copy your schema files to a folder on the Core server, e.g. `C:\schemas\orders\`:

`C:\schemas\orders\
 order.schema.json <- root schema
 address.schema.json <- referenced by order.schema.json`

2. In the workflow rule, enable **Validate against Schema** under Schema-Based JSON Validation.
3. Set **JSON Schema Location** = `C:\schemas\orders` and **Schema File Name** = `order.schema.json`.
4. Pick the **Validation Effect**: start with `Success` to see results without blocking, switch to `Failure` once the schema is trusted.
5. Scan a JSON file and check the result (see below).

Example schema `order.schema.json`:

{
"$schema": "http://json-schema.org/draft-07/schema#",
"type": "object",
"required": ["id", "amount"],
"properties": {
"id": { "type": "string" },
"amount": { "type": "number", "exclusiveMinimum": 0 },
"shipTo": { "$ref": "address.schema.json" }
}
}

**Referenced schemas (**`$ref`**)**

- A `$ref` to another file is resolved **by file name, in the same directory as the root schema**. `address.schema.json`, `./address.schema.json` and `https://example.com/schemas/address.schema.json` all load `address.schema.json` from that directory.
- Nothing is downloaded. To use a schema that references a remote URL, save the referenced file beside the root schema under the same file name.
- A referenced file that is missing or not valid JSON fails the file with *Schema error*.

## [**Results**](/docs/mdcore/v5.24.1/file-structure-validation/json-schema-validation#results)

Results appear in the Core scan result under `filestructurevalidation_info.process_details`, as the processed object `structural JSON` in `details`. A blocked file has the message in `details` and a `failure_category` instead.

**Valid file**

{
"object_name": "structural JSON",
"result_of_action": "valid",
"object_metadata": [ "Validated against \"order.schema.json\"" ]
}

**Invalid file, effect =** `success` — the file is still allowed; the violation is reported:

{
"object_name": "structural JSON",
"result_of_action": "invalid",
"object_metadata": [
"Schema violation at \"/amount\" (keyword \"exclusiveMinimum\", schema \"order.schema.json\"): Exclusive minimum value is 0 but found -3",
"Validated against \"order.schema.json\""
]
}

**Invalid file, effect =** `failure` — the file is blocked, category *invalid file structure*, with the same message as the failure details.

### [**Message reference**](/docs/mdcore/v5.24.1/file-structure-validation/json-schema-validation#message-reference)

| Situation | Category | Details |
| --- | --- | --- |
| Instance violates the schema | invalid file structure (effect `failure`) / reported as `invalid` (effect `success`) | `Schema violation at "<JSON pointer>" (keyword "<kw>", schema "<file>"): <reason>` — only the first violation is reported |
| File is detected as JSON but cannot be parsed (e.g. NDJSON) | invalid file structure (both effects) | Effect `failure`: `Malformed JSON at line L, column C: <reason>`. Effect `success`: `Invalid JSON file structure` |
| Location empty / missing | failed to sanitize | `Schema unavailable: the schema location is empty` / `... does not exist` |
| Schema file name empty | failed to sanitize | `Schema unavailable: the schema file name is empty` |
| Schema file not found | failed to sanitize | `Schema unavailable: the JSON schema file "<name>" does not exist at the schema location` |
| Schema is broken or a `$ref` cannot be resolved | failed to sanitize | `Schema error in "<file>"[ at line L, column C]: <reason>` |

Schema configuration problems (*Schema unavailable*, *Schema error*) always fail the file, whatever the validation effect, so a misconfiguration is never silently passed.

## [Specify the schema through the REST API](/docs/mdcore/v5.24.1/file-structure-validation/json-schema-validation#specify-the-schema-through-the-rest-api)

When you submit a file through the REST API (`POST /file`), you can choose which JSON schema File Structure Validation validates the file against. Pass the schema file name in the `engines-metadata` request header:

{
"fsv": {
"json_schema_validation.validate_against_schema.schema_name": "<schema file name>"
}
}

| Parameter | Description |
| --- | --- |
| `json_schema_validation.validate_against_schema.schema_name` | File name of the XSD to validate against, for example, for example `purchase-order.schema.json`. |

## [**Known limitations**](/docs/mdcore/v5.24.1/file-structure-validation/json-schema-validation#known-limitations)

- **NDJSON** (newline-delimited JSON) is not validated per line. With effect `failure` the file is blocked as `Malformed JSON`; with effect `success` it is allowed and reported as `invalid` with the `Malformed JSON` message.
- **UTF-16** JSON files are not validated: the file is allowed and no `structural JSON` entry is reported.
