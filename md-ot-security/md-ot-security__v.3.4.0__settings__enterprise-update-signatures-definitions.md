<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/settings/enterprise-update-signatures-definitions -->

# Enterprise - Update Signatures & Definitions

## [How to Update CVEs Offline](/docs/md-ot-security/v.3.4.0/settings/enterprise-update-signatures-definitions#how-to-update-cves-offline)

This guide explains the steps to update the CVE (Common Vulnerabilities and Exposures) database offline, ensuring continuous vulnerability updates in environments without internet access.

The **Update CVEs** is accessible under **Settings > Update CVEs**

### [1. Navigating to the Update CVEs Feature](/docs/md-ot-security/v.3.4.0/settings/enterprise-update-signatures-definitions#1-navigating-to-the-update-cves-feature)

1. Go to **Settings** from the main menu.
2. Under **Settings**, select **Update CVEs**.

### [2. Obtaining the CVE Database Update File](/docs/md-ot-security/v.3.4.0/settings/enterprise-update-signatures-definitions#2-obtaining-the-cve-database-update-file)

To update the CVE database offline, you need the latest database file:

1. Obtain the database update file from the official source or designated provider at: **Signature & Definition Update:** <https://my.opswat.com/home/metaDefender-ot-security>
2. Save the file to a secure and accessible location on your system.

### [3. Updating the CVE Database](/docs/md-ot-security/v.3.4.0/settings/enterprise-update-signatures-definitions#3-updating-the-cve-database)

Follow these steps to upload the CVE update file to the system:

1. Navigate to the **Update CVEs** page under **Settings**.
2. Click the **Upload** button on the screen.
3. In the file selection window, locate and select the downloaded database update file.
4. Confirm the upload.

### [4. Completing the Update Process](/docs/md-ot-security/v.3.4.0/settings/enterprise-update-signatures-definitions#4-completing-the-update-process)

1. Once the file is uploaded, the system will process the update automatically.
2. A confirmation message will indicate whether the update was successful.

### [5. Verifying the Update](/docs/md-ot-security/v.3.4.0/settings/enterprise-update-signatures-definitions#5-verifying-the-update)

1. Check the **Last Updated** date or version number on the **Update CVEs** page to confirm the update.
2. Test system functionality or scan results to ensure the latest vulnerabilities are included.

### [Benefits of Offline CVE Updates](/docs/md-ot-security/v.3.4.0/settings/enterprise-update-signatures-definitions#benefits-of-offline-cve-updates)

- **Continuous Protection:** Ensures the system remains updated even without internet access.
- **Secure Environments:** Maintains security for air-gapped or restricted networks.
- **Ease of Use:** Simple file upload process for administrators.
