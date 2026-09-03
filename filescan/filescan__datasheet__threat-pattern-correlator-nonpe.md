<!-- source: https://www.opswat.com/docs/filescan/datasheet/threat-pattern-correlator-nonpe -->

# Threat Pattern Correlator - Support for Non-Executables

Enhancements to Threat Pattern Correlator now include support for all file types, improved speed, accuracy, and additional features for PE, resulting in an overall enhanced analysis experience.

## All file type

Info

Threat Pattern Correlator is applicable in numerous fields(close to 120 for all file types), but due to security reasons, we prefer not to disclose all of them. However, here are a few examples:

These features are carefully selected based on their ability to provide accurate and relevant results, and they are continuously updated to stay current with the latest malware trends and techniques.

| Feature group | **Number of features** |
| --- | --- |
| Apk | 22 |
| Biffopcodes | 1 |
| Emulation | 14 |
| Extracted | 10 |
| Extended data | 24 |
| Metadata | 15 |
| Segments | 6 |
| Sections | 6 |
| Strings | 5 |
| Threat indicators | 2 |
| Yara | 3 |
| Triggered consumer Ids | 1 |

### Some of the features are:

ApkBiffopcodesEmulationExtractedExtendedDataMetaDataSegmentsSectionsStringsThreat IndicatorsYara

| Field name | Type | Description |
| --- | --- | --- |
| Metadata version code | String | Version code of the APK |
| *....(Other features )* | *.....* | *.....* |
| APK signers path | String | Path to APK signers |
| API events class name | String | Class name of API events |
| API events function name | String | Function name of API events |

| Field name | Type | Description |
| --- | --- | --- |
| Biffopcodes | String | Shows basic arithmetic, logic, or data movement operations executed by a processor. |
| *....(Other features )* | *.....* | *.....* |

| Field name | Type | Description |
| --- | --- | --- |
| Emulation exit code | Number | Emulation exit code |
| Additionalinformation compilerconstants | String | Additional information about the compiler constants |
| *....(Other features )* | *.....* | *.....* |
| Metadata reason | String | Reason for emulation metadata |
| Overview modules | String | Overview of modules in emulation metadata |

| Field name | Type | Description |
| --- | --- | --- |
| Extracted Urls | String | Extracted URLs from the file |
| *....(Other features )* | *.....* | *.....* |
| Extracted SHA-512 Hashes | String | Extracted SHA-512 from the file |
| Extracted E-mails | String | Extracted Emails from the file |

| Field name | Type | Description |
| --- | --- | --- |
| Header file size | Number | Size of the header file |
| *....(Other features )* | *.....* | *.....* |
| Symbols static | String | Static symbols |
| Streams ole stream | String | OLE stream |
| Streams subfiles no xml | String | Subfiles with no XML |

| Field name | Type | Description |
| --- | --- | --- |
| Content type | String | Type of content |
| Appversion | String | Application version |
| *....(Other features )* | *.....* | *.....* |
| To | String | Recipient information |
| Subject | String | Subject of the metadata |
| Cc | String | CC metadata |

| Field name | Type | Description |
| --- | --- | --- |
| Segments entropy | String | Entropy of segments |
| *....(Other features )* | *.....* | *.....* |
| Segments flags | String | Flags of segments |

| Field name | Type | Description |
| --- | --- | --- |
| Sections entropy | String | Entropy of sections |
| *....(Other features )* | *.....* | *.....* |
| Sections virtualsize | String | Virtual size of sections |

| Field name | Type | Description |
| --- | --- | --- |
| Strings in binary content parse | String | Strings parsed from binary content |
| *....(Other features )* | *.....* | *.....* |

| Field name | Type | Example | Description |
| --- | --- | --- | --- |
| Threat Indicators | String | Number | An identifier to show what kind of rules (Threat indicator) Filescan itself matched on the target file. It can contain more info than what is present in the actual report |

| Field name | Type | Description |
| --- | --- | --- |
| Yara Matched strings | String | Yara matched strings |
| *....(Other features )* | *.....* | *.....* |
| Yara Rule name | String | Yara rule name |

## Threat Pattern Correlator Filters

In addition to advanced technology, Threat Pattern Correlator provides multi filtering search parameters. This feature offers greater flexibility and ensures that users receive the most accurate and relevant results for their specific needs.

Query filtersNon Query filters

| Field name | Type | Possible values | Example | Description | Required |
| --- | --- | --- | --- | --- | --- |
| SHA-256 | String |  | Number |  | Yes |
| Submission data | Date | 2023-01-17T12:17:20.000Z | Number |  | Optional |
| Final Verdict | String | CONFIRMED THREAT, HIGH RISK, LOW RISK, NO THREAT DETECTED, UNDETERMINED, TRUSTED | CONFIRMED THREAT | Verdict of a file | Optional |
| Tags | String | peexe,xml |  | Tags of a file | Optional |
| Threshold | Number | 1 to 100 any integer | Number | Similarity threshold 0% to 100%  Higher score means higher similarity | Optional |
| Limit | Number | 1 to 100 any integer | Number | Number of returns | Optional |

| Field name | Type | Description |
| --- | --- | --- |
| File size | Number | Size of the input file |
| Entropy | Number | Entropy of the whole file(*) |
| Architecture | Number | A string describing what target of architecture (eg. 32 or 64bit) the binary was compiled for(*) |
| IsDotnet | Number | Whether the executable file is using the .NET framework(*) |

- *Query filters only supported if the file type is PE

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
