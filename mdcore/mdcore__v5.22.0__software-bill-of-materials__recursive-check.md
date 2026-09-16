<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/software-bill-of-materials/recursive-check -->

# Recursive check

SBOM scans (nested) dependencies used in open source libraries to detect known vulnerabilities from potentially harmful packages.

To enable recursive check: Workflow > Workflow name > SBOM > Enable dependency check for source code.

Example scan result

- Supported programming languages: Python, NodeJS, .Net, Ruby, Maven, PHP
- Supported recursive level: 1

Note: in the container, all dependencies are on the container image, the SBOM engine checks all of them without a configuration.
