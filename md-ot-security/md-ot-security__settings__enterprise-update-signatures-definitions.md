<!-- source: https://www.opswat.com/docs/md-ot-security/settings/enterprise-update-signatures-definitions -->

# Enterprise - Update Signatures & Definitions

## [CVE Definitions - How to Update CVEs Offline](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#cve-definitions----how-to-update-cves-offline)

This guide explains the steps to update the CVE (Common Vulnerabilities and Exposures) database offline, ensuring continuous vulnerability updates in environments without internet access.

The **CVE Definitions** are accessible under **Settings > Update Signatures & Definitions > CVE Definitions**

### [1. Navigating to the CVE Definitions Feature](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#1-navigating-to-the-cve-definitions-feature)

1. Go to **Settings** from the main menu.
2. Under **Settings**, select **CVE Definitions**

### [2. Obtaining the CVE Database Update File](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#2-obtaining-the-cve-database-update-file)

To update the CVE database offline, you need the latest database file:

1. Obtain the database update file from the official source or designated provider at:

**Signature & Definition Update:** <https://my.opswat.com/home/metaDefender-ot-security>

2. Save the file to a secure and accessible location on your system.

### [3. Updating the CVE Database](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#3-updating-the-cve-database)

Follow these steps to upload the CVE update file to the system:

1. Navigate to the **CVE Definitions** page under **Settings**.
2. Click the **Upload** button on the screen.
3. In the file selection window, locate and select the downloaded database update file.
4. Confirm the upload.

### [4. Completing the Update Process](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#4-completing-the-update-process)

1. Once the file is uploaded, the system will process the update automatically.
2. A confirmation message will indicate whether the update was successful.

### [5. Verifying the Update](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#5-verifying-the-update)

1. Check the **Last Updated** date or version number on the **CVE Definitions** page to confirm the update.
2. Test system functionality or scan results to ensure the latest vulnerabilities are included.

### [Benefits of Offline CVE Updates](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#benefits-of-offline-cve-updates)

- **Continuous Protection:** Ensures the system remains updated even without internet access.
- **Secure Environments:** Maintains security for air-gapped or restricted networks.
- **Ease of Use:** Simple file upload process for administrators.

## [PLC Firmware - How to Update PLC Firmware database](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#plc-firmware---how-to-update-plc-firmware-database)

This guide provides step-by-step instructions to update the **PLC Firmware database**, ensuring it stays up to date with the **Patching Management** feature for improved security and functionality.

The **PLC Firmware** is accessible under **Settings > Update Signatures & Definitions > PLC Firmware**

## [1. Navigating to the PLC Firmware Feature](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#1-navigating-to-the-plc-firmware-feature)

1. Go to **Settings** from the main menu.
2. Under **Settings**, select **Update Signatures & Definitions > PLC Firmware**

## [2. Updating the PCL Firmware Database](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#2-updating-the-pcl-firmware-database)

There are **two ways** to update the **PLC Firmware database**:

1. Upload Manually

- Click **"Upload Manually"** and select the firmware file from your local system.
- Confirm and apply the update.

2. Get From Cloud Repo

- Click **"Get From Cloud Repo"** to automatically download the latest firmware.
- The system will fetch and apply the update from the cloud.

## [3. View Firmware Inventory](/docs/md-ot-security/settings/enterprise-update-signatures-definitions#3-view-firmware-inventory)

To check the firmware status:

- Click **"View Firmware Inventory"** to see all available firmware versions.
- This ensures that the latest updates are successfully applied.

The **Firmware Inventory** provides a detailed list of installed firmware, allowing for easy tracking and validation of updates.

Keeping the **PLC Firmware** up to date ensures better compatibility, security, and performance for **Patching Management**.
