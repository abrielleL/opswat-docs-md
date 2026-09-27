<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-can-i-check-what-account-metadefender-endpoint-on-my-device- -->

# How can I check what account MetaDefender Endpoint on my device is reporting to?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux and Android systems.

Instructions for retrieving version information from MetaDefender Endpoint vary per Client type, operating system, and UI setting.

## [Windows/macOS with the MetaDefender Endpoint tray icon enabled](https://docs.opswat.com/macloud-sdp/kb/how-can-i-check-what-account-opswat-client-on-my-device-is-repor#windowsmacos-with-the-metadefender-endpoint-tray-icon-enabled)

1. Right-click the **Client Tray Icon**.
2. Select the **About** option.
3. The account to which the Client is reporting is listed under **Managed By**.
4. Also, please ensure that the **Server** to which the device is connecting is listed correctly.

> **Pro Tip:**
>
> Incorrect server listings can occur when the downloaded MetaDefender Endpoint was installed from a Client package download that was associated with a different OPSWAT account.
>
> To correct this, the end user should uninstall the MetaDefender Endpoint completely before downloading and installing a fresh Client package from the appropriate OPSWAT account. To request a suitable download, contact your MetaDefender IT-OT Access administrator, who will access the download link via the MetaDefender IT-OT Access Console’s **+Device** button.

![](https://uploads.developerhub.io/prod/1yda/sq7u3cu86y2cyd6z5ie594j5xbkawatqft2k1ia245v0cl64qa8vbuqitzr8taza.png)

## [Linux](https://docs.opswat.com/macloud-sdp/kb/how-can-i-check-what-account-opswat-client-on-my-device-is-repor#linux)

1. To check management account details, run the command: **opswat-client -i**
2. The account to which the Client is reporting is listed under **Managed By**.
3. Also, please ensure that the **Server** to which the device is connecting is listed correctly.

## [Android/Mobile App](https://docs.opswat.com/macloud-sdp/kb/how-can-i-check-what-account-opswat-client-on-my-device-is-repor#androidmobile-app)

1. Open the mobile app.
2. Click the **Menu** icon at the top right-hand side of the screen.
3. Select the **About** option.
4. The account to which the Client is reporting is listed under **Managed By**.
5. Also, please ensure that the **Server** to which the device is connecting is listed correctly.

> **Support:**
>
> For any queries, concerns or issues regarding **Retrieval Of Management Account Details From MetaDefender Endpoint**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
