<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-2-2 -->

# Fend Optical Diode v4.2.2

Released: 1/28/2025

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-2#featureschanges)

1. Enabled support for additional SFTP/SSH symmetric algorithms.
2. Added support for SFTP file rename and delete commands to streaming mode only.
3. Changed the format of the BACnet JSON schema to support multiple objects in a single payload. Numbers (except floats) and Boolean values are no longer delivered as strings.

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-2#fixes)

1. Fixed an issue where BACnet messages with multiple objects / properties were not being correctly sent in TCP JSON mode
2. Fixed an issue where escapable characters in BACnet messages could cause improper JSON output formatting in TCP JSON mode
3. Fixed an issue in the configuration interface where the output side FTP/S binary/text and active/passive options were not being set correctly
4. Fixed an issue that could cause a lag in the delivery of diagnostic messages
5. Fixed an issue that could cause the configuration session port timeout to fail to close the configuration port properly at expiration
6. Fixed and issue that was causing heartbeat loss indicator LEDs on the output side of the diode to fail to clear with the event clear timer expiration
