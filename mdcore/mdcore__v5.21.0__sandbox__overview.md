<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/sandbox/overview -->

# Overview

As the sandbox product has undertaken a variety of product name changes ("OPSWAT Filescan", "OPSWAT Filescan Sandbox" and now "MetaDefender Sandbox", you may find artefacts in the product or slightly outdated screenshots in the documentation). Please note that "**MetaDefender Aether for Core**" and " **Adaptive Sandbox**" are terms both referring to the same product.

## [What is MetaDefender Aether for Core (Adaptive Sandbox)?](/docs/mdcore/v5.21.0/sandbox/overview#what-is-metadefender-aether-for-core-adaptive-sandbox)

The MetaDefender Aether for Core in MetaDefender Core is a next-gen sandbox and threat intelligence solution that utilizes Adaptive Threat Analysis (ATA) of the OPSWAT Filescan platform. It binds together dozens of state-of-the-art tools, services, and proprietary algorithms with the focus on zero-day malware detection and Indicators of Compromise (IOCs) extraction from files, documents, scripts at speed and scale. Using a technology called Adaptive Threat Analysis (ATA), OPSWAT Sandbox is a solution that is able to provide actionable intelligence in many more cases. Combined with its unmatched speed, it becomes possible to significantly reduce the number of artefacts needing a manual analysis.

For information of the standalone Filescan product, visit [our product documentation site](https://docs.opswat.com/filescan/datasheet).

## [Sandbox Engines in MetaDefender Core](/docs/mdcore/v5.21.0/sandbox/overview#sandbox-engines-in-metadefender-core)

For using Filescan functionality through MD Core, there is 2 types of engines to choose from:

- **Embedded** - this contains a bundled Adaptive Threat Analysis (ATA) engine, and is an optimal choice for off-line environments
- **Remote** - this utilizes a deployed standalone instance of an [MetaDefender Sandbox](https://docs.opswat.com/filescan) platform instance via the API (on premise or in the cloud). This is the recommended engine for most cases.

Info

A MetaDefender Core license can contain only one version of the Sandbox Engine.

The following diagram illustrates the different engine setups:

More details on the exact feature sets can be found [here](https://docs.opswat.com/filescan/integrations/md-core-engine).

## [Example Sandbox Engine results](/docs/mdcore/v5.21.0/sandbox/overview#example-sandbox-engine-results)

### [Verdict and Threat Indicators](/docs/mdcore/v5.21.0/sandbox/overview#verdict-and-threat-indicators)

### [YARA matches and detected IOCs](/docs/mdcore/v5.21.0/sandbox/overview#yara-matches-and-detected-iocs)

### [Executive Summary](/docs/mdcore/v5.21.0/sandbox/overview#executive-summary)

Info

Only available for the Embedded Sandbox Engine
