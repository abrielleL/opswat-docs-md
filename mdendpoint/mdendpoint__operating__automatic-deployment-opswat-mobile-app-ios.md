<!-- source: https://www.opswat.com/docs/mdendpoint/operating/automatic-deployment-opswat-mobile-app-ios -->

# Automatic deployment and enrollment of the OPSWAT Mobile App using Intune for iOS devices

## About

This document summarizes the configuration steps to add **OPSWAT Mobile App** to Microsoft Intune and setup automatic enrollment using `deep_link` registration.

## Prerequisites

- BYOD Device has to install Microsoft’s Company Portal application in ordered to be managed by Intune.
- Corperated’s own device can be enrolled automatically via Apple Business Manager. Reference: [Set up automated device enrollment (ADE) for iOS/iPadOS - Microsoft Intune](https://learn.microsoft.com/en-us/intune/intune-service/enrollment/device-enrollment-program-enroll-ios)
- Configure MDM Push Certificate for iOS on Intune Admin center. Follow these steps: [Get an Apple MDM Push certificate for Intune - Microsoft Intune](https://learn.microsoft.com/en-us/intune/intune-service/enrollment/apple-mdm-push-certificate-get#steps-to-get-your-certificate)

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

## Set up Managed Application

On Microsoft Intune navigation pane, do the following:

Step 1: Select **Apps**.

Step 2: The Apps overview pane opens.

Step 3: Under **Monitor**, choose your **Platforms,** select **iOS**.

Step 4: Select **Create** > From the **App Type** drop-down menu, select **iOS store app**

Step 5: Select **Select**

Step 6: In **Select App** > Choose **Search App Store**

Step 7: Search & choose **OPSWAT Mobile App**

Step 8: Select **Next**

Step 9: In the **App Information** tabs, information auto filled

![](https://uploads.developerhub.io/prod/2x2P/2xafanor4za82mmj3yfw7iu19udzuu2dv3ts1aq4ugb975jstdmmpfk6dex8ss3x.png)

Step 10: Select **Next**

Step 11: In the **Assignments** tabs > add **required >** add Groups into **available for enrolled devices** (If you don’t have groups, check [Set up new group](https://opswat.atlassian.net/wiki/spaces/GEAR/pages/edit-v2/4402938991#Set-up-new-Groups%3A))

![](https://uploads.developerhub.io/prod/2x2P/kwcuxr84cwirwnhvvph41lr4yzyqv2h5vycospj5y7fmbhkt0vhv31zui542win6.png)

Step 12: Select **Next** > Re-check information app > Select **Create**

## Set up device onboarding enrollment for iOS

1. Select **Devices**.
2. The Devices overview pane opens.
3. Under **Devices Onboarding**, choose your **Enrollment**
4. Choose **Apple**
5. Under **Prerequisites** > Select **MDM Push Certificate**
6. Select **I Agree**
7. Select **Download your CSR** > Get a intune certificate signing request on your local computer
8. Select hyperlink **Create your MDM push Certificate**
   1. Sign in with your organization's Apple ID.
   2. Select **Create a Certificate**.
   3. Read and accept the terms and conditions.
   4. Select **Choose File** and then select the CSR file you downloaded in Intune.
   5. Select **Upload**.
   6. On the confirmation page, select **Download**. The certificate file (.pem) downloads to your device. Save this file for later.
9. Type your **Apple ID**
10. Upload **Apple MDM push certificate** from step 8
11. Select **Upload**

![](https://uploads.developerhub.io/prod/2x2P/l7r43biu1l77rhfxc95tqr7nkwdza7p9yayg300o92if78oecorv0u50qyfrycs8.png)

### Set up Manage Devices Configuration

On Microsoft Intune navigation pane, do the following:

1. Select **Apps**.
2. The Apps overview pane opens.
3. Under **Manage Apps**, select **Configuration**.
4. Select **Create** > **Managed devices**
5. The Create app configuration policy pane opens.
6. In the **Basics** tab, do the following:
   1. In the **Name** field, enter **OPSWAT Mobile App**.
   2. From the Platform drop-down menu, select **iOS/iPadOS**.
   3. From the Profile type drop-down menu, select appropriate Work Profile.
   4. Next to **Targeted app**, select **Select app**.
   5. The Associated app pane opens.
   6. Select **OPSWAT Mobile App**, and select **OK** > **Next**.
7. Do the following:
   1. Under **Configuration Settings**, from the Configuration settings format drop-down menu, select **Use configuration designer**.
   2. Select the value types and enter the configuration values for the following configuration keys*
   3. Example **description - your deep link:  gears://regcode/<registration_code>/<group_id>/<server_address>**
   4. `<registration_code>` – **Required**: the unique registration code used for device enrollment.
   5. `<group_id>` – *Optional*: specify the group the device will belong to.
   6. `<server_address>` – *Optional*: server address if different from the default one.
8. Next, do the following:
   1. Select **Next**.
   2. The **Assignments** tab opens.
   3. Under **Included groups**, select **Add all users** and select **Next**.
   4. The **Review + create** tab opens.
   5. Select **Create**.

| **Configuration key** | **Value type** | **Description** |
| ---- | ---- | ---- |
| `deep_link` | `String` | Your deep link **(Required)** |

## For developers, please read the guideline below:

> **NOTE**
>
> Auto-enrollment will be only successful if the OPSWAT Mobile App is deployed via Microsoft Intune Admin Center + Company Portal App Installed on Client Device. The precondition is that user’s device doesn’t have out app at that time.

## Recommendations

- After successfully auto-enrollment, user should not manually unregister device. We will have an enhancement for this in the next release.
- Admin need to config with correct information (*Registration Code, Server Address, Group Id* (if group_id invalid → Device will register with Default’s group))

## Download & setup Company Portal App

1. Go to **App Store**
2. Download **Company Portal** app **(Microsoft)**
3. Login **Microsoft** account
4. Setup **add work profile**
5. **Auto-enrollment will be active**
6. **OPSWAT Mobile App** will **automatically** download to devices and **auto register device**
