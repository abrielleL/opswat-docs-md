<!-- source: https://www.opswat.com/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes -->

# OPSWAT AI Content Inspector release notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [V 2.3.1](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-231)

Release date: 29 September 2026

Release type: MINOR

AI Content Inspector 2.3.1 adds support for WMF/EMF images and OpenDocument spreadsheets and presentations, introduces a Linux NVIDIA GPU engine package, and delivers updated image and text detection models, revised default confidence thresholds, and stability fixes for e-mail, Office, and text processing.

#### [**New Features**](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#new-features)

- Added support for WMF and EMF images (.wmf, .emf)
- Added support for OpenDocument spreadsheets and presentations (.ods, .ots, .odp, .otp)
- Added a Linux NVIDIA GPU engine package (requires CUDA 13.0 and NVIDIA driver R580 or newer)
- Added engine and database versions to every scan result
- Added metadata forensic analysis for images attached to .eml and .msg messages

#### [**Changes and Improvements**](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#changes-and-improvements)

- Updated the ML SDK from 1.7.0 to 1.8.0, model weights from 1.7.0 to 1.8.0, and the DB API from 10 to 11
- Replaced OriginLens v0.5.1 with v1.4.2 in both FAST and FORENSIC profiles. The CNN and CommFor detectors and image heat maps have been removed; `output_images` remains available in the Core interface
- Replaced the RoBERTa text classifier with Ettin-17m in the FORENSIC profile, and added Ettin-17m as a second text verdict source in the FAST profile
- Updated default confidence bands: images now use 60/40 (previously 70/30), and the text suspicious threshold is now 50 (previously 45). Workflows still using the previous defaults are migrated automatically
- Texts shorter than 45 words are no longer scored and are reported as Uncertain
- Python engine modules are now compiled with Nuitka

#### [**Bugfixes**](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#bugfixes)

- Fixed an issue where scanning .msg files with certain code pages failed with error code 1
- Fixed an issue where correctly typed .msg files were rejected as unsupported
- Fixed an issue where capture date, camera, and GPS values stored in nested EXIF IFDs were not read
- Fixed an issue where the fraud result was reported as `not detected` when the fraud classifier did not run; it is now reported as `not scanned`
- Fixed an issue where unreadable Office documents were reported as an unsupported file type; they now fail with `err_code` 1 and a descriptive error message
- Fixed an issue where files with no extractable text returned a model score; they now report text as Not Detected
- Fixed an issue where text scans did not fail when the required text classifier could not be loaded

## [V 2.3.0](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-230)

Release date: 14 September 2026

Release type: MAJOR

AI Content Inspector 2.3.0 introduces support for Microsoft Office document formats, adds engine lifecycle notifications, and includes improvements to document text processing, an ML model update, and fixes for result consistency.

#### [**New Features**](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#new-features)

- Added support for Microsoft Word documents (.docx, .docm, .doc, .rtf, .odt)
- Added support for Microsoft PowerPoint presentations (.pptx, .pptm, .potx, .potm, .ppsx, .ppsm, .ppt, .pot, .pps)
- Added support for Microsoft Excel spreadsheets (.xlsx, .xlsm, .xltx, .xltm, .xlam, .xlsb, .xls, .xlt)
- Added out-of-support lifecycle notifications, informing users when the engine version reaches end of support

#### [**Changes and Improvements**](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#changes-and-improvements)

- Reworked document text cleaning to improve the quality and consistency of text extracted for analysis
- Improved the performance of markdown text cleanup

#### [**Bugfixes**](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#bugfixes)

- Fixed an issue where the result JSON could be inconsistent when preferences were misconfigured
- Fixed an issue where sub-verdicts could be inconsistent when scanning with some features disabled

## [V 2.2.0](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-220)

Release date: 14 August 2026

Release type: MAJOR

AI Content Inspector 2.2.0 introduces support for additional email file formats, expands forensic analysis capabilities for embedded images, and includes improvements to provenance validation, image processing, and overall engine stability.

#### [New Features](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#new-features)

- Added support for **E-mail Message (.eml)** files
- Added support for **Microsoft Outlook Message (.msg)** files
- Added **metadata forensic analysis for images embedded within PDF documents**, enabling the engine to inspect image-level metadata and forensic signals extracted from PDF content

#### [Changes and Improvements](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#changes-and-improvements)

- Strengthened **C2PA provenance validation and handling** to improve reliability when analyzing Content Credentials and provenance information
- Improved **image input normalization** to provide more consistent preprocessing across supported image formats and improve downstream analysis reliability

#### [Bug Fixes](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#bug-fixes)

- Fixed a dependency issue affecting the **C2PA library**
- Fixed processing issues affecting **EPS files**
- Fixed an issue where **grayscale and bilevel EPS images** could fail during processing
- Resolved a stability issue where processing **FPX files** could cause the scan to terminate unexpectedly. **FPX is no longer supported** by AI Content Inspector
- Fixed an issue affecting **LA-mode images**, including certain `.cur` cursor files, which could fail with a `"not enough image data"` error

