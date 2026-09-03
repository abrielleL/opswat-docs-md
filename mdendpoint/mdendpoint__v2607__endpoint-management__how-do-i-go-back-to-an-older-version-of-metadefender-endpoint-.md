<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-do-i-go-back-to-an-older-version-of-metadefender-endpoint- -->

# How do I go back to an older version of MetaDefender Endpoint?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows or macOS systems.

> **Pro Tips:**
>
> All supported versions of the Persistent MetaDefender Endpoint are accessible via the **MetaDefender IT-OT Access** **Console**, and can be downloaded as per the instructions below.
>
> However, OPSWAT highly recommends that you maintain the latest MetaDefender Endpoint across your network of managed devices, in order to benefit from the latest features, functions and bug-fixes.

## Option 1: from the MetaDefender IT-OT Access Console

> **Please note:**
>
> The process outlined below will not affect any already-installed MetaDefender Endpoint instances.

To set the version of MetaDefender Endpoint that’s available on your personalized download page, please follow the instructions below.

1. Log into the **MetaDefender IT-OT Access Console** and navigate to the **Settings>Global** tab.
2. Select the **Enforce download managed agent version** option, select the version you want to download, then click **Save**, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/1yda/9lmly00qc55lec8zv109hb8uv2sfmda8v02dh4b0dpuoy0c37qce9p2abuwovae9.png)

3. Now, click on the **+Device** button in the top right-hand corner of your **MetaDefender IT-OT Access Console**, then select to **Download MetaDefender Endpoint for Distribution**, as shown below.

![](https://uploads.developerhub.io/prod/2x2P/jt4beudn8966zu35ssdh4leaau3403yeoeawh5l6kprkz3y49917ythb2ok14kvs.png)

4. You will now be directed to your personalized download page, where you can download installers for the selected version for each operation system, as shown in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/5wn2lyib1zdciodbpqfke5fbqjfea48hu78etwb08iap1bvsq2813ccpu92w3swz.png)

## Option 2: from the MetaDefender IT-OT Access Archives

> **Please note:**
>
> Archived installers are provided for archival and testing purposes only, and are available via the following links:
>
> - [Windows Installer Archive](https://s3-us-west-2.amazonaws.com/opswat-gears-cloud-clients/index.html?prefix=windows_installer/)
> - [Windows Portable Archive (UAC and Non-UAC Versions)](https://s3-us-west-2.amazonaws.com/opswat-gears-cloud-clients/index.html?prefix=windows_portable/)
> - [macOS Installer Archive](https://s3-us-west-2.amazonaws.com/opswat-gears-cloud-clients/index.html?prefix=osx_installer/)
> - [macOS Portable Archive](https://s3-us-west-2.amazonaws.com/opswat-gears-cloud-clients/index.html?prefix=osx_portable/)

When using one of the archived installers, further steps must be taken to associate it with your account.

After downloading the archived installer of your choice, please follow the instructions below.

1. Log into your **MetaDefender IT-OT Access Console** and navigate to **Settings>Global>Account** to look up your license key.
2. Rename the archived installer file according to the relevant format below, where **XXXXXXXXXXXX** represents your license key:

- Windows Persistent MetaDefender Endpoint: rename the ***.msi*** file to **OPSWAT_GEARS_CLIENT_3445-XXXXXXXXXXXX.msi**
- Windows On-Demand MetaDefender Endpoint: rename the ***.exe*** file to **opswat-gears_3445-XXXXXXXXXXXX.exe** or **opswat-gears-admin_3445-XXXXXXXXXXXX.exe**
- macOS Persistent MetaDefender Endpoint: rename the ***.dmg*** file to **OPSWAT_GEARS_CLIENT_3445-XXXXXXXXXXXX.dmg**
- macOS On-Demand MetaDefender Endpoint: rename the ***.zip*** file to **OPSWAT_GEARS_Client_2358-XXXXXXXXXXXX.zip**

> **Pro Tips:**
>
> Upon completion of the Option 1 or Option 2 steps above, you can apply the historic release by running the file and letting the Setup Wizard guide you through the install process.

> **Support:**
>
> If you have followed the relevant instructions below but are **Unable To Download Or Run The Historic** **MetaDefender Endpoint** **Release**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
