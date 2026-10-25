<!-- source: https://www.opswat.com/docs/mdcore/opswat-ai-content-inspector-engine/ai-generated-image-detection -->

# AI-Generated Image Detection

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**AI-Generated Image Detection** identifies images created or edited by generative AI, including current diffusion, flow-matching and autoregressive image models. It combines deep-learning pixel analysis with verification of C2PA Content Credentials and metadata inspection, and returns a verdict, an AI probability and the contributing detectors.

It targets image-fraud entry points in enterprise workflows: fabricated accident photos in auto insurance claims, synthetic damage evidence in home insurance, and AI-generated images in onboarding and e-mail.

## [Image detectors](/docs/mdcore/opswat-ai-content-inspector-engine/ai-generated-image-detection#image-detectors)

This section explains how each detector analyzes image content to distinguish AI-generated or manipulated images from authentic camera-captured photos. The detectors evaluate a range of visual, statistical, and metadata-based signals within the image to identify patterns commonly associated with synthetic or edited media, helping organizations assess the authenticity and integrity of visual data.

### [How to Configure](/docs/mdcore/opswat-ai-content-inspector-engine/ai-generated-image-detection#how-to-configure)

Policies > Workflow rules > "Workflow name" > OPSWAT AI Content Inspector > Advanced Options

- **Detect Image:** When enabled, the uploaded image is scanned for metadata indicators associated with AI-generated or edited media. This includes checking for software tags, missing camera information, provenance data, and other file-level signals that may suggest synthetic content. (Only metadata-based analysis is performed when this option is enabled by itself.)

- **Enable AI Model:** When enabled, the image is analyzed using the full AI-detection pipeline, including forensic analysis, machine learning models, metadata inspection, and visual artifact detection. This option performs a comprehensive scan using all available detectors and AI models to provide a higher-confidence authenticity assessment.
