<!-- source: https://www.opswat.com/docs/mdcore/release-notes/predictive-alin-ai-release-notes -->

# Predictive Alin AI release notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## **V 3.6.0**

Release date: 30 September 2026

- Added concurrent scanning, significantly increasing throughput on multi-core systems with no change to verdicts, with the largest gains on Android APK files.
- Added a configurable limit on simultaneous resource-intensive scans to keep memory usage stable under heavy load.
- Added a unique rule identifier to rule-based, signature and reputation detections, shown in the reported threat name.
- Updated the detection database format. This engine version requires a matching database version, and incompatible databases are now rejected cleanly at startup.
- Improved startup performance, with lower memory usage, faster startup and a significantly smaller detection database.
- Improved scan time on very large files while maintaining full detection coverage.
- Improved resilience against malformed files, eliminating hangs and crashes and reducing memory usage when processing them.
- Improved PDF detection accuracy.
- Fixed a crash when scanning certain malformed Windows executables, which left the file without a verdict.
- Fixed a detection gap on certain Windows executables carrying multiple digital signatures.
- Fixed validly signed large Windows executables being treated as unsigned.
- Fixed a lost verdict when certain files containing malicious embedded content were rescanned.
- Fixed false positives on legitimate legacy Windows applications, certain PDF files and other files identified in the field.

## **V 3.5.0**

Release date: 31 August 2026

- Added analysis and detection for additional image formats (JP2, EXR, PSD, PCX, TGA, DDS), covering common image-based attack techniques, initially in monitoring mode.
- Added recognition of archive and container formats so they are handled correctly:

  - 7Z, RAR, GZ, BZ2, XZ, CAB, PKG/XAR, RPM, DEB, TAR, DMG and ZIP
  - ODT, ODS, ODP, ODG, OTT, OTS, OTP, EPUB, APPX, MSIX, ASICE, XPS, OXPS, HWPX, PBIX, PBIVIZ, THMX, VSDX, VSTX and TDSX
- Added recognition of legacy Visio (VSD, VST, VSS), Publisher (PUB) and Project (MPP) files, and distinguished Word templates (DOT) from documents.
- Added malicious macro detection for Excel binary workbooks (XLSB), matching existing coverage for other macro-enabled Excel formats.
- Added deeper analysis of .NET applications, including detection of obfuscated or packed files.
- Added HTML file detection, including analysis of embedded content.
- Added optional detection of hidden data appended to PNG and JPEG images, disabled by default.
- Enabled machine-learning detection for Office documents (DOCX, XLSX, PPTX).
- Updated the script detection model.
- Improved Android APK analysis, including more reliable handling of malformed or obfuscated packages.
- Improved performance when running multiple scans in parallel.
- Improved XML file detection, including support for additional encodings and formats.
- Improved performance of repeated scans of the same file.
- Fixed scan failures on certain PDF files, such as those produced by print or mail systems.
- Fixed false positives on plain-text emails containing PDF-like text.
- Fixed Java class files being misidentified as macOS executables.
- Fixed inconsistent threat names on some detections.
- Fixed false positives and slow scans on certain large Microsoft installers and redistributables.
- Fixed false positives on large animated GIF images.
- Fixed an issue where scanned files could remain locked after scanning, which could prevent drives from being unmounted.

## **V 3.4.3**

Release date: 17 August 2026

- Added detection of malicious macros in Office documents (DOCM, XLSM, PPTM) and legacy Office files.
- Added detection of malicious scripts embedded in PDF documents.
- Added scanning of Outlook MSG email bodies for malicious content.
- Added detection of malicious scripts embedded in SVG files.
- Added support for macro-enabled and template PowerPoint files:

  - PPTM, POTM, PPSM, PPAM
- Added reputation-based detection of known malicious and phishing URLs, IP addresses and domains.
- Added new detection rules for malicious HTML content.
- Added configurable control over which files extracted from containers are deep-scanned.
- Updated detection models for Android APK and PDF files with improved accuracy.
- Improved engine startup time and memory usage.

## **V 3.4.2**

Release date: 13 August 2026

- Added support for scanning Android APK files, alongside existing support for Windows, Linux, PDF and Office files.
- Added detection of malicious content in EML email bodies, along with support for scanning standalone script and text files.
- Improved protection of the detection database, which is now encrypted at rest.
- Updated the detection database.
- Fixed an issue where macro-based detection did not apply to macro-enabled Word documents (DOCM and DOTM).

