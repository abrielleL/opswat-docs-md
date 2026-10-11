<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/wake-on-ac-option -->

# Wake-on-AC Option

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Kiosk can automatically power a supported device back on whenever AC power is restored after an outage — for example, after a brief power cut or a facility maintenance shutdown — without anyone needing to press the physical power button. This is especially useful for kiosks in unattended or hard-to-reach locations, such as lobbies, factory floors, or vessels, where a manual restart isn't always practical. Available starting in Kiosk 4.8.4.

## [Prerequisites](/docs/mdkiosk/v4.8.6/hardened-image/wake-on-ac-option#prerequisites)

- Kiosk 4.8.4 or later.
- This option is available only on supported Dell-based Kiosk hardware models. On other hardware, the option is unavailable and the Console will indicate that it isn't supported on the current device.
- If the device's BIOS is protected with a BIOS password, you will need that password to save changes to this setting.

## [Configuring the Wake-on-AC Option](/docs/mdkiosk/v4.8.6/hardened-image/wake-on-ac-option#configuring-the-wake-on-ac-option)

1. Sign in to the Kiosk Web Management Console as an administrator.
2. Navigate to **Settings > System Hardening**.
3. Expand the **Power management** section.
4. Turn on **Enable Wake On AC**.
5. If your device's BIOS is password-protected, enter the BIOS password when prompted.
6. Click **Save Updates**.

Once saved, the Console reports whether the setting was successfully applied to the device. Turning this option on or off does not require restarting the Kiosk.

Note

If saving fails — for example, because the BIOS password was missing or entered incorrectly — an error message appears, and the setting is **not** applied to the device. In this situation, the on-screen switch may still appear to show the new position even though the change did not take effect. If you see an error message after saving, treat the message as the accurate result rather than the switch's position, and try again with the correct BIOS password.

Note

If you reinstall the Kiosk application on a device that already has Wake-on-AC enabled at the hardware level, the Console may briefly show an out-of-date status. This corrects itself automatically the next time the Kiosk service starts, at which point the Console's displayed status matches the device's actual configuration.

## [Example](/docs/mdkiosk/v4.8.6/hardened-image/wake-on-ac-option#example)

A kiosk is deployed in a location without on-site IT staff, such as a ship or a remote facility. After enabling Wake-on-AC:

1. The site experiences a power outage.
2. When power is restored, the kiosk powers itself back on automatically — no one needs to be physically present to press the power button.

## [Managing Wake-on-AC Across Multiple Devices](/docs/mdkiosk/v4.8.6/hardened-image/wake-on-ac-option#managing-wake-on-ac-across-multiple-devices)

If your Kiosk devices are enrolled in Central Management, this option can also be configured and applied centrally, and the applied status is reported back for each enrolled device — so administrators can confirm the setting took effect without having to check each device individually.
