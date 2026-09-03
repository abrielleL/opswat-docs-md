<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-could-i-find-an-app-id-of-an-application- -->

# How could I find an app ID of an application?

The **App ID** of apps on both Android and iOS systems should be configured when an administrator adds SaaS applications. This is done in order to restrict access, enforce endpoint compliance, and integrate with MetaDefender IT Access via **Universal Link**.

For more about **Access Control**, [Read This](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-guide).

For more about **Universal Link**, [Read This](https://www.opswat.com/docs/cm/developer-guidelines/universal-link).

The App ID is an application URL scheme on iOS, and a package name on Android.

> **Pro Tip:**
>
> An application URL scheme is a way of referencing resources deep inside the app package, that allow for the app to open in a specified context whenever the URL is accessed.
>
> When clicked, the link forwards the user directly to the app without routing through any other browser or website - provided the app is installed on the device.

## On iOS

1. Download the app installer file (*.ipa*) from the App Store.
2. Change the *.ipa* to a *.zip* file by editing the extension.
3. Unzip the file, then open the **Payload** folder.
4. Tap and hold the app **Icon**, then select **Show Package Contents**.
5. Open **Info.plist**.
6. Search for an entry named either **URL Schemes key** or **URL Types key**, this is the app ID.

## On Android

### Option 1: via web browser

1. Open the **Google Play Store** and search for the relevant app.
2. Copy the ID parameter directly from the URL, as illustrated below - this is the package name/app ID.

![](https://uploads.developerhub.io/prod/97qW/b5pgcz0za8k7wcqoul89z07d02j6bpmypx19pecr349asw6ncc76r731mlxn7wcs.png)

### Option 2: via mobile device

1. Install the **ES File Explorer File Manager** app, along with the app for which you’d like to retrieve a package name.
2. Open the **ES File Explorer File Manager** app.
3. Tap on the **App** category, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/t43vm2w0943iesoffzek1j27eoj9glmnmbdroxvgecec3quyxx4urfxa2pi0s6as.png)

4. Now, locate the app for which you’d like to retrieve the package name.

![](https://uploads.developerhub.io/prod/97qW/vdmkt9ghpnsoff8hc8q8zrb1x8wjbflu3718u3u8od2p2x9pmhvrsfecsmep19xt.png)

5. Tap on the app **Icon**. The package name will be shown among the app details, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/93w53fxgf7w4w30emmjrpemhwbs23xlqudl6n486ys6pjycotly2wsil7a8m3m09.png)

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Finding The App ID Of An Application**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
