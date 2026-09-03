<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/operating/automatic-deployment-and-enrollment-of-the-opswat-mobile-app-usi -->

# Automatic deployment and enrollment of the OPSWAT Mobile App using Intune for Android devices

## About

This document summarizes the configuration steps to add **OPSWAT Mobile App** to Microsoft Intune and setup automatic enrollment using `deep_link` registration.

## Prerequisites

- Connect your Intune account to your managed Google Play account [Connect Intune account to managed Google Play account - Microsoft Intune | Microsoft Learn](https://learn.microsoft.com/en-us/intune/intune-service/enrollment/connect-intune-android-enterprise)
- Add Managed Google Play apps to Android Enterprise devices with Intune [Add and assign Managed Google Play apps to Android Enterprise devices - Microsoft Intune | Microsoft Learn](https://learn.microsoft.com/en-us/intune/intune-service/apps/apps-add-android-for-work#managed-google-play-store-apps)

## Set up Managed Google Play

On Microsoft Intune navigation pane, follow these steps:

**Step 1:** Select **Apps**.

**Step 2:** The Apps overview pane opens.

**Step 3:** Under **Monitor**, choose your **Platforms,** select **Android**.

**Step 4:** Select **Create** > From the **App Type** drop-down menu, select **Managed Google Play app**

**Step 5:** Select **Next** > If you are **connected** with Android Enterprise > **Jump to step 7**

**Step 6:** If you are **not connected** with Android Enterprise, please follow the steps below:

6.1. Check **Status > Not setup**

6.2. Below “I grant Microsoft permission to send both user and device information to Google” > Choose **I agree***

6.3. After **I agree** > Choose **Launch Google to connect now**

6.4.  Popup will open > Sign in with your email > Choose **Sign up for Android only**

6.5. **Android Apps on Google Play** will open > **Sign in** your Google account

6.6. Add your **Business Name**

![](https://uploads.developerhub.io/prod/2x2P/3sf24ww276c9e36gh5biehucf81s4fl5yhxzycrkj4vslbji788nmow8mue4fxoj.png)

6.7. Choose **Next** > Add Data Protection Officer & EU Representative (Optional)

6.8. Choose **Confirm** > Try to refresh your page Intune and check **Status** from Step 6.1. again*

> **Info**
>
> Sometimes Intune website is unable to auto-update. Try to Refresh (F5) your browser and choose again

**Step 7:** If you're already connected with Android Enterprise:

7.1. Google Play View will open:

![](https://uploads.developerhub.io/prod/2x2P/cb55l1oz7miqkeqsyzt9jwqwahb3cgoescg7qktk506w29o5t958s0nzoa5l9jef.png)

7.2. Search application OPSWAT Mobile App

7.3. Click Select (Please wait for around 15 seconds after one-click Select)

![](https://uploads.developerhub.io/prod/2x2P/czhod56cz43nkc4t4zpgg55049dg2qh7igzdzmzplqkjehwobm1a05qai6umn47l.png)

7.4. Click Sync

7.5. In the "All Apps" list, you will find OPSWAT Mobile App (Android)

![](https://uploads.developerhub.io/prod/2x2P/l23v89fff7k8ztrqp3u1mlzh3ifxini0nlzi24a19s9dqcbd0uvotsyqs296x68p.png)

7.6. Click OPSWAT Mobile App - platform Android in the list

7.7. Select Properties

7.8. Select Edit in Assignments

7.9. Assigned your group/roles/users (Required)

## Set up new Groups

On Microsoft Intune navigation pane, do the following:

1. Select **Groups**.
2. The Groups overview pane opens.
3. Select **New Group**
4. In the **Group Type** tabs > Choose **Security**
5. Enter your **Group Name**
6. **Membership type:** Assigned
7. Add **Owners**
8. Add **Members:** can be Groups or Users **(Required)**

## Set up Manage Apps Configuration

On Microsoft Intune navigation pane, do the following:

1. Select **Apps**.
2. The Apps overview pane opens.
3. Under **Manage Apps**, select **Configuration**.
4. Select **Create** > **Managed devices**
5. The Create app configuration policy pane opens.
6. In the **Basics** tab, do the following:
   1. In the **Name** field, enter **OPSWAT Mobile App**.
   2. From the Platform drop-down menu, select **Android Enterprise**.
   3. From the **Profile type** drop-down menu, select **Personally-Owned Work Profile Only**.
   4. Next to **Targeted app**, select **Select app**.
   5. The Associated app pane opens.
   6. Select **OPSWAT Mobile App**, and select **OK** > **Next**.
7. The Settings tab opens.
8. Follow these steps:
   1. Under **Configuration Settings**, from the Configuration settings format drop-down menu, select **Use configuration designer**.
   2. Select **+Add**.
   3. Select the value types and enter the configuration values for the configuration keys from the table below*
   4. Select **Next**.
   5. The **Assignments** tab opens.
   6. Under **Included groups**, select **Add all users** and select **Next**.
   7. The **Review + create** tab opens.
   8. Select **Create**

| **Configuration key** | **Value type** | **Description** |
| ---- | ---- | ---- |
| `Registration Code` | `String` | Your registration code **(Required)** |
| `Group Id` | `String` | Group ID on My OPSWAT Central Management  (**Optional)** |
| `Server Name` | `String` | ID Access domain (`gears.opswat.com / gears-eu.opswat.com`)  **(Optional)** |

## How to check if an app support managed configuration feature

From the reference [Apps that support app configuration | Microsoft](https://learn.microsoft.com/en-us/intune/intune-service/apps/app-configuration-policies-overview), it shows how to check whether an app supports configuration settings:

![](https://uploads.developerhub.io/prod/2x2P/a8vafeiyv61mux7qcpt5bpc4bshbqyjtwlfpbqgat505gv11htkeqhdn9i6bpup6.png)

For developers, please read the guideline below:

> **For developers**
>
> The available configuration parameters and the implementation of the configuration parameters are decided by the developers of the application. Documentation from the application vendor should be reviewed to see what configurations are available and how the configurations influence the behavior of the application. For some applications, Intune will populate the available configuration settings.

> **NOTE**
>
> Auto-enrollment will be only successful if the OPSWAT Mobile App is deployed via Microsoft Intune Admin Center + Company Portal App Installed on Client Device. The precondition is that user’s device doesn’t have out app at that time.

## Recommendations

- After successfully auto-enrollment, user should not manually unregister device. We will have an enhancement for this in the next release.
- Admin need to config with correct information (*Registration Code, Server Address, Group Id* (if group_id invalid → Device will register with Default’s group))

## Download & setup Company Portal App

1. Go to **Play Store**
2. Download **Company Portal** app **(Microsoft)**
3. Login **Microsoft** account
4. Setup **add work profile**
5. **Auto-enrollment will be active**
6. **OPSWAT Mobile App** will **automatically** download to devices and **auto register device**
