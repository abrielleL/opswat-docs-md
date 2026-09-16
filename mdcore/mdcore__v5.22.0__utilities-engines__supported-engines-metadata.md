<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/utilities-engines/supported-engines-metadata -->

# Supported engines-metadata header

## [Include more file info details](/docs/mdcore/v5.22.0/utilities-engines/supported-engines-metadata#include-more-file-info-details)

Beside the basic file type info such as true file type, file type group, etc... the File type engine is able to return more details about the file. To retrieve more file info please follow the steps

1. Use [MetaDefender Core API](https://docs.opswat.com/mdcore/metadefender-core/ref) to process a file
2. Send the **engines-metadata** header with this value

JsonCopy{
"file_type": {
"include_file_details.file_metadata": false,
"include_file_details.other_details": true
}
}

A **file_info_details** attribute will be added to the output, e.g.:

JavascriptCopy{
...
"file_info_details": {
"properties": {
"portfolio": true
}
},
"file_size": 3600732,
"file_type": "application/pdf",
"file_type_description": "Adobe Portable Document Format",
"file_type_id": "PDF",
...
}

Note: Enabling this feature may impact the performance.

## [Overwrite file type detection](/docs/mdcore/v5.22.0/utilities-engines/supported-engines-metadata#overwrite-file-type-detection)

The File Type Verification Engine analyzes the file’s structure and content to verify the true file type for given files and minimize the risk of file type spoofing. However, in some specific cases, the File Type Verification Engine returns unexpected results from the client's perspective. For example, if a file contains "Hello, **John**", it can be either an HTML file, or a text file, or even a CSV file with a comma separator.

Therefore, to handle these similar cases, MetaDefender Core now supports users to overwrite the true file type with 2 simple steps:

1. Use [MetaDefender Core API](https://docs.opswat.com/mdcore/metadefender-core/ref) to process a file
2. Send the **engines-metadata** header with this value

JsonCopy{
"file_type": {
"overwritten": {
"file_type_id": "HTML"
}
}
}
## [Other settings](/docs/mdcore/v5.22.0/utilities-engines/supported-engines-metadata#other-settings)

- Detect encrypted archive: Perform detection on encryption attribute of archive files.
- Classify with Machine Learning: Classify text-based files with Machine learning engine. Module setting 'Enable Machine Learning module' needs to be turned on.
- Detect Base64 encoded text: Returns Base64 if the file is TXT and Base64 encoded.
- Detect file type mismatch: Detects when the extension of the file does not match with the allowed extensions.

  - Accepted extensions: Accepted extensions in addition to default extensions.

    - File type ID: File type to apply
    - Extensions: List of extensions separated by commas
- Detect ASCII text: Enable ASCII detector to cover wide variety of ASCII text, e.g., non-printable or control characters.
- Non-printable threshold: Percent of non-printable characters over total characters allowed in text.

JsonCopy{
"file_type": {
"detect_encrypted_archive": true,
"classify_with_ml": false,
"detect_base64": false,
"filetype_mismatch": true,
"filetype_mismatch.accepted_extensions": [
{
"filetype_to_apply": "doc",
"extensions_to_apply": "txt"
}
],
"enable_ascii": false,
"enable_ascii.non_printable_threshold": 5
}
}
