<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve-slow-usb-detection-on-kiosk-tower-with-floppy-dri -->

# How to resolve slow USB Detection on Kiosk Tower with Floppy Drive?

## [Symptom](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve-slow-usb-detection-on-kiosk-tower-with-floppy-dri#symptom)

In MetaDefender Kiosk versions 4.7.4 and prior, systems running MetaDefender Kiosk software, including the Kiosk Tower or devices with a connected floppy drive, encounter substantial delays in USB device detection.

## [Cause](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve-slow-usb-detection-on-kiosk-tower-with-floppy-dri#cause)

By design, the Kiosk scans through all available drives during media detection. When a floppy drive is connected, the system may hang while attempting to detect it, significantly slowing down USB detection.

## [Solution](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve-slow-usb-detection-on-kiosk-tower-with-floppy-dri#solution)

Upgrade to MetaDefender Kiosk version 4.7.5, which includes improvements to the USB detection process. Refer to [Release Notes - MetaDefender Kiosk Windows](https://www.opswat.com/docs/mdkiosk/release-notes) for details. After upgrading, restart the system to apply the changes. Be aware that the first restart may take longer if a floppy drive is connected.

## [Notes](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-resolve-slow-usb-detection-on-kiosk-tower-with-floppy-dri#notes)

- This issue is specific to devices with a connected floppy drive, such as the Kiosk Tower.
- A system restart is required after upgrading to Kiosk 4.7.5 to apply the changes.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