## **V 3.4.1**

Release date: 06 August 2026

- Added detection of malicious content hidden inside image files, targeting image-poisoning campaigns.
- Added malicious macro detection for Excel files:

  - XLSM, XLTX, XLTM, XLAM
- Added new behavioral detection rules for Windows executables.
- Improved accuracy on Office documents by reducing false positives on legitimate files.
- Fixed a crash that could occur when the engine shut down.
- Fixed an issue in version 3.4.0 where macOS executables received no verdict.
- Fixed an issue where detection database packages for versions 3.4.0 and 3.4.1 could not be uploaded to MetaDefender Core v5.19.0 and v5.20.0.

## **V 3.4.0**

Release date: 03 August 2026

- Enabled signature, heuristic and rule-based detection for Windows, Linux and macOS executables, PDF, Office and image files.
- Added optional deep inspection of Windows, Linux and macOS executables, disabled by default with no performance impact when off.
- Added scanning support for macOS archive containers that were previously not scanned.
- Added detection of malicious scripts hidden in image metadata.
- Fixed certain valid BMP images being rejected as an unknown file type.
- Fixed Java archive (.jar) files that cannot be extracted, including encrypted ones, being reported as malicious; they are now reported as unsupported.

## **V 3.3.3**

Release date: 28 June 2026

- Added content-based video file recognition.

  - Supported formats: MP4, AVI, MKV, MOV, WebM, FLV, WMV

## **V 3.3.2**

Release date: 21 June 2026

- Added recognition of audio files.
- Fixed an engine startup failure on MetaDefender Core v5.18.0 in certain virtualized environments.

## **V 3.3.1**

Release date: 16 June 2026

- Improved file type recognition for Adobe Illustrator (.ai) files.
- Improved scanning performance for Office documents.
- Fixed an issue where reputation-based detection failed to start on Linux.

## **V 3.3.0**

Release date: 9 June 2026

- Added multi-layered detection for image files used as attack vectors.

  - Machine-learning detection for images is enabled in Deflection mode and disabled in Detection mode.
- Added detection of suspicious, malformed or malicious Office documents (DOCX, XLSX, PPTX).
- Added analysis of Android APK files to support machine-learning detection.

## **V 3.2.3**

Release date: 27 May 2026

- Added support for legacy Office files (.doc, .xls, .ppt) and Outlook messages (.msg), including those containing macros, with safe handling of malformed files.

## **V 3.2.2**

Release date: 20 May 2026

- Added analysis of links found in PDF, Office and EML files.
- Fixed file type recognition failures on certain macOS executables.
- Fixed an issue where scanned files remained locked for several minutes after scanning, preventing drives from being unmounted.

## **V 3.2.1**

Release date: 11 May 2026

- Added more precise recognition of executable types, so installers, firmware and similar files are routed to the appropriate engines instead of being scanned as standard executables.
- Added support for additional Linux file types.
- Updated detection capabilities for Windows, Linux, macOS and PDF files.
- Removed Office and image files from detection.
- Fixed an issue where scanning certain Linux files could exhaust system memory.
- Fixed a scan-time slowdown when scanning SD cards over USB on MetaDefender Smart Touch.

## **V 3.2.0**

Release date: 04 May 2026

- Added recognition of email (EML) files so they are analyzed instead of skipped.
- Added recognition of legacy Office documents (DOC, XLS, PPT) and Outlook messages (.msg).
- Added recognition of Android APK files.
- Added image scanning with settings configurable per scanning profile.

  - Supported formats: JPG/JPEG, PNG, WEBP, GIF
- Added per-document-type settings for DOCX, XLSX and PPTX files.
- Added analysis of links embedded in files.
- Added support for older CPUs on Linux and Windows, selected automatically at startup.
- Added support for 32-bit deployments.
- Improved compatibility with older Linux distributions.
- Improved performance under high parallel scan load.
- Fixed a false positive where a third-party antivirus flagged a file in the engine package.

## **V 3.1.4**

Release date: 27 April 2026

- Fixed a false positive on a legitimate Windows utility bundled with third-party industrial software.

## V 3.1.3

Release date: 14 April 2026

