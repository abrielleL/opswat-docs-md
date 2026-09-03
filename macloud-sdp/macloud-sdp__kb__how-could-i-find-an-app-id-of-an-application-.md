<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-could-i-find-an-app-id-of-an-application- -->

# How could I find an app ID of an application?

This article applies to all OPSWAT Mobile App releases deployed on Android and iOS devices.

The **App ID** of apps on both Android and iOS systems should be configured when an administrator adds SaaS applications. This is done in order to restrict access, enforce endpoint compliance, and integrate with MetaDefender IT Access via **Universal Link**.

For more about **Access Control**, [Read This](/docs/macloud-sdp/secure-access/how-it-works).

For more about **Universal Link**, [Read This](/docs/macloud-sdp/developer-guide/universal-link).

The App ID is an application URL scheme on iOS, and a package name on Android.

Pro Tip:

An application URL scheme is a way of referencing resources deep inside the app package, that allow for the app to open in a specified context whenever the URL is accessed.

When clicked, the link forwards the user directly to the app without routing through any other browser or website - provided the app is installed on the device.

## [On iOS](/docs/macloud-sdp/kb/how-could-i-find-an-app-id-of-an-application-#on-ios)

1. Download the app installer file (*.ipa*) from the App Store.
2. Change the *.ipa* to a *.zip* file by editing the extension.
3. Unzip the file, then open the **Payload** folder.
4. Tap and hold the app **Icon**, then select **Show Package Contents**.
5. Open **Info.plist**.
6. Search for an entry named either **URL Schemes key** or **URL Types key**, this is the app ID.

## [On Android](/docs/macloud-sdp/kb/how-could-i-find-an-app-id-of-an-application-#on-android)

### [Option 1: via web browser](/docs/macloud-sdp/kb/how-could-i-find-an-app-id-of-an-application-#option-1-via-web-browser)

1. Open the **Google Play Store** and search for the relevant app.
2. Copy the ID parameter directly from the URL, as illustrated below - this is the package name/app ID.

### [Option 2: via mobile device](/docs/macloud-sdp/kb/how-could-i-find-an-app-id-of-an-application-#option-2-via-mobile-device)

1. Install the **ES File Explorer File Manager** app, along with the app for which you’d like to retrieve a package name.
2. Open the **ES File Explorer File Manager** app.
3. Tap on the **App** category, as illustrated below.

4. Now, locate the app for which you’d like to retrieve the package name.

5. Tap on the app **Icon**. The package name will be shown among the app details, as illustrated below.

Support:

If you have followed the instructions above but are having difficulty **Finding The App ID Of An Application**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
