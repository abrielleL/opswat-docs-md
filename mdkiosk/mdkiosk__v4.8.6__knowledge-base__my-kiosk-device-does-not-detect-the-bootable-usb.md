<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/my-kiosk-device-does-not-detect-the-bootable-usb -->

# My Kiosk device does not detect the bootable USB

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Issue](/docs/mdkiosk/v4.8.6/knowledge-base/my-kiosk-device-does-not-detect-the-bootable-usb#issue)

I followed the KB ([link](https://www.opswat.com/docs/mdkiosk/hardened-image/guideline---deploying-kiosk-hardened-image)) to create a bootable USB for deploying the Kiosk Hardened Image. However, even with the USB inserted, the boot menu does not display the USB as a boot option

### [Possible causes and solutions](/docs/mdkiosk/v4.8.6/knowledge-base/my-kiosk-device-does-not-detect-the-bootable-usb#possible-causes-and-solutions)

Besides verifying that the USB is not faulty and that the bootable partition was successfully created by following the KB ([link](https://www.opswat.com/docs/mdkiosk/hardened-image/guideline---deploying-kiosk-hardened-image)), please ensure that the **USB boot option is enabled**.

By default, Kiosk devices (Kiosk Tower, Desktop, Mobile, and Mini) have the USB boot option disabled for security reasons. To re-enable USB boot support, follow these steps:

- While the device is starting up, keep pressing F12 to open the Boot Menu and select BIOS Setup
- Navigate to **Integrated Device** > **USB/Thunderbolt Configuration**
- Enable **"Enable USB Boot Support"**

Disable USB Boot to enhance security

After completing the Kiosk Hardened Image deployment, it is recommended to disable USB Boot again to enhance security.

Support

If Further Assistance is required, please proceed to log a support case or chatting with our support engineer.
