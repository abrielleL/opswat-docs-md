<!-- source: https://www.opswat.com/docs/metadefender-ot-access/2.3.0/knowledge-base/md-core-integration---secure-file-transfer-via-rdp -->

# MD Core Integration - Secure File Transfer via RDP

## [**Overview**](/docs/metadefender-ot-access/2.3.0/knowledge-base/md-core-integration---secure-file-transfer-via-rdp#overview)

This guide describes how to integrate **MetaDefender OT Access** with **MetaDefender Core (MD Core)** to enable secure file transfer during Remote Desktop (RDP) sessions.

With this integration, files are scanned and approved before being securely transferred to remote hosts through OT Access, ensuring controlled and compliant file delivery.

## [**Configure MD Core Settings**](/docs/metadefender-ot-access/2.3.0/knowledge-base/md-core-integration---secure-file-transfer-via-rdp#configure-md-core-settings)

Navigate to: **Settings → Integration**

To establish the integration:

- Enter the **Server Name**
- Provide the **Server Address**

1. Enter the **API Key**

These settings allow OT Access to securely communicate with MD Core.

## [**Upload Files to MD Core**](/docs/metadefender-ot-access/2.3.0/knowledge-base/md-core-integration---secure-file-transfer-via-rdp#upload-files-to-md-core)

After completing the configuration:

- Log in as a **standard user**
- Navigate to the **MD Core Files** section
- Upload the file you want to transfer

At this stage, the file cannot yet be transferred.

## [**File Approval Process**](/docs/metadefender-ot-access/2.3.0/knowledge-base/md-core-integration---secure-file-transfer-via-rdp#file-approval-process)

Before a file can be used:

- A **Super Administrator** must review the uploaded file
- Navigate to the **approval page** in MD Core
- Approve the file

Only approved files are eligible for transfer to remote systems.

## [**Enable File Transfer in RDP Service**](/docs/metadefender-ot-access/2.3.0/knowledge-base/md-core-integration---secure-file-transfer-via-rdp#enable-file-transfer-in-rdp-service)

To allow file transfer:

- Ensure that **File Transfer is enabled** in the target RDP service
- Configure the **shared folder path** on the remote host

For detailed steps, refer to: [MFT Integration – Secure File Transfer via RDP](/docs/metadefender-ot-access/2.3.0/knowledge-base/mft-integration---secure-file-transfer-with-rdp)

## [**Transfer File to Remote Host**](/docs/metadefender-ot-access/2.3.0/knowledge-base/md-core-integration---secure-file-transfer-via-rdp#transfer-file-to-remote-host)

Once the file is approved:

1. Select the desired **RDP service**
2. Choose the approved file from MD Core
3. Initiate the transfer

The file will be securely delivered to the configured shared folder on the remote system.

## [**Verify File on Remote Host**](/docs/metadefender-ot-access/2.3.0/knowledge-base/md-core-integration---secure-file-transfer-via-rdp#verify-file-on-remote-host)

- Access the remote machine
- Navigate to the configured **shared folder**
- Confirm that the file has been successfully transferred
