<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport -->

# Introduction to Regulatory Compliance Reporting with GetComplianceReport

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Check Your Version

This article applies to MetaDefender Endpoint Security SDK 4.3.6404.0 and later on Windows, 4.3.5791.0 and later on macOS, and 4.3.5406.0 and later on Linux.

## [What is GetComplianceReport?](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#what-is-getcompliancereport)

`GetComplianceReport` (method `1035`) collects the device-state evidence needed to assess an endpoint against a compliance framework, and returns it in a single call. You name the framework, for example PCI DSS 4.0.1, and the SDK returns the evidence for each control in that framework: which security products are installed in each category, and the state of each product, such as real-time protection, firewall, encryption or missing patches.

Key points:

- **Evidence, not a verdict.** The SDK never returns pass or fail. Your application applies its own compliance logic, for example in your compliance dashboard.
- **One call.** No separate load or detect step is needed. The SDK runs the required detection and state calls internally.
- **Same on every platform.** Windows, macOS and Linux share the same input, output schema, controls and error codes. The values inside reflect each platform's own detection results.
- **Additive.** No existing method changes. Integrations that do not call method `1035` are unaffected.
- **No separate license.** The method is covered by your existing OESIS compliance license.
- **Data-driven.** Frameworks, framework versions and controls are defined in the SDK data package (`libwaresource`), so new frameworks that reuse existing controls can be added through a data package update, without an SDK upgrade.

## [Supported frameworks](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#supported-frameworks)

| `framework_id` | `framework_version` | Controls returned | Requirement IDs |
| --- | --- | --- | --- |
| `generic` | `1.0` | 12 | None. Framework-agnostic evidence. |
| `pci_dss` | `4.0.1` | 6 | PCI DSS 4.0.1 requirement IDs per control |

These are the only two combinations available as of November 2026. Both values are matched exactly and are case-sensitive: `PCI_DSS` or `4.0` is not accepted. New combinations will be announced in the OESIS Framework release notes, and this article will be updated.

Need a different framework?

