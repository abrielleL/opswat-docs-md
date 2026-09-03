<!-- source: https://www.opswat.com/docs/mdcore/opswat-ai-content-inspector-engine/ai-generated-text-detection -->

# AI-Generated Text Detection

**AI-Generated Text Detection** identifies text passages produced or substantially rewritten by generative language models. The classifier evaluates stylometric features, statistical token patterns, and structural cues that distinguish model-generated prose from human-written content, then returns a verdict with a confidence score and the contributing signals.

This classifier is designed for high-volume text intake pipelines where authenticity matters incoming applications, support submissions, contract reviews, and any workflow where AI-generated content must be flagged, attributed, or routed for human review.

## [Text detectors](/docs/mdcore/opswat-ai-content-inspector-engine/ai-generated-text-detection#text-detectors)

This section explains how each detector analyzes written content to distinguish AI-generated text from human written text. The detectors evaluate various linguistic, structural, and contextual patterns within the content to identify indicators commonly associated with AI generated writing while helping organizations assess the authenticity of textual data.

### [How to Configuration](/docs/mdcore/opswat-ai-content-inspector-engine/ai-generated-text-detection#how-to-configuration)

Policies > Workflow rules > "Workflow name" > OPSWAT AI Content Inspector > Advanced Options

- **Detect text:** When enabled, the text is analyzed using the full AI detection pipeline, including forensic analysis, linguistic pattern evaluation, contextual analysis, and machine learning models designed to identify indicators commonly associated with AI-generated content.
