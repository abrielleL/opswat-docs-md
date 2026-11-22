<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/software-bill-of-materials/analyze-cyclonedx-spdx-report-file -->

# Analyze CycloneDX/SPDX report file

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

In the SBOM ecosystem, CycloneDX is commonly associated with vulnerability tracking, while SPDX has historically focused on software license information. The SBOM engine can scan reports in either format and enrich them with any missing data, such as CVE details, license information, and library metadata. The result is a fully enriched SBOM that combines security and compliance insights for more accurate analysis and reporting.

Supported format:

- CycloneDX JSON 1.4, 1.5, 1.6, 1.7. CycloneDX 1.6+ reports also feed CBOM, and 1.5+ reports also feed AIBOM.
- SPDX JSON v2.3, v3.0.1. On MetaDefender Core 5.23 or later, a CycloneDX 1.6 or 1.7 report also feeds the CBOM, and a CycloneDX 1.5–1.7 report also feeds the AIBOM. SPDX reports feed the SBOM only. A report in an unsupported version, or one that fails schema validation, returns no data; to block such files instead, enable **Block on Invalid Input Report**.

## [CycloneDX CBOM documents](/docs/mdcore/v5.24.1/software-bill-of-materials/analyze-cyclonedx-spdx-report-file#cyclonedx-cbom-documents)

The SBOM engine also reads CycloneDX documents that describe cryptography (a Cryptographic Bill of Materials, supported in CycloneDX v1.6 and later). Their cryptographic assets are added to the CBOM results and graded for classical and quantum risk in the same way as a file the engine analyzes directly. See [CBOM – Cryptographic Bill of Materials](cbom).

- **References are normalized.** References between components, such as a certificate's signature algorithm or a key's algorithm, are resolved to the target component's `uid` rather than the source document's `bom-ref`, so you never need to understand the producing tool's scheme.
- **Dangling references stay visible.** A reference that cannot be resolved is replaced with a placeholder of the form `crypto/unresolved/@sha256:<hash>` instead of being dropped.
- **Invalid documents are flagged.** A CycloneDX CBOM document that fails validation returns the CBOM verdict `Verification Failed`.

For the result fields, see [CBOM JSON response](cbom-json-response).
