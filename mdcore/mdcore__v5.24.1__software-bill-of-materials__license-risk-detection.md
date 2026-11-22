<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/software-bill-of-materials/license-risk-detection -->

# License risk detection

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Some open-source licenses include clauses — such as copyleft provisions — that can require you to open-source your own code. Verifying that your dependencies use licenses compatible with your business model is essential to protecting your intellectual property.

The SBOM engine includes license detection that examines each open-source component detected in a scan. Beyond identifying the license type, it reports detailed license information for your open-source dependencies, helping you assess compliance obligations before they become a risk.

To block licenses, go to Workflow > [workflow name] > SBOM and enable **Block Licenses**, then choose the licenses to block. A scan that finds a blocked license is blocked, and its verdict is **License Risk Found**, unless vulnerabilities are also found, in which case the verdict is **Vulnerabilities Found**.

Process result:

License information is reported for packages from Python (PyPI), JavaScript (npm), Java (Maven), .NET (NuGet), PHP (Packagist), Ruby (RubyGems), C/C++, and identified software applications. It is also reported for operating-system packages in container images, and for license data already present in scanned CycloneDX and SPDX reports. AIBOM uses its own license list (see AIBOM).
