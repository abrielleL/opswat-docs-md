<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/opswat-ai-content-inspector-engine/ai-generated-image-detection -->

# AI-Generated Image Detection

**AI-Generated Image Detection** identifies images produced by diffusion models, GANs, and other generative image systems. The classifier combines metadata inspection, perceptual fingerprinting, and multimodal vision classifiers to evaluate whether an image originated from a generative model, was substantially manipulated, or is an authentic capture.

This classifier targets the highest-value image-fraud entry points in enterprise workflows fabricated accident photos in auto insurance claims, synthetic damage evidence in home insurance, and etc.

## [Image detectors](/docs/mdcore/v5.22.0/opswat-ai-content-inspector-engine/ai-generated-image-detection#image-detectors)

This section explains how each detector analyzes image content to distinguish AI-generated or manipulated images from authentic camera-captured photos. The detectors evaluate a range of visual, statistical, and metadata-based signals within the image to identify patterns commonly associated with synthetic or edited media, helping organizations assess the authenticity and integrity of visual data.

### [How to Configuration](/docs/mdcore/v5.22.0/opswat-ai-content-inspector-engine/ai-generated-image-detection#how-to-configuration)

Policies > Workflow rules > "Workflow name" > OPSWAT AI Content Inspector > Advanced Options

- **Detect Image:** When enabled, the uploaded image is scanned for metadata indicators associated with AI-generated or edited media. This includes checking for software tags, missing camera information, provenance data, and other file-level signals that may suggest synthetic content. *Only metadata-based analysis is performed when this option is enabled by itself.

- **Enable AI Model:** When enabled, the image is analyzed using the full AI detection pipeline, including forensic analysis, machine learning models, metadata inspection, and visual artifact detection. This option performs a comprehensive scan using all available detectors and AI models to provide a higher-confidence authenticity assessment.
