<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v220 -->

# Release Notes for v2.2.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Date: 6 February, 2025](/docs/filescan/3.2.0/release-notes/release-notes-v220#date-6-february-2025)

**What's New**

- **Setup Wizard**: A new setup wizard simplifies the initial admin configuration, licensing setup, and the addition of the MetaDefender Cloud Reputation API key. This enhances the ease of deployment for administrators, ensuring a smoother start for new users.

- **Zero-Day Office Document Support**: We now support the analysis of broken Office documents, including those used in zero-day attacks. This helps detect previously evasive threats targeting Office file vulnerabilities. auto$

- **Concatenated Archives Detection**: MetaDefender Sandbox can now analyze concatenated archives, a common bypass technique used by malware authors to evade detection. This improves our ability to detect malware hidden in complex archive structures. auto$

- **Mitigation for Bloated Executables**: A new mitigation feature identifies intentionally bloated executables that attempt to bypass sandbox environments. This enhances the platform's ability to analyze suspicious files that may try to evade detection. auto$

- **Adaptive Threat Indicators**: Threat indicators are now context-aware, allowing for more accurate identification of threats and a reduction in false positives. [Adaptive Threat Context](/docs/filescan/3.2.0/datasheet/adaptive-threat-context)

- **New Malware Family Detection**: Detection capabilities have been extended to include notable malware families such as WezRat, Remcos, Lumma Stealer, among others. This expands our database and improves detection across a wider array of threats. [Supported malware families via YARA](/docs/filescan/3.2.0/datasheet/supported-malware-families-via-yara)
- **JavaScript-Compiled PE File Support**: We’ve added unpacking and decompilation support for JavaScript-compiled PE files, enabling better analysis of malicious payloads that may be delivered through JavaScript.
- **Malicious Techniques Detection**: MetaDefender now identifies and flags malicious techniques such as disabling Data Execution Prevention (DEP), Authenticode evasion (SigFlip), and misleading script encoding. This enhances the platform's ability to spot sophisticated attack vectors.
- **Extended Threat Hunting Capabilities**: Threat hunting has been enhanced to identify open file directories, aiding in deeper investigation into suspicious activity.
- **New Similarity-Based Hashes**: Added new similarity-based hashes like .NET TypeRefHash and Gimphash, improving the detection of related malicious files through their structural similarities.
- **WebDAV Communications Identification**: MetaDefender can now identify WebDAV communications, improving the detection of network-based attacks that use this protocol. [Aether Tags](/docs/filescan/3.2.0/datasheet/sandbox-tags)
- **Enhanced Phishing Detection**: We’ve added 38 new brands to our phishing detection capabilities, significantly improving the platform’s overall phishing detection accuracy. Additionally, phishing URL rendering now bypasses SSL certification for missing sites. [What brands can the Brand Spoofing Detector catch?](/docs/filescan/3.2.0/datasheet/detected-brands)
- **Login Support for SAML & OKTA**: We now support SAML (protocol) and OKTA (identity provider) for secure, flexible login options in enterprise environments. [Okta](/docs/filescan/3.2.0/adminguide/okta)
- **Scan Execution Profiles**: Administrators can now create and manage custom scan execution profiles, providing more control over how different file types and threats are analyzed.
- **Support for Password-Protected Office Documents**: MetaDefender now supports the analysis of password-protected Office documents, improving its ability to handle encrypted files during analysis.
- **UNC Paths on IOCs Page**: The IOCs (Indicators of Compromise) page now supports UNC path display, providing easier access to file locations in network environments.
- **Exported Reports (My Downloads)**: Users can now view exported reports directly on the "My Downloads" page, streamlining access to previously generated reports. [Output Report Formats](/docs/filescan/3.2.0/datasheet/export-formats)
- **Settings for HTML & PDF Report Generator**: Added customizable settings for generating HTML & PDF reports, offering greater flexibility in report formats and content. [Output Report Formats](/docs/filescan/3.2.0/datasheet/export-formats)
- **Certificate Details for RDP Files**: MetaDefender now provides detailed certificate information for RDP (Remote Desktop Protocol) files, aiding in deeper analysis of network-based threats.
- **ODF File Details**: Support for ODF (Open Document Format) files has been enhanced, now showing more detailed analysis of these file types.
- **More Detailed Information for GoLang Files**: We've expanded the level of detail provided in the analysis of GoLang files, improving detection of threats in this increasingly popular language.
- **Similarity Search for All File Types**: Similarity search now supports all file types, not just PE files, expanding its ability to detect malicious files based on structural similarities. [Threat Pattern Correlator - Support for Non-Executables](/docs/filescan/3.2.0/datasheet/threat-pattern-correlator-nonpe)
- **Support for Online Installation on RedHat 9**: MetaDefender now supports online installation on the RedHat 9 operating system, expanding compatibility for enterprise deployments. [Technical Requirements](/docs/filescan/3.2.0/installation/technical-requirements)
- **Rename "Threat Intelligence" to "Similarity Search"**: The "Threat Intelligence" feature has been renamed to "Similarity Search" to better reflect its functionality.
- **WebThreat URL Threat Detection Model:** Enabling advanced phishing detection through network data analysis for enhanced URL threat protection. [Web Threat Analyzer Overview](/docs/filescan/3.2.0/datasheet/webthreat)

