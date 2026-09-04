<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v2-0-3 -->

# Fend Optical Diode v2.0.3

Released: 08/18/2022

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v2-0-3#featureschanges)

1. Added new non-buffered FTP/S streaming feature (stream files of unlimited size over FTP)
2. Increased number of files supported in buffered mode FTP/S
3. Added secure FTPS option to the input side of the diode
4. Added new factory restore feature. Hold reset button for 10 second to reset the diode to default to factory settings (will overwrite current settings)
5. Added new configuration port timeout settings. If enabled, requires physical power off/on to access configuration login
6. Added ability to turn power loss warning feature on/off.
7. Added ability to view and clear power loss events in Configuration Tool
8. Improved Configuration Tool password change feature layout and functionality
9. Increased the speed of Modbus passthrough, now supports 40,000 registers @ 1 second polling intervals

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v2-0-3#fixes)

1. Fixed an issue with power loss LEDs not clearing properly
2. Fixed issue with "Failed to Connect to Destination" LED pattern now appearing in some cases
3. Fixed an issue with diode FTP server IP address not displaying correctly in the Configuration Tool when in DHCP mode
4. Fixed an issue where FTP commands would be re-sent unnecessarily at the beginning of an FTP transfer
5. Set TCP/IP as the default for connecting to the diode in the Configuration Tool connection settings
6. Fixed an issue with loading large certificates for secure protocols
7. Fixed an issue with invalid FTP port range settings causing the diode to reboot
8. Fixed an issue with setting min and max configuration values
