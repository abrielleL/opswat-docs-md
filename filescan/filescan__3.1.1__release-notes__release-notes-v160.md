<!-- source: https://www.opswat.com/docs/filescan/3.1.1/release-notes/release-notes-v160 -->

# Release Notes for v1.60

---

## [Date: 28 October, 2022](/docs/filescan/3.1.1/release-notes/release-notes-v160#date-28-october-2022)

Added:

- Added ability to extract and validate certificate data from OOXML files
- Added sample feed (public/private) with archive downloads
- Added support for CustomXMLParts
- Added support for the Format function
- Added "runWebserviceHealthCheckGracefulExitIfLastSuccessOlderThanXSec" to initiiate a soft restart in a rare deadlock scenario
- Added support for ACE files
- Added support for Microsoft Store apps ("ms-appx" tag and mime-type "application/vns.ms-appx")
- Added ability to specify multiple VirusTotal API keys in fsTransform
- Added ability to disable OSINT cache (see 'enableOSINTCache')
- Added ability to abort additional OSINT lookups if malware found (see 'abortOSINTLookupIfAnyProviderFoundMalware')
- Added a configurable "dark mode" for the webservice UX
- Added a beta-version of "Rapid mode" and individually configurable analysis options on the submission dialogue (admin-only)

Changed:

- Performance improvements for OOXML files with many AX controls
- Improved detection of embedded PE files
- Improved the performance of webservice background jobs
- Improved handling very large (50MB+) PDF and PE files

Fixed:

- Fixed a few minor bugs in the emulation engine

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
