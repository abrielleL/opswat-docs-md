<!-- source: https://www.opswat.com/docs/mdcore/file-structure-validation/understanding-the-validation-report -->

# Understanding the Validation Report

FSV results appear in the scan result JSON under `filestructurevalidation_info`, with extracted objects listed under the sibling block `fsv_output_files`.

"filestructurevalidation_info": {
"process_details": {
"description": "Analyzed and validated successfully.",
"details": [
{
"object_name": "hyperlink",
"action": "validated",
"count": 3,
"result_of_action": "valid",
"object_details": ["https://example.com", "..."]
}
],
"verdict_explanations": []
},
"final_verdict": { "verdict": "allowed" },
"version": "2.0.0"
},
"fsv_output_files": {
"fsv_output_files_count": 2,
"files_in_fsv_output": [
{
"object_type": "macro",
"display_name": "vbaProject.bin",
"file_size": 15360,
"file_type_id": "..."
}
]
}
## [**Verdict**](/docs/mdcore/file-structure-validation/understanding-the-validation-report#verdict)

`final_verdict.verdict` is `allowed` or `blocked`. When blocked, `verdict_explanations` lists the reasons in plain language, for example:

- `invalid file structure`
- `contain JavaScript`, `contain DDE`, `contain document open action`, … (one per blocked object class)
- `This is a polyglot file. Hit: PDF at offset 0; ZIP at offset 204849`

## [**Object details**](/docs/mdcore/file-structure-validation/understanding-the-validation-report#object-details)

Each entry in `details[]` describes one object class found in the file:

| Field | Meaning |
| --- | --- |
| `object_name` | The object class, for example `macro`, `hyperlink`, `embedded object`, `metadata` |
| `action` | What FSV did: `validated`, `extracted`, `detected`, or `skipped` |
| `count` | Number of instances |
| `result_of_action` | `valid` or `invalid` |
| `object_details` | Instance data, for example the hyperlink URLs found |
| `object_metadata` | Spec-level explanation, for example `Graph valid against specification` |
| `object_sha256` | Per-instance content hashes |
| `skipped_reason` | Why an object was not processed: `signed_file`, `limit_exceeded`, `marked_as_skipped`, … |

With the **deep dive** setting enabled (default), entries also carry structural data — object relationships and offsets inside the file.

Custom blocking rules match against these fields with a JSON path — see [Blocking files based on rules](https://file+.vscode-resource.vscode-cdn.net/c%3A/Users/vlam/Downloads/fsv-docs/blocking-files-based-on-rules).

## [**Extracted output files**](/docs/mdcore/file-structure-validation/understanding-the-validation-report#extracted-output-files)

`fsv_output_files.files_in_fsv_output[]` lists every object returned to the workflow, with `object_type`, `display_name`, `file_size`, and its detected file type. Which classes are returned is controlled by the selected object types — see [Extracting objects and recursive processing](https://file+.vscode-resource.vscode-cdn.net/c%3A/Users/vlam/Downloads/fsv-docs/extracting-objects-and-recursive-processing).

## [**Failures**](/docs/mdcore/file-structure-validation/understanding-the-validation-report#failures)

A file FSV could not process carries `process_details.failure_category` — most commonly `invalid file structure`, meaning the file violates its format specification badly enough that parsing cannot continue.
