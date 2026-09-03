<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-can-i-synchronize-devices-from-active-directory-to-my-metaac -->

# How can I synchronize devices from Active Directory to my MetaDefender IT Access account?

This article applies to all MetaDefender IT Access products deployed on Windows systems.

Pro Tip:

Administrators who have Active Directory Domain Services installed have the option to synchronize those devices to their MetaDefender IT Access account, enabling them to see which of their managed endpoints have the MetaDefender Endpoint installed, and which do not.

Devices without the MetaDefender Endpoint installed will be flagged as *Unknown_devices*, helping administrators ensure compliance through all new devices that join or are added to their domain network.

To synchronize devices from Active Directory to your MetaDefender IT Access account, please follow the instructions below.

1. Log into your MetaDefender IT Access Console and navigate to **Inventory>Device Groups**.
2. Click on the download link in the note at the top of the page, where it says **Click Here**, as illustrated in the screenshot below.

3. Follow the instructions on the download page to set up a **PIN**, if required, then click **Download** to download the OPSWAT Domain Controller Client.

4. Once downloaded, let the **Installation Wizard** guide you through the install process.
5. Enter your **PIN** to activate the product.

Please Note:

Only administrator users will be able to install and run the OPSWAT Domain Controller Client.

6. Select **OU**s to synchronize devices from your Active Directory to MetaDefender IT Access.

Each OU selected will be reported as a **Device Group** to MetaDefender IT Access, along with your **Domain Name** or your **Domain Controller**. Administrators can re-select OUs to synchronize devices to MetaDefender IT Access by clicking the **Select OUs to sync** option menu on the Domain Controller Client tray icon (see step 7 on activating the tray icon).

Pro Tip:

Should you not select any OUs, all devices will be grouped into a group with the same name as the domain.

Every 15 minutes, the MetaDefender Endpoint will ping the Active Directory domain controllers to sync any changes, then in-turn, these changes will be synced to MetaDefender IT Access. All MetaDefender Endpoints perform this compliance check at 15 minute intervals by default.

7. Following installation, the domain controller will run continuously as a background process.

To activate the controller’s tray icon, simply search for OPSWAT **Domain Controller Client** from the start menu.

If you encounter any connection problems, with errors such as **Connection terminated** or **Incompatible SSL**, please download [This Script](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/OPSWATClient/TLS_registry_update.reg), then run it as administrator to enable TLS1.1 and TLS 1.2 by default. Alternatively, [Read This Guide](https://support.microsoft.com/en-us/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392).

Support:

If you have followed the instructions above but are having difficulty **Synchronizing Devices From Active Directory To Your** **MetaDefender IT Access** **Account**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
