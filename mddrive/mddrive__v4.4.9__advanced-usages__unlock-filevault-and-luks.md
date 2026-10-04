<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/advanced-usages/unlock-filevault-and-luks -->

# Unlock FileVault and LUKS

OPSWAT MetaDefender Drive enables macOS and Linux users with FileVault and LUKS disk encryption to run a scan on their protected drives. The decryption process only requires the user to enter the passphrase when prompted.

## [Unlock and Mount FileVault and LUKS Encrypted Disks](/docs/mddrive/v4.4.9/advanced-usages/unlock-filevault-and-luks#unlock-and-mount-filevault-and-luks-encrypted-disks)

Before performing a scan, some of the target system disks might show as **Unmounted** on the **Disk Status and Remediation** page. MetaDefender Drive detects if those disks are unmounted due to encryption and the type of encryption. If your disks are encrypted using FileVault or LUKS, you can unlock them by entering a password.

### [Unlock FileVault using a Password](/docs/mddrive/v4.4.9/advanced-usages/unlock-filevault-and-luks#unlock-filevault-using-a-password)

1. Select the disk you intend to unlock, and click **Unlock Disk**.
2. In the window, Confirm the encryption type (FileVault in this case), and enter the password, then click **Unlock**:

Unlocking a FileVault encrypted disk using a password

### [Unlock LUKS using a Password](/docs/mddrive/v4.4.9/advanced-usages/unlock-filevault-and-luks#unlock-luks-using-a-password)

1. Select the disk you intend to unlock, and click **Unlock Drive**.
2. In the window, Confirm the encryption type (LUKS in this case), and enter the password, then click **Unlock**:

Unlocking a LUKS encrypted disk using a password

LUKS Decryption Memory Requirements

The LUKS decryption process requires high memory usage. It is required that the target device to have at least 1.5GB of RAM available for the LUKS decryption to work as expected.

.
