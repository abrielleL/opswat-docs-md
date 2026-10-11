<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening -->

# Kiosk Hardening

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

All OPSWAT Kiosk appliances ship by default with our **Hardened Image**. For customers who are installing the Kiosk application on their own custom hardware OPSWAT recommends that the following steps to harden the operating system.

## [Auto login](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#auto-login)

If MetaDefender Kiosk is being used on a dedicated system we recommend that the Windows system on the kiosk is configured to auto-login into the account with Administrator privileges that Kiosk will run with. If the Kiosk system is part of a domain additional steps may be required to allow this.

## [User Access Control (UAC)](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#user-access-control-uac)

OPSWAT recommends that UAC is disabled on systems that are being used as dedicated MetaDefender Kiosks. If UAC is not disabled MetaDefender Kiosk's watchdog functionality may not work correctly.

There are two ways to completely disable UAC in Windows:

**By editing the registry**

1. Click **Start** and type `regedit.exe` to open the Registry Editor
2. Navigate to the registry key at **HKEY_LOCAL_MACHINE > SOFTWARE > Microsoft > Windows > CurrentVersion > Policies > System**
3. Set `EnableLUA` to `0`
4. Restart Windows

**By adjusting Local Group Policy settings**

1. Click **Start** and type `gpedit.msc` to open the Group Policy Editor
2. Navigate to **Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options**
3. Right pane is populated with policies, locate the ones for User Access Control and set:

   1. **User Account Control: Only elevate executables that are signed and validated** → *Enabled*
   2. **User Account Control: Switch to the secure desktop when prompting for elevation***→ Disabled*
4. Restart Windows

## [Windows Update](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#windows-update)

Install all patches and updates available through Windows Update. Once all updates are installed, OPSWAT recommends that automatic updates are turned off to prevent system reboots.

1. Navigate to **Start > Control Panel > Windows Update > Change settings**
2. Select **Never check for updates** from the menu
3. Click **Apply** or **OK** and close the dialog box

If turning off automatic updates is not desired, a process must be configured to restart the MetaDefender Kiosk system. We recommend using standard organizational patch practices and tools.

## [Setting the power saving options](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#setting-the-power-saving-options)

Select the maximum performance power saving option.

1. Navigate to **Start > Control Panel > Power Options**
2. Click **Change plan settings**
3. Click **Change advanced power settings**
4. Select **High Performance** from the menu
5. Click **OK**

## [Disabling mouse cursor pointer](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#disabling-mouse-cursor-pointer)

Info

This configuration is optional. Once these steps are taken, there will be no visible mouse pointer.

OPSWAT recommends that mouse cursor points are turned off after MetaDefender Kiosk has been configured. If the system touchscreen configuration software does not have this feature, it can be done manually by following the steps below:

1. Navigate to **Start > Control Panel > Mouse**
2. Click the **Pointers** tab
3. Browse to `C:\Program Files (x86)\OPSWAT\Metadefender Kiosk\Client\blank.cur`
4. Customize each pointer type to the provided blank pointer: `blank.cur`
5. Click **Apply** and close the dialog box.

## [Disabling hotkeys](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#disabling-hotkeys)

By default, the Kiosk will ignore any command that is a combination of Ctrl and another key.

The `Ctrl + Alt + Del` combination is disabled once you launch the Kiosk. When a user presses these keys, it is expected to see a screen with no options displayed.

If you want to disable completely where nothing happens, please follow [how to disable Windows hot keys](https://docs.opswat.com/mdkiosk/operating/disabling-windows-hot-keys).

## [Enable Bitlocker Drive Encryption](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#enable-bitlocker-drive-encryption)

To protect data and prevent unauthorized access, we recommend enabling BitLocker Drive Encryption on the system and data drives to safeguard sensitive information in the event of theft, loss, or unauthorized access.

For detailed configuration steps, please refer to [Enable Bitlocker guide](https://www.opswat.com/docs/mdkiosk/hardened-image/enabling-bitlocker-for-kiosk-hardened-image).

## [Other system hardening configuration](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#other-system-hardening-configuration)

MetaDefender Kiosk does the following system hardening when installed:

- Disables auto-run on all plug-and-play media and drives
- Captures and disables all hotkey combinations such as the `Windows Key`, `Alt+Tab`, etc... when Kiosk is running

## [See also](/docs/mdkiosk/v4.8.6/hardened-image/kiosk-hardening#see-also)

- [System requirements — Security requirements](https://www.opswat.com/docs/mdkiosk/installation/kiosk-system-requirements#security-requirements) for setting a BIOS password, enabling TPM and Secure Boot, and turning on BitLocker encryption.
- [Setting BIOS Password on Kiosk Devices (Dell)](https://www.opswat.com/docs/mdkiosk/hardened-image/setting-bios-password-on-kiosk-devices--dell-) for step-by-step instructions on Dell hardware.
- Additional opt-in hardening controls available from **Settings > System Hardening** in the Kiosk Web Management Console:

  - [Boot Hardening Option](https://www.opswat.com/docs/mdkiosk/hardened-image/boot-hardening-option)
  - [Anti-tamper Hardening Option](https://www.opswat.com/docs/mdkiosk/hardened-image/anti-tamper-hardening-option)
  - [Network Hardening Policies Option](https://www.opswat.com/docs/mdkiosk/hardened-image/network-hardening-policies-option)
  - [Device Location Option](https://www.opswat.com/docs/mdkiosk/hardened-image/device-location-option)
