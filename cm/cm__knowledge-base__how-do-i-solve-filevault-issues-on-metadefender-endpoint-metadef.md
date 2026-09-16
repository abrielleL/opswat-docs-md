<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-filevault-issues-on-metadefender-endpoint-metadef -->

# How do I solve FileVault issues on MetaDefender Endpoint/My OPSWAT Central Management devices?

> **Check Your Product:**
>
> This article applies to macOS FileVault, the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on macOS systems.

Users running MetaDefender Endpoint on one or more macOS devices may occasionally see My OPSWAT Central Management device compliance warnings/flags related to FileVault encryption.

> **Pro Tip:**
>
> FileVault is a native macOS tool that allows users to easily encrypt or decrypt their hard disks.
>
> - Filevault uses XTS-AES-128 encryption with a 256-bit key to encrypt your startup disk and prevent unauthorized access to any data on it.
> - When FileVault is turned on, the disk will be encrypted and will remain in that state unless Filevault is turned off.
> - Turning FileVault off will decrypt the disk.

This warning/flag is triggered by a device issue and will appear under **My OPSWAT Central Management** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Encryption**, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/xddrllouh0a430v03gda4mkfzm5esdq4wkhukaxfceinxy9fqkz5q5ix6g35tzpl.png)

## My OPSWAT Central Management Compliance Warning: FileVault - System volume is not encrypted/Device volume data is not encrypted

1. Click on the **Apple** menu in the top left-hand corner of the screen.
2. Navigate to **System Preferences>Security & Privacy**.

![](https://uploads.developerhub.io/prod/1yda/oq3s5zgym24fuzz6knu8f717pz5fl09gab3jpnvi6a96wnux9ud7akqii35up31d.png)

3. Click on **FileVault**.

![](https://uploads.developerhub.io/prod/1yda/zd9ffp5kyahi5m0b7lo182sskw38a7bgjf6hbdiw75k5rz3hwkf4dognf4x8omvb.png)

4. Click the **Lock** to open it, then click **Turn on FileVault**.

![](https://uploads.developerhub.io/prod/1yda/ta4vg8bzurd14apn8741kbz1f64wvp7rz93b0yyl959ppqoyzm9zuc21e6jnqe0d.png)

5. Select how you want to unlock the disk and reset your password, in case you forget, by checking the appropriate option. Your choices are to:

- **Allow your iCloud account to unlock your disk** - i.e, use your iCloud password.
- **Create a recovery key and not use your iCloud account** - i.e, use a generated recovery key.

![](https://uploads.developerhub.io/prod/1yda/maovdazxjuxvbfvvrx65ncde5xgdl5w3pt9hs56gj1p9bwel0nayrxifyunuhups.png)

6. Your disk will now be encrypted.

> **Pro Tip:**
>
> - The encryption process may take a number of hours and will run in the background while your system is powered on.
> - It is safe to switch your system off and on while this process is underway.
> - New files that are created while the process is underway will also be encrypted.
> - With FileVault encryption enabled, no account will be permitted to log in automatically.
> - Once encrypted, your disk will remain in an encrypted state until FileVault is turned off, at which time a lengthy decryption process will ensue.

![](https://uploads.developerhub.io/prod/1yda/315djlavy6o8rvgwhhx53p7wyucn95q4a874u5cf5tky59y36jogtjrf5i2nzekq.png)

7. Once FileVault encryption has completed, **Restart** your system, using your chosen **Password** method to unlock the disk and finish the process.

![](https://uploads.developerhub.io/prod/1yda/4yayhljbgpa57lhvsw8oowy62khbtojgbsx4c3k3gostxlon9clmh491pdwekecr.png)

8. Click on the OPSWAT **Tray Icon**, then click the **Recheck** option.

![](https://uploads.developerhub.io/prod/1yda/goq17lcwtb07ouoi9hl16epxjrjw56a97y8y1c1ggo7v769jm6sotlixpns6r3xq.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience macOS FileVault Encryption Issues On Your** **MetaDefender Endpoint/My OPSWAT Central Management Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
