<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553-- -->

# Why Does MetaDefender NetWall Show “unexpected response: 553–Could not create file” for FTP Transfers (vsftpd)?

**Check Your Version:**

This article applies to all NetWall versions.

## [Overview](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#overview)

In some deployments, the transfer log may show on RED side:

Receive Status = success, Send Status = error, and Error = "unexpected response: 553-Could not create file."

This indicates the destination FTP server rejected the upload.

## [Symptoms](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#symptoms)

- Error field contains: “unexpected response: 553-Could not create file.”
- Failures correlate with deep directory paths (many nested folders).
- Uploading a single file to a top-level folder (e.g., /ftp_data/incoming) succeeds.
- Uploading a folder or large repository (requiring many subfolder creations) fails.

## [Cause](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#cause)

The 553 response comes from the destination FTP server (vsftpd), not from NetWall. During folder uploads, the FTP client must create directories with MKD and then upload files with STOR. If the FTP account used by NetWall lacks permission to create or write within the target path, vsftpd returns 553 and the RED-side transfer fails.

- Insufficient file system permissions for the FTP user (cannot MKD or STOR in target path).
- Parent directory exists but user cannot create subfolders (group/other permissions too restrictive).
- vsftpd write operations disabled or restricted for the logged-in user.
- Incorrect, non-existent, or policy-restricted destination path.

Key insight: If single-file uploads to a shallow directory succeed but folder uploads fail, focus on MKD (directory creation) permissions and vsftpd write settings.

## [Resolution Steps](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#resolution-steps)

### [1) Verify directory ownership, group, and permissions](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#1-verify-directory-ownership-group-and-permissions)

On the FTP server, inspect the target directories and the FTP user identity:

ls -ld /ftp_data /ftp_data/incoming
ls -ld /ftp_data/incoming/repo /ftp_data/incoming/repo/deb
id <ftp_username>

Requirements for creating subfolders and files under the target path:

- The NetWall FTP user should be the owner of the directory, or belong to the owning group with write permission.
- If permissions are 775, only owner and group can create subfolders; users treated as “other” cannot.

Example fixes:

sudo chown -R <ftp_username>:<ftp_group> /ftp_data/incoming
sudo chmod 775 /ftp_data/incoming
sudo chmod g+s /ftp_data/incoming # ensure group inheritance on new subfolders
### [2) Confirm vsftpd write settings](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#2-confirm-vsftpd-write-settings)

Open and review the vsftpd configuration:

sudo nano /etc/vsftpd.conf

Ensure write and directory creation are allowed, and verify default permissions for new items:

write_enable=YES
local_umask=022

Apply changes:

sudo systemctl restart vsftpd
### [3) Test with the same FTP credentials](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#3-test-with-the-same-ftp-credentials)

From a test client, log in using the exact credentials configured on NetWall RED and validate directory creation and upload:

mkdir /ftp_data/incoming/test_from_ftp
# then upload a small test file into that folder using your FTP client

If manual testing fails or returns 553, the problem is confirmed on the FTP server side (permissions or configuration).

### [4) Re-run the transfer from NetWall](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#4-re-run-the-transfer-from-netwall)

- Trigger the same file or folder transfer again in NetWall.
- Confirm Receive Status = success (BLUE) and Send Status = success (RED).
- Verify the full directory structure and files exist on the FTP server.

## [Prevention and Best Practices](/docs/netwalldiode/v1.14.0/knowledge-base/why-does-metadefender-netwall-show----unexpected-response--553--#prevention-and-best-practices)

- Use a dedicated FTP system user and group for NetWall transfers; align directory ownership to that account and group.
- Apply directory setgid (g+s) on the top-level target to keep group ownership consistent in nested folders.
- Document and routinely verify vsftpd write-related settings after OS or package updates.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

MetaDefender
