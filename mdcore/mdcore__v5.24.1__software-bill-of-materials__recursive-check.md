<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/software-bill-of-materials/recursive-check -->

# Recursive check

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

SBOM scans (nested) dependencies used in open source libraries to detect known vulnerabilities from potentially harmful packages.

To enable recursive check: Workflow > Workflow name > SBOM > Enable dependency check for source code.

> Two sub-options refine the check (both off by default):
>
> - **Return all dependency packages**: list every dependency package found, not only the vulnerable ones.
> - **Block if dependencies have vulnerabilities**: vulnerabilities in dependencies raise the file's severity and can block it, and vulnerable dependencies are counted in `vulnerable_package_count`. When off, dependency vulnerabilities are still listed but do not block the file.

Example scan result

- Supported ecosystems: Python (PyPI), Node.js (npm, including TypeScript and CoffeeScript projects), Java and other Maven/Gradle languages, .NET (NuGet), Ruby, PHP. Dependency data is not available for C/C++, Go, Rust, Dart, Elixir, Swift, Julia or R.
- Dependency depth: 1. The engine lists the direct dependencies of each detected package. It does not follow them further.

Note: dependency check applies to source code only. For container images, the engine reports the operating-system packages installed in the image, not application packages.
