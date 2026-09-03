<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/troubleshooting/troubleshoot-microsoft-defender-atp-license -->

# Verify and Troubleshoot Microsoft Defender ATP License Status on Endpoints

> **Check Your Product**
>
> This article applies to Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP), now known as Microsoft Defender for Endpoint, all MetaDefender Endpoint releases deployed on macOS or GNU/Linux systems.

## Overview

Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP), now known as Microsoft Defender for Endpoint, requires a valid license for complete protection, including Endpoint Detection and Response (EDR), threat analytics, and advanced reporting. Endpoints may encounter issues like expired or missing licenses, which can cause MetaDefender Endpoint to report Real-Time Protection status (RTP) as **disabled** (in case of running on macOS or GNU/Linux), it will mark these endpoints as non-compliant devices.

The purpose of this article is to:

- Provide **platform-specific steps** for checking license validity/RTP status.
- Suggest **troubleshooting solutions** if licensing problems are detected.

---

## How to Check Microsoft Defender for Endpoint License

### 1. Platform: macOS

**Check the license status**

When Microsoft Defender for Endpoint on macOS is being deployed, an error message with an x on top of the Microsoft Defender for Endpoint on macOS shield appears.

![](https://uploads.developerhub.io/prod/2x2P/q6fxohfoojqes5of4auqptbruiilzfkrnjg9kolttdeqcx7ypw3qxekf3b8sl0ki.png)

When you select the **x** symbol, it will show some options include “**Action Needed**“, then choose it.

![](https://uploads.developerhub.io/prod/2x2P/6rrvr00yu6wlt54tftsroz7fwx53bp098w2j10xkv0f8kaygbmth0afbcgdbooc7.png)

The error message that indicates license problem will be shown as below:

![](https://uploads.developerhub.io/prod/2x2P/6vsu7g8120dywwj2amajhvqvtwhxd35o5bpyeih1usc0nx3bzjtf1ypmftsaopm8.png)

You can also get this error message through command line `mdatp health`

![](https://uploads.developerhub.io/prod/2x2P/menca1w9qsddkq2jzh9www20u2c6w01oejkv882q5wr9zgffwrartxfxv7f9zy4b.png)

**Possible root causes**

This error can come from various scenarios:

- The Microsoft Defender for Endpoint on macOS installation package has been deployed and/or installed, but the configuration script containing the license settings was not executed
- The Microsoft Defender for Endpoint on macOS agent is not up to date
- When offboarding and re-onboarding macOS devices to Microsoft Defender for Endpoint
- If a license has not been assigned to a user

### 2. Platform: Platform GNU/Linux

**Check the license status**

1. Open the Terminal by pressing `Ctrl+Alt+T` (or search “Terminal” in your applications menu).
2. Run the command: mdatp health

In case there are **no license found**, it will show like this.

![](https://uploads.developerhub.io/prod/2x2P/131oa1654c0ro2bx6703n8okdcimanwltndz5sc2tz0lscgbgmq9xc4357ndj4ot.png)

**Possible root causes**

- Not onboarded – The device is not onboarded to your tenant.

---

## Solutions

### 1. Platform: macOS

**If you didn't run the configuration script**

Depending on the deployment management tool used, follow the tool-specific instructions to onboard the package (register the license) as described in the following table:

| **Management** | **License deployment instructions (Onboarding instructions)** |
| ---- | ---- |
| Intune | [Intune-based deployment for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/mac-install-with-intune#step-15-check-device-and-configuration-status) |
| JamF | [Set up the Microsoft Defender for Endpoint on macOS policies in Jamf Pro - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/mac-jamfpro-policies#step-1-get-the-microsoft-defender-for-endpoint-onboarding-package) |
| Other MDM | [Deployment with a different Mobile Device Management (MDM) system for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/mac-install-with-other-mdm#license-settings) |
| Manual installation | [Manual deployment for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/mac-install-manually#download-installation-and-onboarding-packages); and [Manual deployment for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/mac-install-manually#onboarding-package) |

**If Microsoft Defender for Endpoint on macOS isn’t up to date**

You must update the agent to resolve the issue ([Deploy updates for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/mac-updates))

**If Microsoft Defender for Endpoint on macOS has been offboarded**

When the offboarding script is executed on the macOS, it saves a file in `/Library/Application Support/Microsoft/Defender/` and it's named `com.microsoft.wdav.atp.offboarding.plist`.

If the file exists, it prevents the macOS from being onboarded again. Delete the **com.microsoft.wdav.atp.offboarding.plist** running the onboarding script again.

**If a license isn't assigned to a user**

Visit original document for more detail: [Troubleshoot license issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint | Microsoft Learn](https://learn.microsoft.com/en-us/defender-endpoint/mac-support-license#solutions)

### 2. Platform: Platform GNU/Linux

These steps are implemented to onboard endpoint to your organization’s tenant. To get the onboarding script, you would need to contact to your administrators.

**Step 1:** Download the onboarding package from Microsoft Defender portal by following these steps:

In the first drop-down menu, select **Linux Server** as the operating system.

In the second drop-down menu, select **Local Script** as the deployment method.

Select **Download onboarding package**. Save the file as `WindowsDefenderATPOnboardingPackage.zip`.

![](https://uploads.developerhub.io/prod/2x2P/1e50sacwed5on48djiq94y3mtzqxh1cjkizmz5336ty4r1u6cugfzloi5ugze2iz.png)

From a command prompt, extract the contents of the archive: `unzip WindowsDefenderATPOnboardingPackage.zip`

**Step 2:** Download the [installer bash script](https://github.com/microsoft/mdatp-xplat/blob/master/linux/installation/mde_installer.sh) provided in Microsoft’s public [GitHub repository](https://github.com/microsoft/mdatp-xplat/).

**Step 3:** Grant executable permissions to the installer script: `chmod +x mde_installer.sh`

**Step 4:** Execute the installer script and provide the onboarding package as a parameter to install the agent and onboard the device to the Defender portal.

`sudo ./mdeinstaller.sh --install --onboard ./MicrosoftDefenderATPOnboardingLinuxServer.py --channel prod --min` req``

This command deploys the latest agent version to the production channel, check for min system requisites and onboard the device to Defender Portal.

---

## References

1. [Troubleshoot license issues for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/mac-support-license)
2. [Deploy Microsoft Defender for Endpoint on Linux manually - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/linux-install-manually)
3. [Manual deployment for Microsoft Defender for Endpoint on macOS - Microsoft Defender for Endpoint](https://learn.microsoft.com/en-us/defender-endpoint/mac-install-manually)
