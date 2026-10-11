<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/troubleshooting/services -->

# Services

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
### [MFT Helper Installation Issue](/docs/mdmft/v3.11.5/troubleshooting/services#mft-helper-installation-issue)

Users may sometimes encounter the message "Mfthelper could not be installed" during the installation process.

#### [Resolution](/docs/mdmft/v3.11.5/troubleshooting/services#resolution)

To address this situation, follow these steps:

1. Restart your computer.

Restarting the PC often resolves issues related to MetaDefender Managed File Transfer™ Helper installation. After restarting, attempt the installation process again to see if the problem persists.

---

### [Nginx Startup Failure After MetaDefender MFT Installation](/docs/mdmft/v3.11.5/troubleshooting/services#nginx-startup-failure-after-metadefender-mft--installation)

Users may face difficulties starting Nginx after successfully installing MetaDefender Managed File Transfer, which may be due to port 8000 or 8010 being in use during the restart.

#### [Resolution](/docs/mdmft/v3.11.5/troubleshooting/services#resolution)

To address this situation, follow these steps:

1. Restart your computer.

Restarting the PC can resolve issues related to port conflicts and Nginx startup failures. After the restart, attempt to launch MetaDefender MFT again.

---

### [Service Restart Issue After Installation with Windows Authentication](/docs/mdmft/v3.11.5/troubleshooting/services#service-restart-issue-after-installation-with-windows-authentication)

Users may face difficulties manually restarting services after installing with the "Windows Authentication" option, especially in versions 3.0.8 or higher. This issue can be resolved by enabling service logon after the installation.

#### [Resolution](/docs/mdmft/v3.11.5/troubleshooting/services#resolution)

Follow the instructions provided in the link to enable service logon: [Enable service logon | Microsoft Docs](https://docs.microsoft.com/en-us/system-center/scsm/enable-service-log-on-sm?view=sc-sm-2022)

This ensures proper functionality of the services and resolves the post-installation restart issue.

---

### [MetaDefender Managed File Transfer service is not accessible](/docs/mdmft/v3.11.5/troubleshooting/services#metadefender-managed-file-transfer-service-is-not-accessible)

If the MetaDefender Managed File Transfer web UI is inaccessible and you encounter a *502 Bad Gateway* error, the root cause could be one of the following:

1. **Firewall blocking the server:**

   - Add the server to your firewall’s allowlist
2. **Accessing the web UI from a different machine:**

   - Open the 8010 web UI port (default)
3. **MetaDefender Managed File Transfer installation failure:**

   - Either fix the installation or reinstall MetaDefender Managed File Transfer
   - Check if the MetaDefender Managed File Transfer *REST service* is running
