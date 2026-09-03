<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-pre-tag-devices-with-a-tag- -->

# How can I pre-tag devices with a tag?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Android and iOS systems.
>
> This feature is not available for MetaDefender Endpoint releases deployed on dissolvable or Linux systems.

My OPSWAT Central Management provides a mechanism for pre-tagging devices according to any arbitrary string, allowing for easy search filtering and streamlining your device administration.

To utilize this feature, there are two options:

- Option 1: **tagging a device via enrollment process**
- Option 2: **tagging a device by editing the device’s nickname with a tag.**

## Option 1: tag devices via enrollment process

### For Windows and macOS devices

This can be done by appending the device installer filename with a device tag name.

- For example, if the managed device installer package for an account is named **OPSWAT_GEARS_Client_3445-d212055151e00f8b6ecd3dfb73032391-0.msi**, and the desired tag is **SanFranciscoOffice**, the installer would be renamed to **OPSWAT_GEARS_Client_3445-d212055151e00f8b6ecd3dfb73032391-0-SanFranciscoOffice.msi**.

### For Android and iOS devices

This can be done by adding a tag to the **Group ID** when you enroll a device to a My OPSWAT Central Management account in advanced mode. For detailed instructions, please [Read This](https://www.opswat.com/docs/cm/kb/how-do-i-register-a-mobile-device-to-a-metaaccess-account-).

> **Pro Tip:**
>
> When you assign a Group ID to a mobile device that’s being added to your  account, the device will be assigned to that group as soon as it connects to the Cloud.

Alternatively, for mobile devices, you can add the tag to the deeplink.

- So, with a **SanFranciscoOffice** tag, the deeplink would be **gears://regcode/*****your reg code*****/SanFranciscoOffice**.

For devices with a Group ID, the administrator could create a new deeplink with the following format:

- **gears://regcode/<registration_code>/group_id>/<serverName>**

The link can be made clickable by using any popular text to link converter, such as [This One](https://www.htmlstrip.com/text-to-link-converter).

If the server Name is null, the application will assume that the code is from production.

If there is no group ID, the deeplink should be created as follows:

- **gears://regcode/TALX5ZJB// gears.opswat.com** **(production URL)**

> **For Example:**
>
> Sample URLs include:
>
> - [gears.opswat.com](http://gears.opswat.com)
> - [gears-staging.opswat.com](http://gears-staging.opswat.com)
> - [gears-beta.opswat.com](http://gears-beta.opswat.com)
> - [gears-eu.opswat.com](http://gears-eu.opswat.com)
> - [metadefender-it-ot-access.opswat.com](http://metaaccess-a.opswat.com)
>
> This is common for iOS and Android.

## Option 2: Tag devices by manually editing their nicknames

### For Windows, macOS, Android and iOS devices

1. Log into your **My OPSWAT Central Management** **Console** and navigate to **Inventory>Devices**.
2. Click on the device that you would like to tag/rename to open the **Device Details** view.
3. Now, click on the pencil icon, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/3uklp8eerx94h4d5pjfg2fbrwr88xcn9pl2oq4q6itltz0hn5u9igskv53e3u28y.png)

4. The name field will now be open for editing.

Rename your device or add the desired tag to the end of the device name, as illustrated in the screenshot below, then hit the **Enter** key to confirm your choice.

![](https://uploads.developerhub.io/prod/97qW/5k2td3ftn0hj1ai0wxdl96ktycmedtoe0gttzcmkrs30gs9vs53thfpq0oyxiwok.png)

## [Where to find devices with a specific tag](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-pre-tag-devices-with-a-tag-#where-to-find-devices-with-a-specific-tag)

### [For Windows, macOS, Android, and iOS devices](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-pre-tag-devices-with-a-tag-#for-windows-macos-android-and-ios-devices)

After tagging a device during enrollment, the nickname of the device will automatically be constructed and displayed as the **hostname** followed by a **hyphen** (-) followed by the **tag name**, with no spaces in between.

So, the format will be ***hostname-tagname***.

This nickname will then be searchable via the **Console** or via **API**.

- **Console**: go to **Inventory>Devices** and enter the tag name into the search field, then click **Search**.
- **API**: conduct a search or use the **Get device API** search parameter to retrieve devices with a specific tag name. For detailed instructions, [Read This](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-devices) .

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Pre-tagging Your Managed Endpoint Devices**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
