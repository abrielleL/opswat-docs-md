<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-to-properly-check-if-windows-firewall-is-on- -->

# How to properly check if Windows Firewall is on?

This article applies to all MetaDefender Endpoint releases deployed on Windows systems.

**Overview**

Windows Firewall settings are determined by a combination of Group Policy (GPO) and Local Policy. The final applied settings result from a merge of these configurations, depending on the policies set in Group Policy.

**Understanding Firewall Policy Merging**

Windows Firewall has multiple configuration stores:

- Group Policy (GPO) – Managed by administrators via Active Directory.
- Local Policy – Configured directly on the machine.
- Active Policy – The merged result of both policies.

**Example Scenario**

- Group Policy: Firewall enabled for the domain profile.
- Local Policy: Firewall disabled for the domain profile.
- Final (Active) Policy: Firewall remains enabled, as Group Policy takes precedence.

**How to Verify the Active Firewall Policy**

Since different tools may show different policies, it's important to use the correct method for verification.

*1. Checking Local Policy Only (Limited View)*

The following command shows only the local store configuration, which may not reflect the merged policy:

PowershellCopypowershellnetsh advfirewall show allprofiles

Limitation: This does not display Group Policy settings, so the actual firewall status may differ.

*2. Checking the Merged (Active) Policy*

To see the effective firewall settings, including Group Policy, use:

PowershellCopyGet-NetFirewallProfile -PolicyStore ActiveStore

Best Practice: This command provides the most accurate representation of the applied firewall policy.

*3. Comparing Command Output with UI*

The Control Panel reflects the active policy (merged result). However, the Windows Firewall with Advanced Security (WFAS) snap-in may show only local settings when connected to the local machine.

*Recommendation:*

- Always verify the Control Panel firewall settings.
- Compare with Get-NetFirewallProfile -PolicyStore ActiveStore to confirm the actual firewall status.

*Conclusion*

- Windows Firewall settings result from a merge of Group Policy and local policy.
- Group Policy overrides local settings, so relying on local policy alone can be misleading.
- Use PowerShell (Get-NetFirewallProfile -PolicyStore ActiveStore) to check the actual applied policy.
- Always compare command output with UI settings for the most accurate firewall status.

Support

For any queries, concerns or issues regarding **Verifying** **Windows Firewall's Status** **From MetaDefender Endpoint**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
