<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices- -->

# Why is the Kiosk not detecting devices?

If your Kiosk is not detecting devices, several factors may be causing the issue. Below are common causes and their potential solutions.

### [**Windows Defender Real-Time Protection**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#windows-defender-real-time-protection)

Windows Defender may block the Kiosk application from recognizing USB devices. Try disabling real-time protection using a Group Policy Object (GPO) to see if it resolves the issue.

### [**Malfunctioning USB Port or Device**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#malfunctioning-usb-port-or-device)

A faulty USB port or an incompatible USB device might prevent detection. Test different ports or devices to identify the issue.

### [**WMI Service Failure**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#wmi-service-failure)

The Windows Management Instrumentation (WMI) service is crucial for detecting USB devices. If this service fails, the Kiosk may not recognize devices. Reinstalling the operating system and Kiosk software has resolved this issue in some cases.

### [**Driver Conflicts**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#driver-conflicts)

A connected floppy disk drive without a disk can create driver conflicts, leading to detection failures. Disabling or disconnecting such devices may resolve the issue.

### [**Software or Hardware Glitch**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#software-or-hardware-glitch)

Temporary software or hardware glitches may disrupt USB detection. Restart the Kiosk device and its services to see if the issue resolves.

### [**USB Drivers or Windows Issues**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#usb-drivers-or-windows-issues)

Outdated or corrupted USB drivers can interfere with detection. Updating or reinstalling USB drivers, or reimaging the Kiosk, can resolve the issue.

### [**Event Handling in Windows**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#event-handling-in-windows)

Windows event message handling issues may prevent proper USB detection. Upgrading the Kiosk application or reimaging the device could resolve this.

### [**Device Insertion Timing**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#device-insertion-timing)

All external USB devices, such as SD card readers and floppy disk drives, should be connected before starting the MetaDefender Kiosk application. Otherwise, they may not be recognized.

### [**Unsupported Remote Operation**](/docs/mdkiosk/v4.8.5/knowledge-base/why-is-the-kiosk-not-detecting-devices-#unsupported-remote-operation)

The Kiosk is designed for local use. Running it in a remote desktop session is unsupported and may result in detection failures.

By following these troubleshooting steps, you should be able to identify and resolve the issue preventing the Kiosk from detecting devices. If problems persist, consider reaching out to support for further assistance.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
