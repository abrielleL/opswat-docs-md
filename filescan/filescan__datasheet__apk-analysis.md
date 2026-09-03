<!-- source: https://www.opswat.com/docs/filescan/datasheet/apk-analysis -->

# Android Application Package (APK) Analysis

Android applications are a frequent vector for malware delivery, posing significant risks to both users and organizations. MetaDefender Aether can play a crucial role in detecting malicious behavior within APK files through in-depth static analysis.

Our sandbox offers advanced APK analysis capabilities, providing deep insights into Android malware:

- **APK file parsing**: Extracts essential metadata and structural information, such as requested permissions, signing certificates, and registered receivers and services.
- **Certificate validation and whitelisting**: Reduces false positives and enhances trust assessment, especially for widely distributed APK.
- **Code disassembly and resource decoding**: Powered by Apktool, enabling reverse engineering of APKs.
- **Smali code analysis**: Leverages a proprietary smali parser to identify risky method calls by analyzing the assembly-like code.
- **Extensive threat detection**: 100+ threat indicators to enable detection of unknown mobile malware.
- **MITRE Mobile Matrix**: Extended coverage of the MITRE Mobile Matrix. Check it out [here](https://www.opswat.com/docs/filescan/3.1.1/datasheet/mitre-attack-coverage#mitre-mobile-matrix).

## [Showcase Report: Detecting Cerberus and its malicious capabilities](/docs/filescan/datasheet/apk-analysis#showcase-report-detecting-cerberus-and-its-malicious-capabilities)

Cerberus

Android banking Trojan that steals sensitive and confidential banking data.

Here we can see how Cerberus can intercept communications (using high priority intents), including one-time passwords and transaction verification codes from banking apps, allowing attackers to bypass two-factor authentication. Check out the full report [here](https://www.filescan.io/uploads/679a56fba2886cdc5ac63ebb/reports/0611de87-6957-43e6-b644-d3fddc24cdd3)!

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
