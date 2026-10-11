<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/release-notes/file-structure-validation-release-notes -->

# File Structure Validation release notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [v2.1.0](/docs/mdcore/v5.22.1/release-notes/file-structure-validation-release-notes#v210)

Release date: 9/23/2026

- Supported structure validation for HDF5, HL7, GDBTABLE, LPKX, MPKX, and Pickle AI model files.
- Supported DICOM encapsulated object extraction, including handling of preamble data.
- Supported returning embedded objects and external image link from Microsoft Office 2003 files.
- Supported streaming of returned objects to improve performance and less disk I/O.
- Added standard validation references to the validation result.
- Added schema upgrading logic for the selected object types setting.

## [v2.0.0](/docs/mdcore/v5.22.1/release-notes/file-structure-validation-release-notes#v200)

Release date: 8/27/2026

- Validates file structure across 160+ supported formats.
- Extracted embedded objects from the file and applied the full processing pipeline to each.
- Blocked files based on object-level policies.
- Supported polyglot file detection and blocking.
- Supported XML Schemas validation.
