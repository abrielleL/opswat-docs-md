<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-0-3 -->

# Fend Optical Diode v4.0.3

Released: 03/29/2024

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-0-3#fixes)

1. Fixed a UI issue where the user could input a Modbus register count in increments that were not compatible with the selected data type.
2. Added a UI warning that initiating a firmware update will cause any unsaved changes to settings to be lost.
3. Added a UI warning if communication with diode fails or is lost during a session.
4. Added a UI warning about the implications of changing the input side IP address from static to DHCP.
5. Fixed an issue where rebooting only the output side of the diode while data was streaming from the input side could cause the output side to keep rebooting until the input side was also powered down. This no longer happens.
6. Fixed an issue in the BACnet MSTCP JSON formatting.