- Fixed a scan hang and high memory usage on certain malformed PDF files.
- Fixed false positives on certain legitimate Windows and macOS files, including installers and developer tools.

## V 3.0.1

Release date: 31 March 2026

- Fixed files not being scanned when their paths contained forward slashes.
- Fixed an engine crash during batch scanning.
- Improved detection reliability for Windows executables.

## V 3.0.0

Release date: 23 March 2026

Release type: MAJOR

- General Access release of Predictive Alin AI for customer-facing enterprise use.
- Reputation integration to improve deflection decisions for known good and known bad files.
- File type detection optimized for malware screening workflows across:

  - Executables: PE, ELF, Mach-O
  - Documents: PDF
- File parsing for PE, ELF, Mach-O, and PDF to extract structural signals used as context for ML inference.
- Integration availability:

  - **MetaDefender Cloud** - Predictive Alin AI runs inline as part of the MetaScan package.
  - MetaDefender Core - Predictive Alin AI runs inline as part of the MetaScan package on Linux and Windows.
- Standardized engine verdict codes: Reference: <https://www.opswat.com/docs/mdcloud/integrations/description-on-scan-result-codes>

  - 0 - No Threat Detected
  - 1 - Infected: The file was analyzed and determined to be malicious.
  - 10 - Not Scanned: The file was not analyzed (for example, due to size limits or an internal processing error).
  - 23 - Unsupported File Format: The file type is not currently supported by the engine.
- Threat detection naming convention for policy integration:

  - Format: <platform>/malicious_<threat_confidence>
  - Platform mapping:

    - Windows - PE-based executables
    - Linux - ELF-based binaries
    - Darwin - Mach-O-based binaries
    - Generic - non-platform-specific formats such as PDF
  - Examples:

    - PE: Windows/malicious_99
    - ELF: Unix/malicious_99
    - Mach-O: MacOS/malicious_99
    - PDF: Generic/malicious_99

Info

Known considerations

- This is the first General Access release. Establish an initial operational baseline before tightening policy.
- Malicious naming outputs are standardized for policy integration and should be interpreted alongside the broader security context.

## Introduction

Predictive Alin AI 3.0.0 marks the **General Access release** of OPSWAT’s proprietary machine learning-driven malware detection engine, purpose-built for **high-speed, pre-execution protection** in modern, high-throughput environments.

**What This Means for MetaDefender Customers?**

- **Predictive Alin AI** is fully integrated into the MetaDefender platform and accessible across all products and environments, available in both **cloud and on-premises environments**, supporting **Windows and Linux** operating systems
- **Predictive Alin AI** operates in parallel to MetaScan to enhance detection coverage via machine learning algorithms enhanced by MetaDefender Aether’s dynamic analysis, for reduced false positives and zero-day detection
- **Predictive Alin AI** targets the primary malware entry points, with extensive support for executable formats and PDF files, where most modern threats originate.

**How Is Predictive Alin AI Continuously Improving?**

Predictive Alin AI has a documented Machine Learning pipeline lifecycle concept for transparency, including:

- Data ingestion and normalization controls (hashing, deduplication, validation)
- Labeling and enrichment through MetaDefender Aether using multi-source evidence (static characteristics, dynamic analysis context, consensus-oriented verdict context, and threat intelligence enrichment)
- Training, evaluation, and quality gating against false-positive benchmarks before promotion
- Continuous refresh and monitoring to adapt to malware evolution

### Key Benefits

- Fast, pre-execution malware detection (P99 under 100ms) to enable allow, block, and quarantine decisions at scale.
- Faster scan times for high-volume workflows while improving accuracy and reducing false positives (0.1% False Positive Rate and over 90% accurcacy across the board)
- Extensive support for executable formats (PE, ELF, Mach-O) plus PDF for common document-borne threats.
- Available as a custom engine in MetaDefender Cloud and MetaDefender Core.

**Next Steps to Upgrade:**

Customers currently using MetaDefender products can add Predictive Alin AI to unlock high-speed, machine learning–based detection for pre-execution threats while retaining familiar multiscanning capabilities. To discuss upgrade options or transition planning, please contact your OPSWAT representative.

**Predictive Alin AI** reflects where we’re heading with pre-execution malware detection: faster decisions, better accuracy, and the ability to handle high-volume environments without added complexity.

### Compatibility

- Platforms: Windows, Linux
