<!-- source: https://www.opswat.com/docs/filescan/3.1.1/release-notes/release-notes-v174 -->

# Release Notes for v1.7.4

---

## [Date: 20 April, 2023](/docs/filescan/3.1.1/release-notes/release-notes-v174#date-20-april-2023)

Added:

- Added [Status Page](https://www.filescan.io/help/status) to inform users about historical health
- ‘What is your opinion about this sample’ vote feature, to influence accuracy of the Filescan verdict engine by users
- [Reputation API](https://docs.opswat.com/filescan/opswat-filescan/ref) with improved performance to provide overall verdict for SHA256 hashes, based on different trusted sources
- Yara rules now available in offline mode (static database, updated with each release)

Changed:

- Support for additional file types (TNEF, OneNote)
- Improvement on verdict precision (ex.: detect invalid digital certifications as malicious, detect suspicious Python patterns)

Fixed:

- Product installer - several native dependencies and Python packages are bundled into the installer, reducing installation time and potential issues
- Verdict inaccuracies

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
