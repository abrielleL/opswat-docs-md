<!-- source: https://www.opswat.com/docs/mdkiosk-linux/troubleshooting/troubleshooting -->

# Troubleshooting

## [Support Package](/docs/mdkiosk-linux/troubleshooting/troubleshooting#support-package)

A support package contains essential information regarding the Kiosk system operation. For any issues encountered with the Kiosk, please generate a support package and provide it when reaching out to Customer Support.

**Creating the package**

1. Prepare a USB with a folder named `Gather OPSWAT support package` at the root directory
2. Insert the USB at any time after the UI is up (after the splash screen and not during a running scan)

   1. The splash screen is the page displayed when the Kiosk is booting up and the text `OPSWAT MetaDefender Kiosk` is displayed in the center of the screen.
3. Wait at least 5 minutes or (if your USB has an activity light) wait until the USB activity light stops flashing
4. Unplug the USB

Successful package creation will generate 2 files in the `Gather OPSWAT support package` directory:

- `MK5-SupportPackage` - the full support package
- `MK5-SupportPackage.sha256` - hash of the support package to ensure completeness

If any file is missing or the hash does not match the package, reattempt the process again until successful.

Warning

It is recommended that the USB used to retrieve a support package be formatted to anything other than FAT32.

In rare cases, a support package may grow larger than 4GB and may result in failure to obtain the package due to exceeding the file size limitation of FAT32.

---

## [System Reset](/docs/mdkiosk-linux/troubleshooting/troubleshooting#system-reset)

Warning

Performing System Reset will revert the Kiosk back to default settings.

License, network settings, and the connection to MyOPSWAT / Central Management will be wiped out.

To reset Kiosk back to allow reconfiguration:

- Hold down the power button to shutdown the system
- Connect a keyboard to the system
- Turn the system on
- Hold down `LEFT-SHIFT + LEFT-ALT + F7` (for version 5.3.2 and older use `LEFT-SHIFT + LEFT-ALT + F9` ) when the Kiosk text is displayed (the splash screen):

splash screen

- Continue to hold down the keys until the system reboots itself, then disconnect the keyboard
- Upon a successful reboot, the language selection menu will be displayed

Info

Do not hold down the `Right-Shift` or `Right-Alt` keys.

Do not hold down the keys before the splash screen is displayed.

Failure to adhere to the specified process will not result in a successful reset.

---

## [Soft Reset](/docs/mdkiosk-linux/troubleshooting/troubleshooting#soft-reset)

A soft reset allows the Kiosk to refresh the internal software while maintaining all existing configuration.

To softly reset the Kiosk:

- Hold down the power button to shutdown the system
- Connect a keyboard to the system
- Turn the system on
- Hold down `LEFT-SHIFT + LEFT-ALT + F6` when the Kiosk text is displayed on the splash screen
- Continue to hold down the keys until the system reboots itself
- Upon a successful reboot, the Kiosk will begin its startup process and become operational

---

## [License](/docs/mdkiosk-linux/troubleshooting/troubleshooting#license)

When connecting Kiosk to a management server, it will do an initial validation check on the volume license obtained.

If there is an issue, a drop down error will be displayed:

MetaDefender Kiosk Linux license verification unsuccessful

The MetaDefender Kiosk Linux license has expired or was revoked

Once onboarding begins, a full screen error may be displayed as follows:

Issue with license - Failed to activate license

Once properly onboarded, if Kiosk detects a license change and the validation check fails, a full screen error will be displayed. This error will be dismissed once the license issue is fixed.

Issue with license - MetaDefender Kiosk Linux license verification unsuccessful

Issue with license - Failed to activate engines, license is expired

To check that your volume license is not expired, navigate to the Settings section of your My OPSWAT or Central Management instance. In the license tab, check the Expired date listed. Also check the number of monitored instances as compared to the limit your license allows.

My OPSWAT will provide information about the volume license expiration and kiosk limit as shown.

OPSWAT Central Management will provide information about the volume license expiration and kiosk limit as shown.

If your license is expired or does not support the number of Kiosks your organization requires, reach out to a representative at OPSWAT. Visit [opswat.com/support](https://www.opswat.com/support) for more information.

Verification errors may be shown if the license file has been modified. Review the license file and ensure line endings are set to Unix (`LF`) style and have not been accidentally modified to Windows (`CR LF`) style.

If there are no notable issues with the license, a [support package](https://docs.opswat.com/mdkiosk-linux/troubleshooting/troubleshooting#support-package) will need to be provided.

---

## [MetaDefender Managed File Transfer Connection](/docs/mdkiosk-linux/troubleshooting/troubleshooting#metadefender-managed-file-transfer-connection)

When enabling the `Scan and Copy to MetaDefender Managed File Transfer` workflow, there are two areas to ensure the configuration was successful.

For any failure cases, check the Kiosk's MFT configuration:

- Ensure the URL is correctly typed
- Kiosk has access to the URL
- The apikey has admin permissions
- The apikey is not expired

**Kiosk Linux dashboard in Central Management**

In the management server, `Dashboard -> MetaDefender Kiosk Linux`, in the Resources column that displays the connected instances, the system indicator will continue to show `Optimized` if connection was successful or `Not Good` if connection failed.

**Kiosk Info display**

Touch the `OPSWAT MetaDefender Kiosk` logo at the bottom-middle of the screen. A window will display the details of the MFT connection. An error message will be displayed if the system cannot connect to MFT. If the connection is successful, a product version will be displayed.

For a direct connection to Managed File Transfer, `MetaDefender Managed File Transfer Version` will be displayed:

If a MetaDefender NetWall is detected, the NetWall version will be displayed:

---

## [Integrity Check](/docs/mdkiosk-linux/troubleshooting/troubleshooting#integrity-check)

For system protection, Kiosk can detect if it is running on unapproved hardware or the hardware has been modified either internally or externally.

At system start, Kiosk will perform a system integrity check. If any violation is detected the splash screen will show:

Integrity Check Violation

Different resolutions can be taken for each case of violation:

- **Unapproved hardware** - capture a [Support Package](https://docs.opswat.com/mdkiosk-linux/troubleshooting/troubleshooting#support-package) and contact [OPSWAT support](https://www.opswat.com/support) for next steps to take
- **Internal hardware modification** - unapproved internal modifications are not allowed, un-do the changes made
- **External hardware modification** - power off the system and ensure hardware (keyboard, USB, etc...) is disconnected when powering back on

After system startup, if Kiosk remains in a violated state, the screensaver will be replaced with this message:

This system is unapproved to run Kiosk

If it is evident that there has been no internal or external modifications or there is no clear understanding why, then a support package will need to be provided as soon as possible.

---

## [Network Setting Input](/docs/mdkiosk-linux/troubleshooting/troubleshooting#network-setting-input)

In rare circumstances, when configuring the network setting during onboarding, the on-screen keyboard will not display due to continual switching of input fields.

When this is encountered, close all networking screens and navigate back out the onboarding page.

Afterwards, navigate back to networking settings and the on-screen keyboard will display again to allow input.

---

## [Memory Card Limitation](/docs/mdkiosk-linux/troubleshooting/troubleshooting#memory-card-limitation)

Info

Only applies to the Mini form factor

Memory Card Limitation: Memory card detected. Additional memory card insert is not supported.

When inserting an SD Card or TF card, this hardware limitation warning will be displayed.

A subsequent memory card insert may not be detected.
