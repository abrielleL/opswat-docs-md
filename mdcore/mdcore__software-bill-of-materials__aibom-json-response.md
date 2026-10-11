<!-- source: https://www.opswat.com/docs/mdcore/software-bill-of-materials/aibom-json-response -->

# AIBOM JSON response

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This page describes the `aibom_info` section of the scan result, for integrations that parse it. For what AIBOM detects and how to read it, see [AI Bill of Materials (AIBOM) (Beta)](aibom).

## [JSON structure](/docs/mdcore/software-bill-of-materials/aibom-json-response#json-structure)

JsonCopy"aibom_info": {
"final_verdict": {
"verdict": "<string>",
//"No AI Components Found" | "License Risk Found" | "AI Components Found"
"verdict_explanation": ["<string>"], //one entry, equal to "verdict"
"blocked": <boolean>, //true only when licensing_component_counts.blocked > 0
"severity": "INFO", //always "INFO"
"total_component_count": <int>, //number of entries in "components" (repositories, not files)
"licensing_component_counts": { //absent when there are no components; zeros are always emitted
"allowed": <int>,
"blocked": <int>,
"unknown": <int> //components with no declared license
}
},
"component_group": { //the scanned file; {} when nothing was found
"group_id": "sha256:<hex>", //SHA-256 of the scanned file, with the "sha256:" prefix
"target": "<string>", //the file name you submitted
"metadata": [ //facts read from the file's bytes
{ "name": "<string>", "value": <string | int> }
],
"refs": ["<string>"] //uid of every component that contains the scanned file
},
"components": [ //one entry per repository; [] when nothing was found
{
"uid": "<string>", //package URL, e.g. pkg:huggingface/<owner>/<repo>@<commit>
"type": "machine-learning-model",
"name": "<string>", //<owner>/<repo>
"version": "<string>", //repository commit
"url": "<string>", //repository page
"authors": "<string>", //repository owner
"description": "<string>",
"published_at": "<string>", //RFC 3339 timestamp
"last_modified_at": "<string>", //RFC 3339 timestamp
"scans_done": <boolean>, //whether the registry has scanned the repository
"library": "<string>", //framework declared by the registry
"hashes": [
{ "file_name": "<string>", "sha256": "<hex>" } //no "sha256:" prefix
],
"licenses": { //absent when the repository declares no license
"allowed": [ <license> ], //or "blocked": [ <license> ]
},
"model_card": { //facts declared by the publishing registry
"base_model": "<string>",
"base_model_relation": "<string>", //e.g. "quantized"
"hyperparameters": [ { "name": "<string>", "value": <int> } ]
}
}
]
}

A `<license>` entry has this shape:

JsonCopy{
"id": "<string>", //SPDX identifier, e.g. "Apache-2.0"
"name": "<string>", //license name as the repository declares it
"category": "<string>", //e.g. "permissive"
"url": "<string>",
"usage_restriction": {
"permissions": ["<string>"],
"conditions": ["<string>"],
"limitations": ["<string>"]
}
}
## [Block states](/docs/mdcore/software-bill-of-materials/aibom-json-response#block-states)

The shape of `aibom_info` tells you whether AIBOM ran:

| Shape | Meaning |
| --- | --- |
| `aibom_info` :`no exist` | AIBOM did not run: it is disabled in the workflow. |
| `err_code` + `err_details` | AIBOM ran and could not finish. `err_details` is `"AIBOM cache unavailable."` when the model database is unavailable, and `"The module did not complete this scan."` otherwise. |
| `final_verdict`, `component_group`, `components` | AIBOM ran. When it found nothing, the verdict is `No AI Components Found`, `component_group` is `{}` ,`components` is `[] and licensing_component_counts`is absent. |

## [Field notes](/docs/mdcore/software-bill-of-materials/aibom-json-response#field-notes)

