<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/software-bill-of-materials/container-image -->

# Container image

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Upload the .tar file written by docker save as is. Do not compress it. The engine also accepts a single-layer tar containing layer.tar, manifest.json and sbom_metadata.json. Only operating-system packages are reported. Application packages inside the image (npm, PyPI, Maven, …) are not scanned; to cover them, scan the application's source code or lockfile.

Supported OS package sources:

- Alpine Linux
- Red Hat Enterprise Linux
- CentOS
- Rocky Linux
- Oracle Linux
- Ubuntu
- Debian
- SUSE Linux Enterprise / openSUSE
- Amazon Linux
- AlmaLinux
- Fedora
