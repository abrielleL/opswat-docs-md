<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v170 -->

# Release Notes for v1.70

View as Markdown Ask ChatGPT about this page Ask Claude about this page

---

## [Date: 16 December, 2022](/docs/filescan/3.2.0/release-notes/release-notes-v170#date-16-december-2022)

Added:

- Support for VHD(x) file formats
- Added a logo picker that can be used to re-brand the product
- Added the option to disable the T&C accept checkbox (admin backend)
- Added the option to specify the product name (admin backend)
- Added better support for large PE files (>100MB)
- Added new threat indicators covering CPL file anomalies
- Added 'runYaraRulesOnInputFileMaxFileSizeInMb' for better control on when to skip YARA being applied to the input file
- Added media-type based prioritizing of archive files
- Added separately configurable max. processing thresholds for archive submissions
- Added media type to the /submit endpoint response (fsBroker)
- Added composition fields containing counters for all submitted, accepted and rejected files

Changed:

- Updated emulation engine
- Updated documentation (added troubleshooting guide)
- Improved heuristic javascript/vbs/powershell detection for text files without a suffix
- Default max. file size for processing is now 2GB

Fixed:

- Some potential performance issues with statistics related DB queries

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
