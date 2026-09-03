<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-solve-filevault-issues-on-opswat-client-metaaccess-devi -->

# How do I solve FileVault issues on MetaDefender Endpoint/MetaDefender IT Access devices?

This article applies to macOS FileVault, the current MetaDefender IT Access Console and API, and all MetaDefender Endpoint releases deployed on macOS systems.

Users running MetaDefender Endpoint on one or more macOS devices may occasionally see MetaDefender IT Access device compliance warnings/flags related to FileVault encryption.

Pro Tip:

FileVault is a native macOS tool that allows users to easily encrypt or decrypt their hard disks.

- Filevault uses XTS-AES-128 encryption with a 256-bit key to encrypt your startup disk and prevent unauthorized access to any data on it.
- When FileVault is turned on, the disk will be encrypted and will remain in that state unless Filevault is turned off.
- Turning FileVault off will decrypt the disk.

This warning/flag is triggered by a device issue and will appear under **MetaDefender IT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Encryption**, as illustrated below.

## MetaDefender IT Access Compliance Warning: FileVault - System volume is not encrypted/Device volume data is not encrypted

1. Click on the **Apple** menu in the top left-hand corner of the screen.
2. Navigate to **System Preferences>Security & Privacy**.

3. Click on **FileVault**.

4. Click the **Lock** to open it, then click **Turn on FileVault**.

5. Select how you want to unlock the disk and reset your password, in case you forget, by checking the appropriate option. Your choices are to:

- **Allow your iCloud account to unlock your disk** - i.e, use your iCloud password.
- **Create a recovery key and not use your iCloud account** - i.e, use a generated recovery key.

6. Your disk will now be encrypted.

Pro Tip:

- The encryption process may take a number of hours and will run in the background while your system is powered on.
- It is safe to switch your system off and on while this process is underway.
- New files that are created while the process is underway will also be encrypted.
- With FileVault encryption enabled, no account will be permitted to log in automatically.
- Once encrypted, your disk will remain in an encrypted state until FileVault is turned off, at which time a lengthy decryption process will ensue.

7. Once FileVault encryption has completed, **Restart** your system, using your chosen **Password** method to unlock the disk and finish the process.

8. Click on the OPSWAT **Tray Icon**, then click the **Recheck** option.

Support:

If you have followed the instructions above but **Continue To Experience macOS FileVault Encryption Issues On Your** **MetaDefender Endpoint/MetaDefender IT Access** **Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
