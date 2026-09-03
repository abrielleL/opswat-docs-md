<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/can-i-use-active-directory-to-distribute--enforce-or-audit-opswa -->

# Can I use Active Directory to distribute, enforce or audit MetaDefender Endpoint usage?

This article applies to all persistent MetaDefender Endpoint releases deployed on Windows systems.

Yes, you can. Microsoft Active Directory is a powerful directory service that can be used to distribute, enforce and audit MetaDefender Endpoint usage on managed endpoint PCs.

### [Distribution through one-time, Automatic Installation](/docs/macloud-sdp/kb/can-i-use-active-directory-to-distribute--enforce-or-audit-opswa#distribution-through-one-time-automatic-installation)

Because it is packaged as a Microsoft Software Installer (or MSI), the persistent MetaDefender Endpoint facilitates streamlined distribution to all managed endpoints.

A simple, one-time installation can be performed by hosting your MetaDefender Endpoint installer in a central location, and then referencing it as a parameter to **MSIEXEC**.

For example, the following line would execute a silent installation of an MetaDefender Endpoint installer, hosted on a shared network drive that is mounted as drive Z:

PowershellCopyZ: MSIEXEC /a "Z:\Shared\Public\OPSWAT_GEARS_Client_3445-2e5e65e6b68ce141d-0.msi" /qn
### [Enforcement through Software Assignment](/docs/macloud-sdp/kb/can-i-use-active-directory-to-distribute--enforce-or-audit-opswa#enforcement-through-software-assignment)

Active Directory can not only be used to distribute and install the software, as mentioned above, but also to enforce that it remains installed.

In Active Directory terms, this is known as ‘assigning software.’

You have the option to assign software to authenticated users or machines. Both are viable options, and you should choose the one that aligns with your other corporate software installations and infrastructure.

To learn more, read the official Microsoft guide, found [Here](https://docs.microsoft.com/en-US/troubleshoot/windows-server/group-policy/use-group-policy-to-install-software).

### [Auditing through Policy creation](/docs/macloud-sdp/kb/can-i-use-active-directory-to-distribute--enforce-or-audit-opswa#auditing-through-policy-creation)

Please Note:

MetaDefender IT Access facilitates a streamlined way to audit MetaDefender Endpoint on your network, with the OPSWAT domain controller Client. To learn more, [Read This](/docs/macloud-sdp/kb/how-can-i-synchronize-devices-from-active-directory-to-my-metaac).

Besides that, Active Directory also facilitates auditing by giving administrators the option to create audit policies.

These can be used to record events such as processes being created and/or terminated on your managed devices.

When combined with event log forwarding, this tool is highly effective in providing a centralized view of all process changes across your organizational network.

The downside is that filtering for a specific process (e.g, GearsAgentService.exe) is not natively supported by Active Directory.

Pro Tip:

We highly recommend that users upgrade to the latest release of the persistent MetaDefender Endpoint for Windows.

Current versions incorporate state-of-the-art features and necessary bug fixes and are freely available for all license holders to download.

For details on the latest releases, [Read This](/docs/macloud-sdp/release-notes/opswat-client-for-windows--persistent-client-) .

Auto-upgrade can be configured either globally via **MetaDefender IT Access Console>Settings>Global>Device Agents**, or at a group level via **MetaDefender IT Access Console>Inventory>Device Groups>Settings**.

To learn more, [Read This](/docs/macloud-sdp/kb/how-do-i-enable-agent-auto-update-feature-) .

Support:

Should you encounter any issues during the process of **Distributing, Enforcing And Auditing The Persistent MetaDefender Endpoint** **On Your Network**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
