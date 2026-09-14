<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-set-up-opswat-kiosk-to-copy-files-to-a-secondary-location -->

# How to Set Up OPSWAT Kiosk to Copy Files to a Secondary Location for an AD User?

This article provides step-by-step instructions for configuring OPSWAT Kiosk to copy files processed by the Kiosk to a secondary network location for Active Directory (AD) authenticated users.

#### [**Prerequisites**:](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-set-up-opswat-kiosk-to-copy-files-to-a-secondary-location#prerequisites)

AD setup is required as this is regarding AD users. How to setup AD for Workflows:

https://www.opswat.com/docs/mdkiosk/knowledge-base/can-i-add-groups-from-active-directory-to-metadefender-kiosk-wor

***Steps to Configure*:**

1. **Login into MD Kiosk Web UI**

   1. Navigate to **Workflows → Employee Worflows → File Handling**
2. **Configure Post Action**

   1. Under **Post Action**, select **Copy to Secondary Location**.
   2. Activate **Directory** and fill out the required fields:

      1. **Path**: Enter the remote network location path (Example: [\192.168.0.1\test\folder](file://192.168.0.1/test/folder)).
      2. **Display Name:** Provide an appropriate name that identifies this location clearly.
      3. Setup the **Access Control** for either **Inherited** or **Restricted**:

         1. **Inherited**: Files and folders will inherit the same permissions as the parent folder
         2. **Restricted**: Only Kiosk authenticated users will have the permissions to access their files and folders

#### [**Important**:](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-set-up-opswat-kiosk-to-copy-files-to-a-secondary-location#important)

- Setting **Access Contro**l to **Restricted** is critical, as this limits file and folder permissions specifically to users who authenticate through the Kiosk.
- The OPSWAT Kiosk feature for copying files only supports Windows network shared folders. Using a file-sharing system on Linux is not supported by this feature.
- This configuration is available for both Allowed & Blocked settings in the File Handling setting.
