<!-- source: https://www.opswat.com/docs/filescan/3.1.1/release-notes/release-notes-v180 -->

# Release Notes for v1.8.0

---

## [Date: 8 June, 2023](/docs/filescan/3.1.1/release-notes/release-notes-v180#date-8-june-2023)

Warning

This version is not suitable for a clean installation due to breaking changes introduced in Docker 25. Please **use version 1.9.2 or later** for clean installations!

Added:

- A new **single source of truth** reputation lookup for Hashes, URLs, IPs, and Domains. Automatically integrated with [MDCloud](https://docs.opswat.com/mdcloud) look up. Always yielding a result, independent of whether a report was generated for the search query.

- Threat Intelligence Similarity Search feature for Portable Executable (PE) files

- Emulation metadata parsing from self-extracting archive files
- Detection of appended files in images with steganography
- Administrative feature to overrule scan report verdict
- Detection of file executions initiated by msiexec on remotely fetched MSI files

Changed:

- Extended certificate whitelisting with QT Framework signatures
- Extended Filescan Reputation API with support for IPs, domains and URLs
- Extended Filescan Fuzzy Hash blacklist hits with additional details
- Optimized JPG processing speed
- Fine -tuned YARA rule behaviors
- Fine-tuned fuzzy hash lookup verdict contribution
- Improved RTF emulation success rate
- Enhanced startup time with lighting fast speed and performance
- Improved verdict calculation

Fixed:

- Service stability issues
- Service availability issues via automated restart mechanism
- Backend disk usage issues
- Backend service error handling issues
- Phishing URL detection issues
- OSINT provider verdict standardization issues

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
