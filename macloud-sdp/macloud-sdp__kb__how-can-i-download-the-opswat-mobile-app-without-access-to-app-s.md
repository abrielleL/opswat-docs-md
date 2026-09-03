<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-can-i-download-the-opswat-mobile-app-without-access-to-app-s -->

# How can I download the OPSWAT Mobile App without access to App Store or Google Play?

This article applies to all OPSWAT Mobile App releases to be deployed on Huawei devices.

Disclaimer:

Gspace and similar tools have neither been tested nor verified by the OPSWAT MetaDefender IT Access team for use with the OPSWAT Mobile App. GSpace has, however, been verified by Huawei and is now available via the Huawei App Gallery.

While OPSWAT Mobile App has been shown to install and function smoothly via the GSpace solution, apps installed outside of the GSpace environment are not visible to OPSWAT Mobile App.

Still, OPSWAT Mobile App is able to monitor phone settings and status, and it is able to scan the apps installed within the GSpace. The extent of this functioning cannot be confirmed without further testing.

While we cannot officially recommend the GSpace tool for mobile device users without access to the App Store or Google Play Store, we suggest it as a possible solution to both install and run the OPSWAT Mobile App on Huawei devices.

GSpace is a popular tool that allows Huawei users to access GSM apps within a sandbox-like environment on their mobile devices, despite the fact that GSM is not officially available for use on Huawei phones.

Because the OPSWAT Mobile App is currently only available via the App Store and Google Play, this tool also indirectly allows Huawei users to access the product via Google Play.

## [Download and install GSpace](/docs/macloud-sdp/kb/how-can-i-download-the-opswat-mobile-app-without-access-to-app-s#download-and-install-gspace)

1. Open the **Huawei AppGallery** and search for an application named **GSpace**.
2. Download and **Install** it.
3. **Launch** Gspace.
4. Click on the **Google** app icon (not the GooglePlay icon, as GSpace requires users to buy VIP membership if they wish to download GooglePlay).

5. **Sign In** to your Google account as prompted.
6. **Install** the Google browser from Google Play Store, as prompted.
7. **Open** the Google browser, search for **Google Play Store**, then **Open** it within the browser.

8. In **Google Play Store**, search for **OPSWAT Mobile App**, then **Install** it.

9. You may be prompted to **Sign In** to Google Play, do so.
10. Once OPSWAT Mobile App is installed, **Launch** it.

11. **Accept** the OPSWAT terms of service, then click the **Register Your Device** button.

12. Scan the **QR Code** or enter the **Registration Code** for the relevant OPSWAT MetaDefender IT Access account.

Pro Tip:

To retrieve the Registration Code or QR Code mentioned above, contact your administrator or, if you are an administrator, do the following:

1. Log into the **MetaDefender IT Access Console** and click the **Add Device** button in the upper right-hand corner of the screen.

2. Click the **Download MetaDefender Endpoint for Distribution** button, then click on the **Mobile and Chrome OS** tab, after selecting the option to **Assign all devices to a group**, if required.

3. The **QR Code**, **Registration Code** and **Group ID** are all shown here.

13. Your device is now registered and your compliance state is visible to your administrator via **MetaDefender IT Access Console>Inventory>Devices**, as illustrated below.

Please Note:

This method is acknowledged but not highly recommended by the OPSWAT team.

- This method is not effective for scanning installed applications to confirm compliance.
- This is due to the fact that, when OPSWAT Mobile App is installed inside GSpace, only apps also installed within GSpace are visible to it.
Support:

For queries, concerns or issues regarding **The OPSWAT Mobile App on Huawei Mobile Devices Without Access To The App Store or Google Play Store**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
