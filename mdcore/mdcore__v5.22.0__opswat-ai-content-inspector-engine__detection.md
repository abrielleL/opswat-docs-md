<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/opswat-ai-content-inspector-engine/detection -->

# Detection

OPSWAT AI Content Inspector applies a hybrid detection methodology across three specialized classifiers, each tuned to a distinct content-risk surface: AI-generated text, AI-generated images, and document fraud. Each classifier produces an independent verdict with a confidence score, and verdicts can be combined into a single policy decision, allow, flag, block, or route for review.

This page introduces the three detection types, the shared methodology that powers them, and how their verdicts surface inside MetaDefender workflows.

## [The three detection types](/docs/mdcore/v5.22.0/opswat-ai-content-inspector-engine/detection#the-three-detection-types)

| Detection type | What it identifies | Primary inputs |
| --- | --- | --- |
| AI-Generated Text Detection | Text passages produced or substantially rewritten by generative language models | .txt, .md, .markdown, text layers in .pdf |
| AI-Generated Image Detection | Images produced by diffusion, GAN, or other generative image models | All supported image formats (see [Supported file types](https://www.opswat.com/docs/mdcore/opswat-ai-content-inspector-engine/supported-file-types)) |
| Document Fraud Detection | Detection of forgery, tampering, and fabrication indicators in business documents using AI models, including fake invoices, insurance fraud, and others | .pdf, text-bearing documents, embedded images |

Each classifier ships with its own quality gates and false-positive benchmarks, so verdicts in one category never compromise the threshold integrity of another.

## [How verdicts are returned](/docs/mdcore/v5.22.0/opswat-ai-content-inspector-engine/detection#how-verdicts-are-returned)

Every scan returns a structured result per classifier:

- **Verdict** - one of `Not Detected`, `Uncertain`, `Detected`
- **Confidence score** - (0–100)
- **Contributing detectors and metrics** - All detected signals and detailed information related to their detection results
