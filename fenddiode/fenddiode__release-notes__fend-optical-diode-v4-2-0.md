<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-2-0 -->

# Fend Optical Diode v4.2.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Released: 09/01/2024

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-0#featureschanges)

1. Improved Modbus functionality:

   1. Configuration now uses function code + register address format
   2. Expanded register ranges. Can now address all 65,535 registers per function code (up from 10,000)
   3. Increased register entry limit per group from 125 to 65,535. Now you can configure large contiguous register blocks in a single entry!
   4. Function codes 1 and 2 can now poll 2000 coils per message
   5. Added Modbus unit ID remapping. Map Modbus IDs from input devices to different Modbus IDs on the output side of the diode.
   6. Total available groups now shared across all devices for more flexibility. Increased the maximum number of groups to 500 for Modbus TCP and 500 for Modbus RTU
   7. Increased the maximum number of polling groups per device to 500 (up from 32)
   8. Improved protocol selection experience for Modbus. Modbus master/client and Modbus listen modes are now selectable as separate options in the main protocol dropdown menu.
   9. Improved Modbus diagnostic messages
2. Added SFTP client timeout setting
3. Enabled NTP client in TCP JSON mode to provide timestamps for Modbus JSON output over TCP

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-0#fixes)

1. Fixed an issue where the power failure clear button would not clear power events on the output side if the input side had not experienced a power event.
2. Fixed an issue where malformed JSON output would be sent for unsupported BACnet message types.
3. Fixed an issue where Modbus RTU listen mode would fail to handle more than 255 coils in a single incoming message