If you need support for a framework or framework version that is not listed here, [open a support case](https://my.opswat.com/support) with the details of your request:

- the framework name and version (for example, the standard and the exact revision you report against),
- the controls or requirement IDs you need evidence for, if any,
- the platforms you need it on (Windows, macOS, Linux).
### [Controls per framework](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#controls-per-framework)

The response includes only the controls the SDK can collect evidence for, in the framework's order.

| Control ID | Description | `generic` 1.0 | `pci_dss` 4.0.1 | PCI DSS 4.0.1 requirement IDs |
| --- | --- | --- | --- | --- |
| `anti_malware` | Antimalware | Yes | Yes | 5.1, 5.2, 5.3 |
| `encryption_at_rest` | Encryption at rest | Yes | Yes | 3.5, 3.6 |
| `firewall` | Firewall | Yes | Yes | 1.4.2 |
| `vpn` | VPN (remote access) | Yes* | Yes* | 8.3.1, 8.4.2 |
| `dlp` | Data loss prevention | Yes* | Yes* | 4.2, 12.3.2 |
| `patch_management` | Patch management | Yes | Yes | 6.3.3 |
| `anti_phishing` | Anti-phishing | Yes | No |  |
| `vulnerability_management` | Vulnerability management | Yes | No |  |
| `remote_control` | Remote control | Yes | No |  |
| `public_file_sharing` | Public file sharing | Yes | No |  |
| `web_conference` | Web conference | Yes | No |  |
| `backup` | Backup | Yes | No |  |

* For `vpn` and `dlp`, the evidence is product detection only (`detect.detected_products`), without additional state calls.

## [How to use GetComplianceReport](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#how-to-use-getcompliancereport)

1. Initialize the SDK with `wa_api_setup`, as your integration already does.
2. Call `GetComplianceReport` through `wa_api_invoke` with `framework_id` and `framework_version` (see [Input](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#input)).
3. Read the `endpoint` context and the `controls[]` array from the response.
4. Apply your own compliance logic to the evidence, for example "an antimalware product is installed, real-time protection is on, and definitions are current".
5. Tear down the SDK with `wa_api_teardown` when your integration finishes.

### [Input](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#input)

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `method` | Integer | Yes | `1035` |
| `framework_id` | String | Yes | Framework to report on: `generic` or `pci_dss`. |
| `framework_version` | String | Yes | Version of that framework: `1.0` for `generic`, `4.0.1` for `pci_dss`. |

Both `framework_id` and `framework_version` are required in every mode, including `generic`.

**PCI DSS 4.0.1 report**

{
"input": {
"method": 1035,
"framework_id": "pci_dss",
"framework_version": "4.0.1"
}
}

**Generic report**

{
"input": {
"method": 1035,
"framework_id": "generic",
"framework_version": "1.0"
}
}
### [Response structure](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#response-structure)

A successful call returns code `0` and the following fields:

| Field | Description |
| --- | --- |
| `framework_id`, `framework_version` | The requested framework, echoed back. |
| `report_time` | Time the report was produced, in Unix epoch seconds (string). |
| `endpoint` | Device context, collected once: `get_os_info` (`GetOSInfo`, method `1`), `get_device_identity` (`GetDeviceIdentity`, method `4`) and `get_active_user_info` (`GetActiveUserInfo`, method `6`). Each holds that call's full result. |
| `controls[]` | One entry per control the framework returns (see the table above). |
| `controls[].id`, `controls[].description` | The control ID and its description. |
| `controls[].requirements` | The framework's requirement IDs for the control. Present for `pci_dss`, absent for `generic`. |
| `controls[].detect` | The `DetectProducts` (method `0`) result for the control's product category. `detect.detected_products` is empty when no matching product is installed. |
| `controls[].detect.detected_products[].methods` | An object keyed by call name that holds the result of each follow-up call made for that product, for example `get_version` (`GetVersion`), `get_rtp_state`, `get_def_state` and `get_last_scan_time` for antimalware, `get_firewall_state` (`GetFirewallState`), `get_encryption_state` (`GetEncryptionState`), `get_backup_state` (`GetBackupState`), `get_antiphishing_state` (`GetAntiphishingState`) and `get_missing_patches` (`GetMissingPatches`). |

A trimmed example for one control (values are illustrative):

{
"result": {
"code": 0,
"method": 1035,
"framework_id": "pci_dss",
"framework_version": "4.0.1",
"report_time": "1794880000",
"endpoint": {
"get_os_info": { "code": 0, "method": 1 },
"get_device_identity": { "code": 0, "method": 4 },
"get_active_user_info": { "code": 0, "method": 6 }
},
"controls": [
{
"id": "anti_malware",
"description": "Antimalware",
"requirements": ["5.1", "5.2", "5.3"],
"detect": {
"code": 0,
"method": 0,
"detected_products": [
{
"signature": "<signature id>",
"methods": {
"get_version": { "code": 0, "method": 100, "version": "<version>" },
"get_rtp_state": { "code": 0, "method": 1000, "enabled": true }
}
}
]
}
}
]
}
}
### [How failures inside a report are handled](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#how-failures-inside-a-report-are-handled)

- If a follow-up call fails for one product, for example `GetFirewallState`, that entry in `methods` holds the call's error code instead of a result. The rest of the report is still returned, with code `0`.
- If `DetectProducts` fails for a control, `detect` holds its error and has no `detected_products`.
- If the compliance data in the data package is missing or malformed, the whole call fails and no partial report is returned, because an inaccurate compliance report is worse than none.

## [Error codes](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#error-codes)

| Return code | Meaning |
| --- | --- |
| `WAAPI_OK` (`0`) | The report was generated. |
| `WAAPI_ERROR_INVALID_INPUT_ARGS` (`-20`) | `framework_id` or `framework_version` is missing, empty or of the wrong type, or `framework_id` is not recognized. |
| `WAAPI_ERROR_FRAMEWORK_VERSION_NOT_SUPPORTED` (`-1080`) | `framework_id` is recognized, but `framework_version` is not supported. |
| `WAAPI_ERROR_DATABASE_ENTRY_MISSING` (`-15`) | Required compliance data is not available in the data package. |
| `WAAPI_ERROR_DATABASE_CORRUPTED` (`-14`) | Required compliance data in the data package is malformed. |
| `WAAPI_ERROR_MALFORMED_EXPRESSION` (`-45`) | An internal inconsistency in the compliance data prevented evidence collection. This is a data package issue, not a request issue. |
| `WAAPI_ERROR_INVALID_OUTPUT_ARGS` (`-58`) | An underlying detection call returned a result the SDK did not expect. This is an internal issue, not a request issue. |
| `WAAPI_ERROR_GENERAL` (`-1`) | Unexpected failure. |

If you receive `-14`, `-15`, `-45` or `-58`, retrying is unlikely to help. Update to the latest data package, and if the error persists, open a support case with the `json_in`, `json_out` and SDK debug logs.

## [Related resources](/docs/mdsdk/knowledge-base/regulatory-compliance-reporting-getcompliancereport#related-resources)

- [OESIS V4 method reference](https://software.opswat.com/OESIS_V4/html/c_method.html) (`GetComplianceReport`, method `1035`)
- [OESIS Framework release notes](/docs/mdsdk/release-notes/release-notes)

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
