<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-0-2 -->

# Fend Optical Diode v4.0.2

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Released: 03/08/2024

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-0-2#featureschanges)

1. **Major Update** New web-based configuration interface. To configure the diode, now enter the diode's IP address into your web browser and log in. The default username is "user". The password remains the same. Standalone configuration application will no longer work after upgrade.
2. Upgraded the firmware update process to significantly increase the speed of future firmware updates from 4.0.0 onward (from minutes to seconds)
3. Changed the format of diode backup and restore files to JSON for easier human readability. Note: this breaks backwards compatibility with legacy .vdiode files. Please re-export your backup configurations after upgrading to firmware 4.0.0.
4. Factory restore button now clears user logs and power events in addition to restoring factory settings
5. Increased cellular modem speeds to 1Mbps
6. Added the following new settings:

   1. Added ability for users to change the length of a configuration session from between 10 and 60 minutes.
   2. Added ability to turn off FTP logs
7. Changed the following settings:

   1. Made "passive" the default Data Socket Mode for output side FTP
   2. Moved FTP log directory to output side settings
   3. Removed unsupported "7 data bits" as an option from the RS485 data bits setting
   4. Changed allowable inputs for input side RS485 Modbus RX timeout from 1-32,000ms to 1-20ms
   5. Changed allowable inputs for input side Ethernet Modbus RX/TX timeout from 100 – 25,500 in increments of 100 ms to 1-32,000ms in increments of 1 milliseconds
8. Added the following diagnostic messages:

   1. Added message for receiving an invalid number of bytes in a Modbus response
   2. Added a configuration session start diagnostic message
   3. Added NTP and DNS set by DHCP messages
   4. Added messages for TCP/UDP data received for input and output sides
   5. Added additional MQTT status messages

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-0-2#fixes)

1. Fixed an issue where the FTP error log would not transfer when network lost in streaming mode
2. Fixed an issue where the firmware update in progress status LEDs were not displaying properly on the output side
3. Fixed an issue where the diagnostics message for the input side TCP connection message showed an invalid IP
4. Fixed an issue where Modbus RTU input side was not properly checking the size of the response packet
5. Fixed an issue where the proper LED error code was not being displayed when an ethernet cable is unplugged from the output side in MQTT mode
6. Fixed an issue where Modbus RTU requests would timeout after 500ms even if settings were greater than 500ms.