- **Absent keys mean "not known".** Inside a component, values are never `null`, `""` or `[]` in place of an unknown, so `"version" in component` is a reliable test. Exceptions: the `format` entry of `metadata` is always present when `component_group` is not empty, the counts in `licensing_component_counts` always include zeros, and `model_card.metrics` is carried exactly as the publisher wrote it, `null` values included.
- **Verdict.** `verdict` is evaluated in this order: `No AI Components Found` (`total_component_count` is 0), `License Risk Found` (`licensing_component_counts.blocked` is greater than 0), `AI Components Found`. Components with an unknown license do not change the verdict.
- **Finding the scanned file in a repository.** In a component's `hashes[]`, the entry whose `sha256` equals `component_group.group_id` **without the `sha256:` prefix** is the file you scanned, under the name that repository gives it. That name often differs from the one you submitted.
- **Header facts versus registry facts.** `component_group.metadata` comes from the file's bytes; everything on a component comes from the publishing registry. If they disagree, for example `parameters` in `metadata` against `model_card.hyperparameters`, that is worth reviewing, not an error in the report. A registry often reports figures for the whole repository rather than for the one file you scanned.
- **Metadata names are the scanner's own.** Entries in `metadata` use the scanner's names, not the keys inside the file. A GGUF header's `general.license` is reported as `license`. Its value is free text the file declares; license buckets come from the repository's declaration, not from it.
- **Component order.** Components are sorted by `published_at`, oldest first.

## [Example](/docs/mdcore/software-bill-of-materials/aibom-json-response#example)

#### [A model file found in a public repository](/docs/mdcore/software-bill-of-materials/aibom-json-response#a-model-file-found-in-a-public-repository)

A safetensors file submitted as `model.safetensors`, matched to one repository that keeps it as `1_Dense/model.safetensors`:

JsonCopy"aibom_info": {
"final_verdict": {
"verdict": "AI Components Found",
"verdict_explanation": ["AI Components Found"],
"blocked": false,
"severity": "INFO",
"total_component_count": 1,
"licensing_component_counts": { "allowed": 1, "blocked": 0, "unknown": 0 }
},
"component_group": {
"group_id": "sha256:3b5d855b26767da1c16a086c90aef497114c7c0c4451c6fe9df7a0afc2401c86",
"target": "model.safetensors",
"metadata": [
{ "name": "format", "value": "safetensors" },
{ "name": "parameters", "value": 16384 },
{ "name": "tensor_count", "value": 1 },
{ "name": "size_bytes", "value": 65624 }
],
"refs": ["pkg:huggingface/NeuML/pylate-bert-tiny@9cb92954e00ee9b127df35354e4714ed5ff70bee"]
},
"components": [
{
"uid": "pkg:huggingface/NeuML/pylate-bert-tiny@9cb92954e00ee9b127df35354e4714ed5ff70bee",
"type": "machine-learning-model",
"name": "NeuML/pylate-bert-tiny",
"version": "9cb92954e00ee9b127df35354e4714ed5ff70bee",
"url": "https://huggingface.co/NeuML/pylate-bert-tiny",
"authors": "NeuML",
"published_at": "<RFC 3339 timestamp>",
"last_modified_at": "<RFC 3339 timestamp>",
"scans_done": <boolean>,
"hashes": [
{ "file_name": "1_Dense/model.safetensors", "sha256": "3b5d855b26767da1c16a086c90aef497114c7c0c4451c6fe9df7a0afc2401c86" }
],
"licenses": {
"allowed": [
{
"id": "<SPDX id>",
"name": "<declared name>",
"category": "<category>",
"url": "<license URL>",
"usage_restriction": { "permissions": ["<...>"], "conditions": ["<...>"], "limitations": ["<...>"] }
}
]
},
"model_card": {
"hyperparameters": [ { "name": "parameters", "value": <int> } ]
}
}
]
}
#### [No AI components found](/docs/mdcore/software-bill-of-materials/aibom-json-response#no-ai-components-found)

JsonCopy"aibom_info": {
"final_verdict": {
"verdict": "No AI Components Found",
"verdict_explanation": ["No AI Components Found"],
"blocked": false,
"severity": "INFO",
"total_component_count": 0
},
"component_group": {},
"components": []
}
