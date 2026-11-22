<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/file-structure-validation/xml-schema-validation -->

# XML schema validation

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

File Structure Validation lets you enforce XML Schema (XSD) validation on XML files. If a file does not conform to the specified schema, it fails validation, and the configured Validation Effect on Final Result determines the outcome of the scan.

A valid XML file that conforms to the schema

An invalid XML file that fails schema validation

## [Specify the schema through the REST API](/docs/mdcore/v5.24.1/file-structure-validation/xml-schema-validation#specify-the-schema-through-the-rest-api)

When you submit a file through the REST API (`POST /file`), you can choose which XML schema File Structure Validation validates the file against. Pass the schema file name in the `engines-metadata` request header:

{
"fsv": {
"schema_validation.validate_against_schema.schema_name": "<schema file name>"
}
}

| Parameter | Description |
| --- | --- |
| `schema_validation.validate_against_schema.schema_name` | File name of the XSD to validate against, for example `cargo-exchange.xsd`. |
