<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/behavior-of-getdefinitionstate-api-for-cortex-xdr -->

# Behavior of the GetDefinitionState API for Cortex XDR

This article is applied to OESIS Framework from version **4.3.4970.0** and later releases deployed on Windows systems.

## [Overview](/docs/mdsdk/knowledge-base/behavior-of-getdefinitionstate-api-for-cortex-xdr#overview)

Starting from **OESIS** version **4.3.4970.0**, the behavior of **GetDefinitionState** method for **Cortex XDR** has changed. The method now relies on Cortex’s officially supported method (`cytool`) to retrieve agent state, ensuring alignment with vendor‑recommended practices and more predictable results across environments.

Key changes at a glance

- **Impact:** Required **admin permission** for Cortex XDR GetDefinitionState
- **Platform:** Windows
- **Behavior update:**

  - Before: used EDR logic by checking Cortex service state and internet connection.
  - Latest: used official Cortex `cytool` command.
## [What changed in last_update](/docs/mdsdk/knowledge-base/behavior-of-getdefinitionstate-api-for-cortex-xdr#what-changed-in-last_update)

Previously, many users interpreted the `last_update` field as the “Last Content Update” time for malware definitions.

However, Cortex XDR does not provide an official API for that exact timestamp. Beginning with the change above, `last_update` now reflects the agent’s “Last Check‑in” time returned by the vendor‑supported flow.

## [Rationale for the Change](/docs/mdsdk/knowledge-base/behavior-of-getdefinitionstate-api-for-cortex-xdr#rationale-for-the-change)

- **No Official API for Content Update Time:** Cortex XDR does not expose a dedicated API to fetch the exact "Last Content Update" timestamp.
- **Vendor Recommendation:** Cortex XDR’s vendor recommended that the agent's check-in process synchronizes configuration and content/definition information. While the check-in time is not the precise moment of a content update, a successful check-in ensures the agent is up to date if new definitions are required. The Reference link can be found at: [Palo Alto Networks documentation portal](https://docs-cortex.paloaltonetworks.com/r/Cortex-XDR/8.2/Cortex-XDR-Agent-Administrator-Guide/Install-the-Cortex-XDR-Agent-with-Installer-and-Content-Update-Package)

- **Fallback to Last Check-in:** Given these constraints, the "Last Check-in" time is the most reliable indicator available for when the agent last synchronized its definitions.

## [Known Issues and Limitations](/docs/mdsdk/knowledge-base/behavior-of-getdefinitionstate-api-for-cortex-xdr#known-issues-and-limitations)

- **User Confusion - Last Update vs. Last Content Update** Some user have reported discrepancies between the `last_update` value and the **"Last Content Update"** time shown in the **Cortex Console**. This is expected, as there is no official API to retrieve the "Last Content Update" time. Please note that these two values may not always match due to system limitations.
- **Administrative Rights** In some cases, retrieving the **last check-in time** may require **administrative privileges**. We recommend ensuring that the necessary permissions are granted when using the **GetDefinitionState** method.
- **Edge Cases** If the agent is unable to check in (e.g., due to network issues or disabled updates), or if the agent successfully checks in but fails to update the content, `last_update` field may not accurately reflect the true state of the definitions.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
