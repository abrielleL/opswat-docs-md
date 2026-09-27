<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/operating/create-app-configuration-policy-to-managed-apps-for-ios-devices -->

# Create app configuration policy to managed apps for iOS devices

## About

This document summarizes the configuration steps to add **OPSWAT Mobile App** to Microsoft Intune and setup automatic enrollment using URL protocol (Scheme)/Schema Link.

## Prerequisites

- BYOD Device has to install Microsoft’s Company Portal application in ordered to be managed by Intune.
- Corperated’s own device can be enrolled automatically via Apple Business Manager. Ref: [Set up automated device enrollment (ADE) for iOS/iPadOS - Microsoft Intune](https://learn.microsoft.com/en-us/intune/intune-service/enrollment/device-enrollment-program-enroll-ios)
- Known about Mobile Application Management: [Mobile Application Management (MAM) for unenrolled devices in Microsoft Intune - Microsoft Intune | Microsoft Learn](https://learn.microsoft.com/en-us/intune/intune-service/fundamentals/deployment-guide-enrollment-mamwe)
- Settings catalog: [Create a policy using settings catalog in Microsoft Intune - Microsoft Intune | Microsoft Learn](https://learn.microsoft.com/en-us/intune/intune-service/configuration/settings-catalog?tabs=sc-search-filter%2Csc-reporting)

## Set up Managed Application for iOS

Please see more details at this page [https://www.opswat.com/docs/mdendpoint/operating/automatic-deployment-opswat-mobile-app-ios](https://www.opswat.com/docs/mdendpoint/operating/automatic-deployment-opswat-mobile-app-ios)

## Set up Manage Apps Configuration

On Microsoft Intune navigation pane, follow the steps:

Step 1: Select **Apps**.

Step 2: The Apps overview pane opens.

Step 3: Under **Manage Apps**, select **Configuration**.

Step 4: Select **Select** > **Managed apps**

Step 5: The Create app configuration policy pane opens.

Step 6: In the **Basics** tab, do the following:

a. In the **Name** field, enter **OPSWAT MAM Mobile App**.

b. From the **Target policy to** drop-down menu, select **Selected App**.

c. From the **Custom app**, select custom app:

d. Use schema link

```json
// Schema name
metaaccess
gears

//For URL open OPSWAT
metaaccess://
gears://
```

e. Under Bundle or Package ID from More apps > Type metaaccess

f. Select Platforms: iOS/iPadOS

g. Select Add > App will move to Selected Apps > Select Select

h. Click Next

![](https://uploads.developerhub.io/prod/2x2P/c9jz03860q0bh4lzajlaornxvpyv4tuxrpim04ck4ucc1vb4chyj2w2h62spp8fv.png)

Step 7: In **Settings Catalog** tabs > Add your **policy** > Select **Next**

Step 8:  In **Settings** tabs:

1. Add your config Microsoft Tunnel for Mobile Application Management settings > Select Next
2. Select the value types and enter the **General configuration** for the following configuration keys*. Then, select **Next**.

| **Name key** | **Value** |
| ---- | ---- |
| `Your name key` | Your value pass to OPSWAT **(Required)** |

Step 9: The **Assignments** tab opens > Under **Included groups**, select **Add all users** and select **Next**.

Step 10: The **Review + create** tab opens.

Step 11: Select **Create**.

> **Info**
>
> For using General configuration settings in Mobile Application Management (MAM), we need to add SDK Intune and define configuration data to support sending any app configuration data.

## Recommendations

> **Info**
>
> Use Mobile Device Management (MDM) + Mobile Application Management (MAM) together, this MAM help to add App Protection Policies to Office mobile apps—even on enrolled devices

> **Info**
>
> For auto-register features should using MDM Intune, please see more details at this page [https://www.opswat.com/docs/mdendpoint/operating/automatic-deployment-opswat-mobile-app-ios](https://www.opswat.com/docs/mdendpoint/operating/automatic-deployment-opswat-mobile-app-ios)

## Download & setup Company Portal App

1. Go to **App Store**
2. Download **Company Portal** app **(Microsoft)**
3. Login **Microsoft** account
4. Setup **add work profile**
5. **Auto-enrollment will be active**
6. **OPSWAT Mobile App** will **automatically** download to devices.

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
