<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-address-os-update-issues-on-opswat-client-metaaccess-am -->

# How do I address OS update issues on MetaDefender Endpoint/MetaDefender IT Access among managed Windows device?

This article is applicable to the latest MetaDefender IT Access Console and API, as well as all MetaDefender Endpoint releases deployed on Windows systems."

MetaDefender IT Access provides variety compliance options tailored to different operating systems. Specifically for Windows devices, we've implemented a dedicated rule aimed at compelling users to regularly update their operating systems. This involves monitoring the current patching status and detecting any available but uninstalled updates. This proactive approach ensure that system remain current, benefiting from the latest enhancements and security patches, ultimately bolstering device stability and security.

Administrators have the flexibility to determine the frequency at which users are prompted to update their operating system. This can be configured by activating the '**Update(s) have been available**' condition under **Policy > Deep Compliance > Operating System > Windows**, allowing administrators to specify the desired update interval in days. A smaller number indicates a more frequent check for operating system updates.

To remediate OS update compliance issues on managed Windows devices, please follow the relevant instructions below.

### [Check Windows Update](/docs/macloud-sdp/kb/how-do-i-address-os-update-issues-on-opswat-client-metaaccess-am#check-windows-update)

- Go to Windows Start menu, search for Check for updates, then click in the first results.

- On the Windows Update page, click **Check for updates** to check for available updates**.**

- Proceed to download and install the recommended updates. Please note that you may be asked to close all running programs and restart the machine if needed.
- Once the installation is done, open the Windows **Start** menu, search for **MetaDefender Endpoint**, and select **Run as administrator**.

- Once the OPSWAT Client is running, right-click on the Client tray icon and click **Recheck .**

### [Through MetaDefender Endpoint](/docs/macloud-sdp/kb/how-do-i-address-os-update-issues-on-opswat-client-metaaccess-am#through-metadefender-endpoint)

- Go to the Windows Start menu, search for MetaDefender Endpoint, and select Run as Administrator.

- On the left panel, click the **OS Updates** section.
- On the OS Updates page, you will find a list of available OS patches. Click the button on the right side of an update to install it, or click **Update All** to install all updates.

- Once the installation is done, right-click on the Client tray icon and click **Recheck**.

Pro Tip

If you wish to install new updates automatically, you can use OPSWAT Client’s auto-update feature by switch on the Auto-Update button on the OS Updates page.

### [Install OS updates manually](/docs/macloud-sdp/kb/how-do-i-address-os-update-issues-on-opswat-client-metaaccess-am#install-os-updates-manually)

If the above approaches are not working, you may need to download and install the OS updates manually.

1. Go to the Windows Start menu, search for the **winver** command, then click on the first result.

2. You will find the running OS version and the current build information here.

3. Head to the [**Windows release information page**](https://learn.microsoft.com/en-us/windows/release-health/release-information). On the left panel, choose the appropriate release information page based on your running OS (Windows 11, Windows 10, or others).

4. On the release information page, find the section for your OS version. You will see a list of builds under the chosen version. Look for the most recent build and click on the link in the **KB article** column.

5. On the KB page, scroll down to the **How to get this update** section and find the instructions to install the update through the **Microsoft Update Catalog** release channel.

6. On the **Microsoft Update Catalog** page, download the appropriate package based on your running OS version and your architecture system.

7. Once the download process is done, double-click on the update package and follow the instructions to install it.
8. Once the installation is done, open the Windows **Start** menu, search for **MetaDefender Endpoint**, and select **Run as administrator**.

9. Once the **MetaDefender Endpoint** is running, right-click on the MetaDefender Endpoint tray icon and click **Recheck**.

Support

If you have followed the instructions above but **Continue To Experience OS update issues on** **MetaDefender Endpoint / MetaDefender IT Access** **managed Windows devices**, please open a [**Support Case**](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [**OPSWAT Expert Forum**](https://go2.opswat.com/s).
