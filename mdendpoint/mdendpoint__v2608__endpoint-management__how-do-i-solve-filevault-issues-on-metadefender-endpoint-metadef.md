<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-solve-filevault-issues-on-metadefender-endpoint-metadef -->

# How do I solve FileVault issues on MetaDefender Endpoint/MetaDefender IT-OT Access devices?

> **Check Your Product:**
>
> This article applies to macOS FileVault, the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on macOS systems.

Users running MetaDefender Endpoint on one or more macOS devices may occasionally see MetaDefender IT-OT Access device compliance warnings/flags related to FileVault encryption.

> **Pro Tips:**
>
> FileVault is a native macOS tool that allows users to easily encrypt or decrypt their hard disks.
>
> - Filevault uses XTS-AES-128 encryption with a 256-bit key to encrypt your startup disk and prevent unauthorized access to any data on it.
> - When FileVault is turned on, the disk will be encrypted and will remain in that state unless Filevault is turned off.
> - Turning FileVault off will decrypt the disk.

This warning/flag is triggered by a device issue and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Encryption**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/dksgaro9l8alq151lxy8v77gcm8nsyo00m8o3e6gs4hi1414302cmcf63i0jbr35.png)

## MetaDefender IT-OT Access Compliance Warning: FileVault - System volume is not encrypted/Device volume data is not encrypted

1. Click on the **Apple** menu in the top left-hand corner of the screen.
2. Navigate to **System Preferences>Security & Privacy**.

![](https://uploads.developerhub.io/prod/2x2P/g7qfb94hazm712qej82yqr1hgfr4o6xc3dp649eile4m37nf6aoso3r2nivrex06.png)

3. Click on **FileVault**.

![](https://uploads.developerhub.io/prod/2x2P/kqk0yowgsthp7zj62qfyqw87dp56ho3dxskdxnvmiar3fk9hy6iym20pvbgejqao.png)

4. Click the **Lock** to open it, then click **Turn on FileVault**.

![](https://uploads.developerhub.io/prod/2x2P/e3zds9u40cslw0c82booo0g8h7xdw7wzguo0x4x9ml2hbcun3jjjef4upy5851c4.png)

5. Select how you want to unlock the disk and reset your password, in case you forget, by checking the appropriate option. Your choices are to:

- **Allow your iCloud account to unlock your disk** - i.e, use your iCloud password.
- **Create a recovery key and not use your iCloud account** - i.e, use a generated recovery key.

![](https://uploads.developerhub.io/prod/2x2P/dcalpagorqq7a4smphv92k35e3kg7p9lrgtxgz2bezzzmyw5vbwt0szqoobmtnd2.png)

6. Your disk will now be encrypted.

> **Pro Tips:**
>
> - The encryption process may take a number of hours and will run in the background while your system is powered on.
> - It is safe to switch your system off and on while this process is underway.
> - New files that are created while the process is underway will also be encrypted.
> - With FileVault encryption enabled, no account will be permitted to log in automatically.
> - Once encrypted, your disk will remain in an encrypted state until FileVault is turned off, at which time a lengthy decryption process will ensue.

![](https://uploads.developerhub.io/prod/2x2P/u9y32o77wc8spkh43prswoqq4gt09zwg0xqhvzqhr65jk9edi0e785fwg4edl1ww.png)

7. Once FileVault encryption has completed, **Restart** your system, using your chosen **Password** method to unlock the disk and finish the process.

![](https://uploads.developerhub.io/prod/2x2P/kamp8ltc3cjga0zrp92hiy1938ts5m6wt00sndlwuwbioe0p5uetbnigef9kh26i.png)

8. Click on the OPSWAT **Tray Icon**, then click the **Recheck** option.

![](https://uploads.developerhub.io/prod/2x2P/vhd1yb8yucw06bf21l0ivwzsdcbv602jm1tkbbkvl8vpo1f8ikr71n1hsqj8ehti.png)

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience macOS FileVault Encryption Issues On Your** **MetaDefender Endpoint/MetaDefender IT-OT Access** **Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
