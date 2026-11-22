<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/software-bill-of-materials/overview -->

# Software Bill of Materials (SBOM)

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

OPSWAT SBOM analyzes third-party packages in source code, package archives and binaries, and container images. It generates an inventory of the components and identifies known vulnerabilities and license risks. It can also export the result as a CycloneDX or SPDX report. On MetaDefender Core 5.23 or later, the same scan can also produce a CBOM and an AIBOM.

To configure the engine, go to Workflow > [workflow name] > SBOM. Settings are grouped into Input and Output, SBOM Module, CBOM Module and AIBOM Module. Some options are shown only when the feature is licensed or the MetaDefender Core version supports it.

The engine also produces a CBOM (CBOM Module) and an AIBOM (AIBOM Module), both enabled by default on Core 5.23+. Packages are also identified in binaries (binary mode), and reports can be exported as JSON or PDF.

Support:

- Source code
- Container
- CycloneDX and SPDX reports from external tools.
