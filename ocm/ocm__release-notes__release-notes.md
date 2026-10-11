<!-- source: https://www.opswat.com/docs/ocm/release-notes/release-notes -->

# Release Notes

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

OPSWAT Central Management v.7 and My OPSWAT On-Premises (My OPSWAT Central Management v.8) will reach End of Life on January 31, 2027. We encourage you to upgrade to My OPSWAT Central Management v.10 before January 31, 2027, to ensure continued support and access to the latest features.

More details can be found [here](/docs/ocm/knowledgebase/end-of-sale-and-end-of-life-cm7-and-cm8).

| 7.40.0 OPSWAT Central Management release June 24, 2026 | OPSWAT Central Management V7 (OCMv7), the newest version of the series, streamlines the product central configuration and adds OPSWAT Client management to further enhance the security stance of organizations to protect against risky devices. |
| --- | --- |
| **Built-in MetaDefender Endpoint version** |  |
| Windows Persistent Endpoint 7.6.2606.1009 | Detailed release notes for MetaDefender Endpoint are [here](https://www.opswat.com/docs/mdendpoint/release-notes)[.](https://www.opswat.com/docs/mdendpoint/v2503/release-notes/metadefender-endpoint-release-notes) |
| Windows On-demand Endpoint 7.3.2606.479 |  |
| macOS Persistent Endpoint 10.4.2606.225 |  |
| macOS On-demand Endpoint 10.5.2606.177 |  |
| **Enhancement** |  |
| Processing history | Enhance internal communication to decrease history sync-up time. Data retention is now fixed to 30 days and configurable via properties file |
| **Security Updates** |  |
| Apache Log4j | Upgraded Apache Log4j to version 2.25.4 to address CVE-2026-34477 (TLS hostname verification bypass), CVE-2026-34478 (Syslog log injection), and CVE-2026-34480 (XmlLayout invalid XML output |
| Apache MINA | Upgraded Apache MINA from 2.1.10 to 2.1.12 to address CVE-2026-41409, CVE-2026-41635, CVE-2026-42778, and CVE-2026-42779 — multiple deserialization RCE vulnerabilities allowing unsafe class resolution and arbitrary code execution |
| mchange-commons-java | Excluded vulnerable c3p0 and mchange-commons-java 0.2.15 from quartz mem-scheduler to address CVE-2026-27727 (CVSS 9.8) — a JNDI-based remote code execution vulnerability that bypasses JDK hardening |
| nginx | Upgraded nginx to address CVE-2026-42945 |
| Apache Commons FileUpload | Upgraded commons-fileupload from 1.5 to 1.6 to address CVE-2025-48976 |
