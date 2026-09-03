<!-- source: https://www.opswat.com/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes -->

# OPSWAT AI Content Inspector release notes

## [V 2.2.0](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-220)

Release date: 8/10/2026

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

Release date: 8/10/2026

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

Release date: 7/13/2026

Release type: MAJOR

- Introduce Fast mode and Forensic mode

  - Fast mode: Optimized for high-speed analysis with a fast response
  - Forensic mode: Optimized for deep analysis and investigative workflows
- Added an option to disable output image generation
- Improved PDF extraction performance
- Improved scan performance with faster processing times

## [V 2.0.1](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-201)

Release date: 5/28/2026

Release type: MINOR

- Upgraded the core image and text detection components for improved accuracy and performance
- Resolved issues affecting text scanning functionality
- Enhanced support for offline and packaged deployments

## [V 2.0.0](/docs/mdcore/release-notes/opswat-ai-content-inspector-release-notes#v-200)

Release date: 5/21/2026

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
