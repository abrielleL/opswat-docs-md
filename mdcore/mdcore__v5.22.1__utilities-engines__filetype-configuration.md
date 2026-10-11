<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration -->

# Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This guide provides detailed configuration options under **Workflow Management > Workflows > [Workflow name] > File Type**, enabling users to customize detection settings effectively.

## [Detect file type mismatch](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#detect-file-type-mismatch)

#### [Accepted extensions](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#accepted-extensions)

*Accepted extensions* is a feature that allows customers to add extensions for specific file type to avoid mismatching.

| Section | Mandatory | Note |
| --- | --- | --- |
| File type ID | Yes |  |
| Extensions | No | Default value: empty. Can be * to accept any extension. |

This feature also supports regular expressions in the value field. To indicate that a value is a regular expression, use the designated prefix. For example:

**regex**:^[^.]+$|.(?![A-Za-z]{3}$)[^.]+$|.(PNG|png)$

## [Include file details](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#include-file-details)

See details of additional info returned by the engine at [File info details](https://www.opswat.com/docs/mdcore/utilities-engines/file-info-details).

## [Detect encrypted archive](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#detect-encrypted-archive)

Perform detection on the encryption attribute of archive files, such as ZIP and RAR.

If the option is turned on, encrypted archive files will have the returned output with value True in field encrypted.

Note: For *Encrypted ZIP* file, this feature only works when Core version is greater than 5.1.0.

Output for Encrypted ZIPCopy"file_info": {
"description": "Encrypted ZIP Archive",
"encrypted": true,
"extensions": "zip,zipx",
"groupID": "A",
"groupIDs": [
"A"
],
"group_description": "Archive Files",
"likely_type_ids": [
{
"score": 1,
"typeID": "ZIP"
}
],
"type": "application/zip",
"typeID": "ZIP",
"type_ids": [
"ZIP"
]
}
## [Overwrite a file type by another file type](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#overwrite-a-file-type-by-another-file-type)

This option is to alter the detected result (type ID) to a similar one.

| **Filetype** | **Sub filetype** |
| --- | --- |
| Encrypted-GPG | GPG |
| Restricted-PDF | Encrypted-PDF |

## [Classify with Machine Learning](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#classify-with-machine-learning)

Classify files using Machine Learning. See details in [here](https://www.opswat.com/docs/mdcore/utilities-engines/text-detection-with-ai-enhancement).

## [Distinguish zero-byte files](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#distinguish-zero-byte-files)

If enabled, zero-byte files will be detected as ZERO instead of DATA.

## [Detect Base64 encoded text](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#detect-base64-encoded-text)

Returns Base64 if the file is TXT and Base64 encoded.

## [Detect ASCII text](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#detect-ascii-text)

Enable ASCII detector to cover wide variety of ASCII text, e.g., non-printable or control characters. We can configure the threshold for allowable non-printable characters via spin-box *Non-printable threshold*.

Non-printable characters

| **ASCII code** | **Character** |
| --- | --- |
| 1 -> 8 | Control characters |
| 11 | [Vertical tab] |
| 12 | [Form feed] |
| 14 -> 31 | Control characters |
| 127 | [DEL] |

## [Detect Shift-JIS text](/docs/mdcore/v5.22.1/utilities-engines/filetype-configuration#detect-shift-jis-text)

Enable Shift-JIS text detector to cover wide variety of Shift-JIS text.
