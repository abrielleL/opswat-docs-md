<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/sandbox/system-requirements -->

# System requirements

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Dependencies](/docs/mdcore/v5.22.1/sandbox/system-requirements#dependencies)

| Embedded Engine | Remote Engine |
| --- | --- |
| See: [How to upgrade to Java 17](/docs/mdcore/v5.22.1/sandbox/upgrade-to-java-17)  **Linux:** openjdk-17-jre  **Windows:** [Amazon Corretto 17](https://corretto.aws/downloads/latest/amazon-corretto-17-x64-windows-jdk.msi) | No additional dependencies are required. |

Note

Before version 2.2.0 [Visual C++ Redistributable for Visual Studio](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) is required for Windows.

Warning

**The required Java version for the embedded Aether(adaptive sandbox) is Java 17. While Java 8 or 11 may still function temporarily, they will no longer work at all after March 2025. Please plan to upgrade to Java 17 before March 2025 to avoid any disruption**

The default system Java version should be set correctly; please check if the correct version is used. The computer should be restarted after Java installation.

Check Java versionCopyjava -version
openjdk version "17.0.12" 2024-07-16
OpenJDK Runtime Environment (build 17.0.12+7-Ubuntu-1ubuntu222.04)
OpenJDK 64-Bit Server VM (build 17.0.12+7-Ubuntu-1ubuntu222.04, mixed mode, sharing)
## [System requirements](/docs/mdcore/v5.22.1/sandbox/system-requirements#system-requirements)

### [Embedded Sandbox Engine](/docs/mdcore/v5.22.1/sandbox/system-requirements#embedded-sandbox-engine)

System requirements depend on the number and type of submitted files, as well as their content and size. The performance also varies based on the configuration of the system and engine workflow. Below, you will find benchmark measurements using different CPU, RAM, and Sandbox parallel processing configurations on various sample sets. These measurements serve as a guideline to help estimate the required resources for your use case.

Warning

These are additional requirements on top of the [MetaDefender Core recommended system configuration](https://docs.opswat.com/mdcore/installation/recommended-system-configuration)

Note

These measurements are done with default engine workflow settings on Ubuntu Linux

#### [Example Configurations](/docs/mdcore/v5.22.1/sandbox/system-requirements#example-configurations)

|  | CPU Cores | RAM | Parallel Count |
| --- | --- | --- | --- |
| **Config #1** | 4 | 8 | 5 (default) |
| **Config #2** | 8 | 16 | 10 |

#### [Measured daily throughput](/docs/mdcore/v5.22.1/sandbox/system-requirements#measured-daily-throughput)

Warning

Throughput can be limited by license restrictions! See [Licensing](/docs/mdcore/v5.22.1/sandbox/licensing)

| File type | Avg size (MB) | Throughput #1 | Throughput #2 | #1 (MB/s) | #2 (MB/s) |
| --- | --- | --- | --- | --- | --- |
| Adobe | 0.93 | 47856 | 90816 | 0.52 | 0.98 |
| Executable | 0.16 | 50424 | 101040 | 0.09 | 0.19 |
| Image | 1.6 | 121728 | 218328 | 2.25 | 4.04 |
| Media | 0.13 | 73776 | 148176 | 0.11 | 0.22 |
| Office | 1.6 | 42744 | 54720 | 0.79 | 1.01 |
| Text | 8.8 | 71520 | 97344 | 7.28 | 9.91 |

### [Remote Aether (Adaptive Sandbox) Engine](/docs/mdcore/v5.22.1/sandbox/system-requirements#remote-aether-adaptive-sandbox-engine)

For MetaDefender Aether (Standalone) system requirements please refer to our [Technical Datasheet](https://www.opswat.com/docs/filescan/datasheet/technical-datasheet) and [Performance Measurement](https://www.opswat.com/docs/filescan/datasheet/performance-measurement) page.
