<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework -->

# Windows 10 ESU Support in OESIS Framework

### [Overview](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#overview)

On October 14, 2025, Windows 10 reaches the end of support. After this date, devices without Extended Security Updates (ESU) enrollment will no longer receive security patches from Microsoft, creating critical vulnerabilities for organizations maintaining Windows 10 infrastructure.

OESIS Framework introduces comprehensive support for the Windows 10 ESU program to help organizations manage this transition. This support enables visibility into device ESU enrollment status and seamless patch management for ESU security updates.

#### [Two Components of ESU Support](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#two-components-of-esu-support)

1. ESU Status Detection

- The new `esu_status` field in the GetOSInfo method provides real-time visibility into device enrollment
- Enables compliance monitoring and policy enforcement based on ESU enrollment state
- Helps identify at-risk devices that won't receive security updates post-EOL

2. ESU Patch Management

- Automatic detection and installation of ESU security updates through existing OESIS workflows
- No code changes or policy modifications required
- ESU updates are treated identically to standard Windows security updates

### [What is Windows 10 ESU?](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#what-is-windows-10-esu)

Windows 10 ESU is a paid program from Microsoft that delivers security updates beyond the operating system's end of support. Organizations with eligible devices and active ESU subscriptions continue receiving monthly security updates.

**Important:** OESIS SDK detects and reports ESU enrollment status but does not manage ESU license procurement or activation. Licenses must be purchased and activated through Microsoft Volume Licensing.

### [ESU Status Detection](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#esu-status-detection)

Info

This function is supported from SDK version 4.3.5364 or later.

#### [A New Parameter](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#a-new-parameter)

A new optional field, `esu_status`, is introduced in the GetOSInfo response under `result.details`. It indicates whether the endpoint is enrolled in the Windows 10 ESU program.

- Location: `result.details.esu_status`
- Type: string (optional)
- Possible values: `enrolled` | `not_enrolled` | `unknown`
- Omission: If no clues regarding ESU enrollment can be found on the machine, the field is omitted.

#### [Interpretation Guide](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#interpretation-guide)

- `enrolled` — The device is enrolled in ESU (license detected).
- `not_enrolled` — The device is not enrolled in ESU.
- `unknown` — The SDK could not reliably determine ESU status due to detection limitations or transient errors.

#### [ESU Status Detection Behavior by Scenario](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#esu-status-detection-behavior-by-scenario)

| Scenario | Expected ESU status | Notes |
| --- | --- | --- |
| Windows 10 22H2 + KB5046613 or later + Active ESU license | `enrolled` | Device will receive ESU security updates |
| Windows 10 22H2 without ESU license (or prerequisites not met) | `not_enrolled` (or field omitted if no clues) | Device will not receive ESU updates post-EOL |
| Detection impeded (e.g., WMI or script issues) | `unknown` | Retry detection recommended |

### [Patch Management Support](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#patch-management-support)

OESIS Patch Management continues to support ESU security updates the same way as other Windows security updates. Customers do not need to change any code or policies to receive or apply ESU patches, assuming prerequisites are met.

#### [Prerequisites](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#prerequisites)

- Operating System: Windows 10, version 22H2
- Updates: KB5046613 (or later cumulative update) installed
- Licensing: Active Windows 10 ESU subscription on the endpoint

#### [Supported Methods](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#supported-methods)

- GetMissingPatches
- InstallMissingPatches
- GetLatestInstaller
- InstallFromFiles

#### [Key Behavior](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#key-behavior)

ESU security updates flow through the same detection, compliance, and installation pipelines as non-ESU Windows security updates. No special category or severity reconfiguration is required.

**Important:** If prerequisites are not met, Windows Update Agent (WUA) will not offer ESU patches to the device; consequently, Patch Management will not list or install them.

#### [Patch Management Behavior by Scenario](/docs/mdsdk/knowledge-base/windows-10-esu-support-in-oesis-framework#patch-management-behavior-by-scenario)

| Scenario | Behavior |
| --- | --- |
| Windows 10 22H2 + KB5046613 or later + Active ESU license | ESU security updates are included in patching flows |
| Windows 10 22H2 without ESU license (or prerequisites not met) | ESU updates are not offered; device may appear non-compliant if policy demands the latest security updates |
