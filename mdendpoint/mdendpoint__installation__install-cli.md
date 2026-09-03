<!-- source: https://www.opswat.com/docs/mdendpoint/installation/install-cli -->

# Install Process

> **Check Your Product:**
>
> This article applies to all persistent MetaDefender Endpoint releases deployed on Windows systems.

Yes, you can. Microsoft Active Directory is a powerful directory service that can be used to distribute MetaDefender Endpoint on managed endpoint PCs.

### [Distribution through one-time, Automatic Installation](https://docs.opswat.com/macloud-sdp/kb/can-i-use-active-directory-to-distribute--enforce-or-audit-opswa#distribution-through-one-time-automatic-installation)

Because it is packaged as a Microsoft Software Installer (or MSI), the persistent MetaDefender Endpoint facilitates streamlined distribution to all managed endpoints.

A simple, one-time installation can be performed by hosting your MetaDefender Endpoint installer in a central location, and then referencing it as a parameter to **MSIEXEC**.

For example, the following line would execute a silent installation of an MetaDefender Endpoint installer, hosted on a shared network drive that is mounted as drive Z:

```powershell
Z: MSIEXEC /a "Z:\Shared\Public\OPSWAT_GEARS_Client_3445-2e5e65e6b68ce141d-0.msi" /qn
```

### [Enforcement through Software Assignment](https://docs.opswat.com/macloud-sdp/kb/can-i-use-active-directory-to-distribute--enforce-or-audit-opswa#enforcement-through-software-assignment)

Active Directory can not only be used to distribute and install the software, as mentioned above, but also to enforce that it remains installed.

In Active Directory terms, this is known as ‘assigning software.’

You have the option to assign software to authenticated users or machines. Both are viable options, and you should choose the one that aligns with your other corporate software installations and infrastructure.

To learn more, read the official Microsoft guide, found [Here](https://docs.microsoft.com/en-US/troubleshoot/windows-server/group-policy/use-group-policy-to-install-software).