**Improvements**

- **Username Length Limit**: The username length limit has been increased from 30 characters to a configurable length (default is 60 characters), giving users more flexibility in naming conventions.
- **Changed Default Sample Retention Period**: The default retention period has been decreased to 14 days for non-malicious samples and to 90 days for malicious samples, alleviating disk space issues for high-volume deployments. This change only affects new installations.
- **Enhanced File Type Analysis**: Analysis for APK, RDP, Shell Script, and CHM files has been expanded, improving detection capabilities across these file formats.
- **Improved Python Unpacking**: The integration of pydecipher enhances Python unpacking, improving detection of obfuscated Python malware.
- **Improved Phishing & Geofencing Detection**: We’ve enhanced our detection for phishing attacks, geofencing, and Chrome extensions to ensure better protection against emerging threats.
- **Heuristic Enhancements for Packed Executables**: The heuristic engine has been upgraded to better detect packed executables, which are commonly used to obfuscate malware.
- **Extended .NET Obfuscation Detection**: We’ve improved detection for obfuscated .NET assemblies and added better handling for unmanaged .NET functions, making it easier to detect threats hiding in .NET-based applications.
- **XOR Decryption Improvements**: XOR decryption capabilities have been enhanced for PE files and URLs, increasing the platform’s ability to analyze encrypted malware.
- **Extended Adaptive Context for Executables and Emails**: The adaptive context feature has been expanded to include deeper analysis of executables and email files, improving detection of hidden threats.
- **Extended Base64 Decoding for Downloaded Files**: The platform now supports extended base64 decoding for downloaded files, enhancing its ability to analyze encrypted or obfuscated content.
- **Blacklist for Abused Certificates**: We’ve extended the blacklist for abused certificates and bootloaders, improving protection against threats using known malicious certificates.
- **Whitelist Accuracy**: The file whitelisting process has been fine-tuned for greater accuracy, ensuring only trusted files are excluded from scans.
- **Improved Emulation Support**: Emulation for JavaScript coming from email attachments has been extended, improving detection of email-borne JavaScript threats.
- **API Page Improvements**: The API page now includes up-to-date examples, input parameters, and possible outputs, making the integration process smoother for developers.
- **Improved Application Stability**: Stability improvements across the platform ensure a smoother and more reliable user experience.
- **Decreased MongoDB Memory Usage**: MongoDB is configured to use 25% of system RAM for caching purposes (the limit was 50% previously). This change improves the overall system stability, especially under heavy load.
- **Polyglot Detection**: The ability to detect polyglot files has been improved, increasing the platform’s ability to identify files that contain multiple formats.
- **Enhanced Emulation for Common Threats**: Emulation for VBA, JavaScript, PowerShell, Microsoft Equation, and shellcode has been improved, providing deeper analysis for common attack techniques.
- **Improved PE Signature Validation**: PE file signature validation has been enhanced, improving detection of malicious files and ensuring more accurate assessments.
- **Improved QR Code Analysis**: Enhancements to QR code analysis allow for better identification of hidden threats and malicious links within QR codes.
- **Improved health check for broker and transform components** with updated status codes (200 for up, 503 for down)

**Bug Fixes**

- **License Corruption**: A bug that caused license corruption when disk space was very low has been fixed, ensuring a stable experience even in resource-constrained environments.
- **Geolocation Data**: Missing report geolocation data and related statistics are now correctly displayed, ensuring accurate tracking of threat origins.
- **Offline Font and Icon Fetch Timeout**: Fixed an issue that caused timeouts while fetching fonts and icons in offline environments, improving reliability when working in isolated systems.
- **SHA-256 Hash Search**: Fixed an issue where incorrect results were returned during SHA-256 hash searches, ensuring more accurate file matching.
- **Ad-Blocker Sign-Up Issue**: Resolved an issue where certain ad-blockers would hide the Privacy Policy checkbox during user sign-up, improving the user registration experience.
- **VBA Macro Signature Detection**: A bug in the VBA macro signature detection has been resolved, ensuring more accurate detection of malicious macros in Office files.
- **Oledump Tool Update**: The oledump tool has been updated to reduce the incorrect extraction of strings, improving the analysis of OLE files.
- **Offline Table Instructions**: Fixed instructions for offline use to improve the clarity and usability of the system when operating in isolated environments.
- **Transform Instance Activation Fix**: Resolved an issue with activating transform instances in multi-server deployments, ensuring proper functionality after restarts.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
