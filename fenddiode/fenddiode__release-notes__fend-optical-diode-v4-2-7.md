<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-2-7 -->

# Fend Optical Diode v4.2.7

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Released: 05/31/2026

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-7#featureschanges)

1. Added TLS 1.3 support
2. Added the ability for users to sync the real-time clock (RTC) time on the diode via the configuration interface.
3. Added a Target Modbus Port field to the Modbus Device configuration panel. This allows the diode to connect to a Modbus device on a TCP port other than the default of 502.

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-7#fixes)

1. Fixed an issue causing some characters in text fields to be rejected in the configuration web UI.
2. Fixed an issue that could cause the configuration web UI to fail to communicate with the diode during a session.
3. Fixed an issue with configuration session handling when navigating away from the tab or page.
4. Fixed the reboot LED pattern.
5. Fixed the cellular connection mode LED pattern (now blinking green = connecting, solid green = connected).
6. Fixed an issue that could cause a user's static NTP server to be overwritten when in DHCP mode.
