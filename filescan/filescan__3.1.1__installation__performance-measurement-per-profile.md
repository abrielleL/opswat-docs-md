<!-- source: https://www.opswat.com/docs/filescan/3.1.1/installation/performance-measurement-per-profile -->

# Performance Measurement Per Profile

This page provides an in-depth overview of the Standalone Throughput feature, including configuration settings and performance profiling for a one-hour duration. The goal is to help users optimize system throughput by understanding key configuration parameters and how different profiles impact performance over time. Whether you are troubleshooting or tuning your system, this guide offers valuable insights to maximize efficiency and streamline operations.

## [Configuration](/docs/filescan/3.1.1/installation/performance-measurement-per-profile#configuration)

|  | CPU | RAM | Parallel Count |
| --- | --- | --- | --- |
| **Config 1** | 8 | 32 | 5 |
| **Config 2** | 16 | 64 | 10 |

## [Throughput Results: Profiles / Filetype](/docs/filescan/3.1.1/installation/performance-measurement-per-profile#throughput-results-profiles--filetype)

This section presents throughput results for different profiles and file types, helping users understand how each configuration affects performance. It's key for optimizing system settings based on specific data handling needs.

| Version | Sample type | Config | Speed profile | Analysis profile |
| --- | --- | --- | --- | --- |
| v2.2.0 Standalone | Mixed | Config 1 | 1525 | 637 |
| v2.2.0 Standalone | Mixed | Config 2 | 2143 | 997 |
| v2.2.0 Standalone | Executable | Config 1 | 2700 | 904 |
| v2.2.0 Standalone | Executable | Config 2 | 4065 | 2036 |
| v2.2.0 Standalone | Media | Config 1 | 1853 | 1857 |
| v2.2.0 Standalone | Media | Config 2 | 3816 | 3779 |
| v2.2.0 Standalone | Offices | Config 1 | 634 | 446 |
| v2.2.0 Standalone | Offices | Config 2 | 1189 | 773 |
| v2.2.0 Standalone | Text | Config 1 | 986 | 538 |
| v2.2.0 Standalone | Text | Config 2 | 1569 | 633 |
| v2.2.0 Standalone | Images | Config 1 | 1922 | 1902 |
| v2.2.0 Standalone | Images | Config 2 | 4658 | 4544 |
| v2.2.0 Standalone | Adobe | Config 1 | 1124 | 509 |
| v2.2.0 Standalone | Adobe | Config 2 | 2541 | 1053 |

## [Throughput Results: Profiles / Active content](/docs/filescan/3.1.1/installation/performance-measurement-per-profile#throughput-results-profiles--active-content)

This section compares throughput results between scanning samples with active content and without active content, highlighting the impact of chosen profile on performance. It helps users optimize system settings based on profile activity.

| Version | Sample Type | Config | Speed profile | Analysis profile |
| --- | --- | --- | --- | --- |
| **v2.2.0-Standalone** | Active content | Config 1 | 664 | 351 |
| **v2.2.0-Standalone** | Active content | Config 2 | 1353 | 641 |
| **v2.2.0-Standalone** | Not active content | Config 1 | 1004 | 988 |
| **v2.2.0-Standalone** | Not active content | Config 2 | 1769 | 1725 |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
