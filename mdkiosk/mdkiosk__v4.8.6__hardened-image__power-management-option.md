<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/hardened-image/power-management-option -->

# Power Management Option

View as Markdown Ask ChatGPT about this page Ask Claude about this page
# [Power Management Option](/docs/mdkiosk/v4.8.6/hardened-image/power-management-option#power-management-option)

MetaDefender Kiosk can automatically power a device on or off on a schedule you define, so a device can start its day and shut down again without anyone on site pressing a button. This is useful for locations that run on a predictable schedule — for example, powering down every evening and back on before the next business day.

Available starting in Kiosk 4.8.0.

## [Prerequisites](/docs/mdkiosk/v4.8.6/hardened-image/power-management-option#prerequisites)

- Automatically powering the device **off** on a schedule works on all Kiosk hardware and software editions.
- Automatically powering the device **on** on a schedule is available only on supported Dell-based Kiosk hardware models. On other hardware, this option is unavailable.
- If the device's BIOS is protected with a BIOS password, you'll need that password to save changes to the power-on schedule.

## [Configuring Power Management](/docs/mdkiosk/v4.8.6/hardened-image/power-management-option#configuring-power-management)

1. Sign in to the Kiosk Web Management Console as an administrator.
2. Navigate to **Settings > System Hardening**.
3. Expand the **Power management** section.
4. To schedule automatic power-on (Dell hardware only): turn on **Enable Auto Power On**, then set a Daily or Weekly schedule and time. If your device's BIOS is password-protected, enter the BIOS password.
5. To schedule automatic power-off: turn on **Enable Auto Power Off**, then set a Daily or Weekly schedule and time.
6. Click **Save Updates**.

Both schedules can be used independently or together. For a Weekly schedule, select at least one day of the week.

> **Note:** The first time you turn on Auto Power Off and save, the scheduled shutdown may not occur on its very first scheduled run. If this happens, open the Power management settings and save the configuration again — subsequent scheduled shutdowns then occur as expected. This can also happen the first time a configuration backup with Auto Power Off enabled is restored to a device.

## [Example](/docs/mdkiosk/v4.8.6/hardened-image/power-management-option#example)

A site wants its kiosk running only during business hours, without staff needing to manually power it on or off:

1. An administrator turns on **Enable Auto Power Off** with a Daily schedule set for 7:00 PM.
2. On Dell hardware, the administrator also turns on **Enable Auto Power On** with a Daily schedule set for 7:00 AM.
3. Each evening, the kiosk shuts itself down at 7:00 PM. Each morning, it powers back on at 7:00 AM — no one needs to be on site to do either.

## [Managing Power Management Settings Across Multiple Devices](/docs/mdkiosk/v4.8.6/hardened-image/power-management-option#managing-power-management-settings-across-multiple-devices)

If your Kiosk devices are enrolled in Central Management, Auto Power On and Auto Power Off can be configured and applied centrally across your fleet, rather than one device at a time.

> **Related:** Kiosk also offers a Wake-on-AC option in the same Power management section, which automatically powers a supported device back on whenever AC power is restored after an outage — independent of any schedule. See the Wake-on-AC documentation for details. *(Editorial note, not for the live page yet: the Wake-on-AC draft's DevHub publish status is unconfirmed as of this upload — replace this note with an actual link once that page is confirmed live.)*
