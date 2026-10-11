<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/threat-pattern-correlator -->

# Threat Pattern Correlator - Introduction

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Our ML-Based Threat Pattern Correlator leverages advanced feature extraction techniques to identify and correlate unknown threats with known malware families. By analyzing behavioral patterns, code structures, and static attributes, our machine learning models detect even evasive or zero-day threats that traditional signature-based methods may miss.

This capability enables security teams to quickly **pivot between related threats**, uncover hidden malware clusters, and enhance threat hunting efficiency—making it a powerful tool for identifying and responding to emerging cyber threats.

## [Portable Executable type](/docs/filescan/3.2.0/datasheet/threat-pattern-correlator#portable-executable-type)

These features are carefully selected based on their ability to provide accurate and relevant results, and they are continuously updated to stay current with the latest malware trends and techniques.

Binary metadataCertificatesCharacteristicDisassembly sectionsDotnet infoHeader infoExtractedThreat Indicators

| Field name | Type | Description |
| --- | --- | --- |
| Language | String | What speaking language does the binary target |
| Entry point section name | String | Name of the section where the entry point of the PE resides. It’s a calculated value, based on the supplied entry point address & section details. |
| Pdb path | String | Path of the PDB file on the compiler machine |
| DetectItEasyInfo | String | Information that has been extracted using DetectitEasy |
| Malware config | String | Malware configuration refers to the settings and parameters within malicious software that dictate its behavior, |
| File size | Number | Size of the input file |
| Unix timestamp | Number | A timestamp showing when the file was compiled |
| Subsystem | Number | Defines whether the PE is made to be a Console or UI application |
| Section number | Number | Number of sections present in the PE |
| Resource number | Number | Number of resources present in the PE |
| Resources to file ratio | Number | Ratio between the size of the resources & the file itself |
| Digitally Signed | Boolean | Whether the digital signature is verified or not. |
| Packed | Boolean | Whether the input file is packed or not |
| Total exported functions | Number | Indicates the number of exported functions in a PE |
| Total imported functions | Number | Indicates the number of imported functions in a PE |
| Digital signature verification | String | Whether the digital signature is verified or not. |

| Field name | Type | Description |
| --- | --- | --- |
| Certificate Owner | String | Shows the owner of the certificate |
| Certificate is Revoked | Boolean | Shows whether the associated certificate is revoked |
| Certificate is SelfSigned | Boolean | Shows whether the associated certificate is selfsigned |
| Certificate is Expired | Boolean | Shows whether the associated certificate is expired |
| Certificate is Valid | Boolean | Shows whether the associated certificate is valid or not |

| Field name | Type | Description |
| --- | --- | --- |
| File characteristic | Number | Characteristics defining the behavior of the PE |
| DLL characteristic | Number | Features which make a PE actually portable in memory |

| Field name | Type | Description |
| --- | --- | --- |
| Disassembly Human descriptor | String | Indicates a Human description of a disassembly part of a PE |
| Disassembly Instruction Count | Number | Indicates the number of instruction of a disassembly part of a PE |

| Field name | Type | Description |
| --- | --- | --- |
| Dotnet | Boolean | Whether the executable file is using the .NET framework |
| Stream names | String | Descriptive identifiers for data streams within a .NET application, facilitating organized data management and manipulation. |
| Member reference names | String | Clear labels for variables, methods, and properties within a .NET assembly, enhancing code readability and maintainability. |
| Module names | String | Identifiers for discrete components or modules within a .NET application, aiding in modular development and component reuse. |
| Assembly Name | String | Unique identifier for a compiled .NET assembly, enabling versioning, deployment, and referencing within the .NET ecosystem. |
| Anti metadata | List of Boolean values | The "Anti metadata" feature detects various anomalies within .NET assemblies to thwart malicious attempts at obfuscation or tampering. It scrutinizes assembly tables for multiple rows, ensuring data integrity, and flags assemblies with invalid or self-referenced typeref entries. Additionally, it identifies assemblies with fake data streams and extra metadata table data, while also checking for hidden .NET data directories. This comprehensive approach aims to enhance the security and reliability of .NET applications. |

