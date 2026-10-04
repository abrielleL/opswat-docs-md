<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/what-operating-systems-does-oesis-support -->

# What Operating Systems Does OESIS Support?

### [Overview](/docs/mdsdk/knowledge-base/what-operating-systems-does-oesis-support#overview)

OESIS supports Windows, macOS, and Linux platforms. This article provides a comprehensive reference of all supported operating system versions, their compatible CPU architectures, and the availability of key OESIS modules — including device Posture (Detection), Vulnerability Assessment, Patch Management, and AppRemover.

### [Terminology](/docs/mdsdk/knowledge-base/what-operating-systems-does-oesis-support#terminology)

- **End-of-support (EOS):** A product lifecycle status indicating that OESIS will no longer provide maintenance updates, feature enhancements, or bug fixes for the affected OS version. Customers are strongly encouraged to upgrade to a supported platform to ensure continued security and stability.

### [OS Support Matrix](/docs/mdsdk/knowledge-base/what-operating-systems-does-oesis-support#os-support-matrix)

#### [Legend](/docs/mdsdk/knowledge-base/what-operating-systems-does-oesis-support#legend)

| Symbol | Description |
| --- | --- |
| ✅ | Support |
| 🚫 | Not Support |
| ⚠️ | Support, but in the EOL/EOS Plan or maintenance |

#### [Windows Matrix](/docs/mdsdk/knowledge-base/what-operating-systems-does-oesis-support#windows-matrix)

| OS | Arch | Device Posture | AppRemover | Vulnerability Assessment | Patch Management |
| --- | --- | --- | --- | --- | --- |
| Windows Server 2025 | x86, x86-64, ARM64 | ✅ | 🚫 | ✅ | ✅ |
| Windows Server 2022 | x86, x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| Windows 11 | x86, x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| Windows Server 2019 | x86, x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| Windows Server 2016 | x86, x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| Windows 10 | x86, x86-64, ARM64 | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) |
| Windows Server 2012 R2 | x86, x86-64, ARM64 | ✅ | ✅ | 🚫 | ✅ |
| Windows 8.1 | x86, x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| Windows Server 2012 | x86, x86-64, ARM64 | ✅ | ✅ | 🚫 | ✅ |
| Windows 8 | x86, x86-64, ARM64 | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) |
| Windows Server 2008 R2 | x86, x86-64, ARM64 | ✅ | ✅ | 🚫 | ✅ |
| Windows 7 | x86, x86-64, ARM64 | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) | ⚠️ (EOS at Jan 1, 2027) |
| Windows Server 2008 | x86, x86-64, ARM64 | 🚫 | 🚫 | 🚫 | 🚫 |
| Windows Vista | x86, x86-64, ARM64 | 🚫 | 🚫 | 🚫 | 🚫 |
| Windows Server 2003 R2 | x86, x86-64 | 🚫 | 🚫 | 🚫 | 🚫 |
| Windows Server 2003 | x86, x86-64 | 🚫 | 🚫 | 🚫 | 🚫 |
| Windows XP | x86, x86-64 | 🚫 | 🚫 | 🚫 | 🚫 |

#### [macOS Matrix](/docs/mdsdk/knowledge-base/what-operating-systems-does-oesis-support#macos-matrix)

| OS | Arch | Device Posture | AppRemover | Vulnerability Assessment | Patch Management |
| --- | --- | --- | --- | --- | --- |
| macOS Golden Gate | x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| macOS Tahoe | x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| macOS Sequoia | x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| macOS Sonoma | x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| macOS Ventura | x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| macOS Monterey | x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| macOS Big Sur | x86-64, ARM64 | ✅ | ✅ | ✅ | ✅ |
| macOS Catalina | x86-64 | ✅ | ✅ | ✅ | ✅ |
| macOS Mojave | x86-64 | ✅ | ✅ | ✅ | ⚠️ (Maintain only, no QA) |
| macOS High Sierra | x86-64 | ✅ | ✅ | ✅ | ⚠️ (Maintain only, no QA) |
| macOS Sierra | x86-64 | ⚠️ (Maintain only, no QA) | ✅ | 🚫 | ⚠️ (Maintain only, no QA) |
| macOS El Capitan | x86-64 | ⚠️ (Maintain only, no QA) | 🚫 | 🚫 | 🚫 |
| macOS Yosemite | x86-64 | ⚠️ (Maintain only, no QA) | 🚫 | 🚫 | 🚫 |

#### [Linux Matrix](/docs/mdsdk/knowledge-base/what-operating-systems-does-oesis-support#linux-matrix)

| OS | Arch | Device Posture | AppRemover | Vulnerability Assessment | Patch Management |
| --- | --- | --- | --- | --- | --- |
| Ubuntu | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (20.04, 22.04, 24.04, 25.04, 26.04) |
| Linux Mint | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (20, 21, 22) |
| Debian | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (11, 12, 13) |
| Red Hat Enterprise Linux | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (8, 9, 10) |
| Amazon Linux | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (2, 2023) |
| AlmaLinux | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (8, 9, 10) |
| Rocky Linux | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (8, 9, 10) |
| Oracle Linux | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (8, 9, 10) |
| Fedora | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (41, 44) |
| SUSE | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (15, 16) |
| CentOS | x86, x86-64 | ✅ | 🚫 | ✅ | ✅ (7, 8) |
