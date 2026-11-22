<!-- source: https://www.opswat.com/docs/mdcore/release-notes/file-structure-validation-release-notes -->

# File Structure Validation release notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [v2.1.3](/docs/mdcore/release-notes/file-structure-validation-release-notes#v213)

Release date: 11/18/2026

- Supported SZIP file structure validation, including validation of its sub-components.
- Supported schema-based JSON validation.
- Detected unlisted entries in ZIP files:

  - Added an option to extract unlisted entries so they can be scanned by other engines.
- Reported additional object types in Office files:

  - ActiveX controls and VSTO macro objects in Office Open XML and legacy Office files.
  - DDE objects in legacy Office files.

- Extracted analyzed objects from RTF files, including images, hyperlinks, DDE, embedded objects, embedded fonts, and metadata.
- Supported detection of stacked polyglot files for the DICOM format.

## [v2.1.2](/docs/mdcore/release-notes/file-structure-validation-release-notes#v212)

Release date: 11/4/2026

- Reported metadata and embedded fonts found in PDF and Microsoft Office 2003 documents.
- Reported DDE objects found in Microsoft Office documents.
- Delivered analysis results sooner for files that produce objects gradually, instead of waiting for a full batch.
- Supported validation of big-endian GGUF files.
- Applied the Selected Object Types setting earlier for Microsoft Office documents, so object types that are not selected are no longer extracted.
- Fixed extracted files being blocked because of an extension mismatch.

## [v2.1.1](/docs/mdcore/release-notes/file-structure-validation-release-notes#v211)

Release date: 10/14/2026

- Reduced Stack Polyglot false positives
- Returned orphaned objects found by the PDF analyzer.
- Improved the XML schema validation output when validation fails.
- Reported more types of embedded content as soon as it is found.
- Fixed polyglot detection failures, slow processing when many files were scanned at the same time.
- Fixed the Schemas Validation setting having no effect when disabled.

## [v2.1.0](/docs/mdcore/release-notes/file-structure-validation-release-notes#v210)

Release date: 9/23/2026

- Supported structure validation for HDF5, HL7, GDBTABLE, LPKX, MPKX, and Pickle AI model files.
- Supported DICOM encapsulated object extraction, including handling of preamble data.
- Supported returning embedded objects and external image link from Microsoft Office 2003 files.
- Supported streaming of returned objects to improve performance and less disk I/O.
- Added standard validation references to the validation result.
- Added schema upgrading logic for the selected object types setting.

## [v2.0.0](/docs/mdcore/release-notes/file-structure-validation-release-notes#v200)

Release date: 8/27/2026

- Validates file structure across 160+ supported formats.
- Extracted embedded objects from the file and applied the full processing pipeline to each.
- Blocked files based on object-level policies.
- Supported polyglot file detection and blocking.
- Supported XML Schemas validation.