| Field name | Type | Description |
| --- | --- | --- |
| Image base | Number | “Base” address used if relocation doesn’t happen |
| Entry point section entropy | Number | Entropy of the section where the entry point resides |
| Entry point section entry point | Number | Value of the section where the entry point of the PE resides |
| Linker version(major) | Number | What version of linker what used at compilation time |
| Linker version(minor) | Number | What version of linker what used at compilation time |
| CFG | Boolean | Indicator whether CFG (Control Flow Guard) is enabled at compilation time. |
| CRC | Boolean | CRC (Cyclic Redundancy Check) is a boolean indicator that determines whether the CRC value calculated for a file matches the expected CRC value. |
| GS | Boolean | Indicator whether GS (Buffer Security Check *[Guarded Stack]*) is enabled at compilation time. |
| ASLR | Boolean | Indicator whether ASLR (Address space layout randomization) is enabled at compilation time. |
| Nxcompat | Boolean | Indicator whether NX compatibility (Data Execution Prevention *[No eXecute]*) is enabled at compilation time. |
| SEH | Boolean | Indicator whether SEH (Structured Exception Handler) is enabled at compilation time. |

| Field name | Type | Description |
| --- | --- | --- |
| Extracted Urls | String | Extracted URLs from the file |
| Extracted Domains | String | Extracted Domains from the file |
| Extracted Ips | String | Extracted Ips from the file |
| Extracted UUIDs | String | Extracted UUIDs from the file |
| Extracted Registry Paths | String | Extracted Registry Paths from the file |
| Extracted MD5 Hashes | String | Extracted MD5 from the file |
| Extracted SHA-1 Hashes | String | Extracted SHA-1 from the file |
| Extracted SHA-256 Hashes | String | Extracted SHA-256 from the file |
| Extracted SHA-512 Hashes | String | Extracted SHA-512 from the file |
| Extracted E-mails | String | Extracted Emails from the file |

| Field name | Type | Description |
| --- | --- | --- |
| Threat Indicators | String | An identifier to show what kind of rules (Threat indicator) Metadefender Sandbox itself matched on the target file. It can contain more info than what is present in the actual report |
| MITRE Techniques | String | An identifier to show what kind of rules (MITRE) Metadefender Sandbox itself matched on the target file. It can contain more info than what is present in the actual report |

Pdb guidResourcesRich Header Compiler IdsSectionsStringsImportsVersion info

| Field name | Type | Description |
| --- | --- | --- |
| Pdb guid | String | GUID of the PDB associated with the binary |

| Field name | Type | Description |
| --- | --- | --- |
| Size of resources | Number | Size of the resource |
| File type of the actual data | String | File type of the actual data |
| Language | String | Intended language of the resource |
| Sublanguage | String | Intended language of the resource |

| Field name | Type | Description |
| --- | --- | --- |
| Rich header compiler ids | String | An ID number to the specific compiler used during the compilation process |

| Field name | Type | Description |
| --- | --- | --- |
| Memory size of a section | Number | In-memory size of the section |
| Size of physical data | Number | Size of the physical data on-disk |
| Entropy of section | Number | Entropy of the specific section |

| Field name | Type | Description |
| --- | --- | --- |
| Strings | String | Extracted strings from the file |

| Field name | Type | Description |
| --- | --- | --- |
| DLL | String | Imported DLL of the input file |
| Functions | String | Imported functions from a specific dll |

| Field name | Type | Description |
| --- | --- | --- |
| Verinfo: File Description | String | Version information describing the file description of this application |
| Verinfo: File version | String | Version information describing the file version of this application |
| Verinfo: Internal name | String | Version information describing the internal name of this application |
| Verinfo: Legal copyright | String | Version information describing the legal copyright of this application |
| Verinfo: Product name | String | Version information describing the product name of this application |
| Verinfo: Product version | String | Version information describing the product version of this application |
| Verinfo: Company name | String | Version information describing the company name who created this application |

## [Threat Pattern Correlator Filters](/docs/filescan/3.2.0/datasheet/threat-pattern-correlator#threat-pattern-correlator-filters)

In addition to advanced technology, Threat Pattern Correlator provides multi filtering search parameters. This feature offers greater flexibility and ensures that users receive the most accurate and relevant results for their specific needs.

Query filtersNon Query filters

| Field name | Type | Possible values | Example | Description | Required |
| --- | --- | --- | --- | --- | --- |
| SHA-256 | String |  | Number |  | Yes |
| Submission data | Date | 2023-01-17T12:17:20.000Z | Number |  | Optional |
| Final Verdict | String | MALICIOUS, LIKELY-MALICIOUS, NO-THREAT, SUSPICIOUS, BENIGN, UNKNOWN | MALICIOUS | Verdict of a file | Optional |
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
