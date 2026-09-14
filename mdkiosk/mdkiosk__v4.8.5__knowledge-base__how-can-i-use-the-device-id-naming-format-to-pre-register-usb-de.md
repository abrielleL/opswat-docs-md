<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-can-i-use-the-device-id-naming-format-to-pre-register-usb-de -->

# How can I use the Device ID naming format to pre-register USB devices in the USB Scanning Allowlist?

**Check Your Version:**

This article applies to MetaDefender Kiosk of all versions.

Administrators may want to pre-register USB devices in the **USB Scanning Allowlist** before physically connecting them to the kiosk. This can be achieved by using **substring** or **regular expression (regex)** matching based on the USB device’s naming format.

The kiosk identifies USB devices following the Windows registry format described in Microsoft documentation:
🔗 [USB Device Registry Entries - Windows drivers | Microsoft Learn](https://learn.microsoft.com/en-us/windows-hardware/drivers/usbcon/usb-device-specific-registry-settings)

The general format is as follows:

`USBSTOR\DISK&VEN_<Vendor>&PROD_<Product>&REV_<Firmware>\<Serial>`

**Example Device ID:**

`USBSTOR\DISK&VEN_GENERAL&PROD_UDISK&REV_5.00\208&0`

Device IDs can be obtained from the **Session History** page after a USB device has been scanned, or from the **Windows registry** on another computer where the USB has been connected.

If the device has not yet been inserted into the kiosk, you can still pre-register it by using part of the Device ID string (substring match) or a regular expression pattern that matches multiple possible variants.

### [**Using Substring Match**](/docs/mdkiosk/v4.8.5/knowledge-base/how-can-i-use-the-device-id-naming-format-to-pre-register-usb-de#using-substring-match)

If you want to allow all USB drives from the same vendor regardless of the serial number or firmware version, you can add the following substring to the allowlist:

`USBSTOR\DISK&VEN_GENERAL&PROD_UDISK`

This substring matches any USB device whose Device ID contains that sequence, such as:

- `USBSTOR\DISK&VEN_GENERAL&PROD_UDISK&REV_5.00\208&0`
- `USBSTOR\DISK&VEN_GENERAL&PROD_UDISK&REV_5.01\336&0`

### [**Using Regular Expression Match**](/docs/mdkiosk/v4.8.5/knowledge-base/how-can-i-use-the-device-id-naming-format-to-pre-register-usb-de#using-regular-expression-match)

Regular expressions can be used for more flexible matching across firmware versions or serial number formats.
For example, the following regex pattern allows all firmware revisions under the same vendor and product:

`USBSTOR\\DISK&VEN_GENERAL&PROD_UDISK&REV_\d+\.\d+\\`

This matches Device IDs such as:

- `USBSTOR\DISK&VEN_GENERAL&PROD_UDISK&REV_5.00\208&0`
- `USBSTOR\DISK&VEN_GENERAL&PROD_UDISK&REV_6.01\402&1`

### [**Recommendations**](/docs/mdkiosk/v4.8.5/knowledge-base/how-can-i-use-the-device-id-naming-format-to-pre-register-usb-de#recommendations)

- Use **substring match** for simple vendor or product-based rules.
- Use **regular expressions** when you need to account for multiple firmware versions or serial formats.
- Confirm the actual Device ID format from session history or registry data before finalizing the allowlist entry.

**Support:**
If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).
