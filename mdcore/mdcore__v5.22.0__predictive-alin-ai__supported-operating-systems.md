<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/predictive-alin-ai/supported-operating-systems -->

# Supported Operating Systems

## [Windows](/docs/mdcore/v5.22.0/predictive-alin-ai/supported-operating-systems#windows)

**Predictive Alin AI** supports **64-bit** Windows only.

### [Supported versions](/docs/mdcore/v5.22.0/predictive-alin-ai/supported-operating-systems#supported-versions)

- **Windows 11** (23H2) and **Windows 11 IoT** (22H2) - **end-user systems only**
- **Windows Server** 2019, 2022, 2025

Windows 11 usage note

Based on the [Microsoft License Terms](https://www.microsoft.com/en-us/useterms), Windows desktop editions are not licensed for server use. As a result, Predictive Alin AI should not be deployed on Windows 11 for server use cases.

## [Linux](/docs/mdcore/v5.22.0/predictive-alin-ai/supported-operating-systems#linux)

**Predictive Alin AI** supports **64-bit** Linux only.

### [Supported versions](/docs/mdcore/v5.22.0/predictive-alin-ai/supported-operating-systems#supported-versions)

- Red Hat Enterprise Linux 8, 9
- Rocky Linux 9
- Oracle Linux 9 (9.5 or later)
- Debian 11, 12
- Ubuntu 22.04, 24.04
- Amazon Linux 2023 (supported via Amazon Machine Image (AMI))

Kernel requirement for RHEL and Rocky

Predictive Alin AI may not function correctly on Red Hat Enterprise Linux or Rocky Linux systems running older kernels (for example, 372.9 or 372.13).

Upgrade to **kernel 372.26 or later** to help ensure proper functionality.

### [Hardware dependencies](/docs/mdcore/v5.22.0/predictive-alin-ai/supported-operating-systems#hardware-dependencies)

- CPU that supports AVX2 (BMI2) instruction set