## [V 2.1.1](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-211)

Release date: 10 August 2026

Release type: MINOR

- Detect AI Model Family from Image Metadata
- New OriginLens image detector
- Improved speed for image scanning (fast & forensic mode)
- Google SynthID watermark detection for images is now reported under its proper name, consistent with the text watermark detector
- Text detector display names aligned with the detection SDK
- Fixed legitimate high-resolution images failing with "Image size exceeds limit … could be decompression bomb". The limit is now 250 megapixels by default and configurable via AIGCD_MAX_IMAGE_PIXELS
- Fixed image fingerprint detection failing on files with malformed XMP metadata
- Fixed scans aborting when an embedded image inside a document could not be decoded
- Fixed Stable Diffusion 3 provenance being reported under an inconsistent model name

## [V 2.1.0](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-210)

Release date: 13 July 2026

Release type: MAJOR

- Introduce Fast mode and Forensic mode

  - Fast mode: Optimized for high-speed analysis with a fast response
  - Forensic mode: Optimized for deep analysis and investigative workflows
- Added an option to disable output image generation
- Improved PDF extraction performance
- Improved scan performance with faster processing times

## [V 2.0.1](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-201)

Release date: 28 May 2026

Release type: MINOR

- Upgraded the core image and text detection components for improved accuracy and performance
- Resolved issues affecting text scanning functionality
- Enhanced support for offline and packaged deployments

## [V 2.0.0](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-200)

Release date: 21 May 2026

Release type: MAJOR

- Added 10 new image detectors to analyze AI-generated footprints in visual content
- Introduced 9 new text detectors to identify AI-generated footprint signals in textual content
- Enhanced results page with deeper insights, providing more detailed outputs from individual detectors, including images and analysis breakdowns
- Introduced a new Uncertain Hits Threshold setting to improve control over uncertain detection results
- Added support for PDF file type including both AI text detection and AI image detection workflows
- Introduced fraud detection support for the following content types:

  - Invoice fraud
  - Car accident insurance fraud
  - Home insurance fraud

## [Introduction](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#introduction)

OPSWAT AI Content Inspector 2.0.0 marks the General Availability release of OPSWAT’s proprietary AI-powered content authenticity and document fraud detection engine. Purpose-built for modern, high-throughput environments, AI Content Inspector helps organizations identify AI-generated content and detect AI fraudulent documents with speed and accuracy.

## [Fully Integrated with the MetaDefender Platform](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#fully-integrated-with-the-metadefender-platform)

AI Content Inspector is fully integrated into the MetaDefender platform and is available across MetaDefender products and deployment environments, including both cloud and on-premises installations on Windows and Linux.

Working alongside Proactive DLP and Deep CDR, AI Content Inspector extends content authenticity and fraud detection coverage through advanced AI technologies. The engine analyzes both textual and visual artifacts to deliver AI-generation and fraud-indicator verdicts, enabling organizations to make informed security decisions before content enters critical workflows.

## [Designed to Combat Modern Fraud](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#designed-to-combat-modern-fraud)

AI Content Inspector focuses on the primary entry points for content-based fraud across enterprise workflows. It supports a wide range of image formats, text-bearing documents, and PDF files where AI-driven deception and document fraud most commonly occur, including:

- Invoice and accounts payable fraud
- AI-generated business and financial documents
- AI-generated or manipulated home damage images and insurance claims
- Detection of AI-generated insurance claim evidence

## [Key Benefits](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#key-benefits)

### [Accelerated Content Review](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#accelerated-content-review)

- Faster review cycles for high-volume workflows such as claims processing and invoice verification
- Improved operational efficiency while reducing false positives

### [Intelligent Pre-Decision Analysis](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#intelligent-pre-decision-analysis)

- Rapid content inspection enables organizations to automatically allow, flag, block, or route content for further review at scale

### [Comprehensive Fraud Detection Coverage](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#comprehensive-fraud-detection-coverage)

Detects both AI-generated content and document fraud indicators across common enterprise fraud scenarios, including:

- AI-generated invoices and financial documents
- AI-generated vehicle and accident imagery fraud
- AI-generated home and property insurance fraud
- AI-generated synthetic claim documentation

### [Broad File Format Support](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#broad-file-format-support)

- Extensive support for image formats commonly used in fraud attempts
- Coverage for text-bearing documents and PDF files across enterprise workflows

## [Availability](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#availability)

AI Content Inspector 2.0.0 is available as a standalone engine within MetaDefender Core and MetaDefender Cloud, providing organizations with advanced AI-driven content authenticity verification and document fraud detection capabilities across their security ecosystem.
