<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-doesn-t-cd-dvd-drive-detect-cd-dvds-on-the-kiosk- -->

# Why doesn't CD/DVD drive detect CD/DVDs on the Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to all MetaDefender Kiosk versions

## **Issue**

The kiosk does not detect CD/DVDs inserted into the CD/DVD drive.

## **Possible Causes**

This issue may be caused by one or more of the following:

- CD/DVD media is not allowed in the kiosk workflow configuration.
- The CD/DVD is damaged, unreadable, or unsupported.
- The CD/DVD drive is not receiving power or is not properly connected.
- The USB-to-SATA cable or SATA adapter is faulty.
- The CD/DVD driver is missing, outdated, or corrupted.
- Microsoft Defender Real-Time Protection is interfering with the scan or access process.
- The CD/DVD is detected by Windows, but not by the Kiosk application.

## **Troubleshooting steps**

Please try the following steps:

1. **Check whether Windows can detect the CD/DVD**

   Exit the Kiosk UI, insert the CD/DVD into the CD/DVD drive, and check whether the CD/DVD appears in Windows Explorer.

   - If Windows Explorer detects the CD/DVD, the issue may be related to the Kiosk application or workflow configuration.
   - If Windows Explorer does not detect the CD/DVD, the issue may be related to the CD/DVD, CD/DVD drive, cable, adapter, or driver.
2. **Test with another CD/DVD**

   Try inserting a different CD/DVD to determine whether the issue is specific to one disc.
3. **Test the CD/DVD drive on another computer**

   If possible, connect the CD/DVD drive to another computer and confirm whether the CD/DVD is detected there.
4. **Test the cable and adapter**

   If possible and applicable, use the same USB-to-SATA cable and SATA adapter to connect the CD/DVD drive to another device. This helps confirm whether the cable or adapter is working correctly.
5. **Check the SATA adapter LED**

   If the CD/DVD drive is connected to the kiosk using a USB-to-SATA cable and SATA adapter, check whether the green LED on the adapter is lit.

   - If the LED is lit, the adapter is receiving power.
   - If the LED is not lit, there may be a cable, adapter, or power issue.
6. **Verify the kiosk workflow configuration**

   Confirm that CD/DVD media is allowed in the Kiosk workflow configuration: Going to Kiosk management console (http(s)://Kiosk_IP:8009) > Workflow > Choose the kiosk workflow in question > Media Types > Make sure CD/DVDs are allowed
7. **Temporarily disable Microsoft Defender Real-Time Protection**

   Temporarily disable Microsoft Defender Real-Time Protection and test again.

   After testing, re-enable Real-Time Protection.
8. **Reinstall or update the CD-ROM drivers**

   Reinstall or update the CD-ROM drive drivers from Windows Device Manager, then reboot the kiosk and test again.

## **Next Steps**

If the issue persists after completing the steps above, please collect the kiosk support package and provide the following information to OPSWAT Support:

- Kiosk serial number
- Kiosk version
- Whether Windows Explorer can detect the CD
- Whether the issue occurs with all CDs or only specific CDs
- Whether the adapter LED is lit
- Any recent hardware, driver, OS update or configuration changes

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
