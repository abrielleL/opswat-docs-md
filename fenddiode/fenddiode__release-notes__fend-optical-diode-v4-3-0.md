<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-3-0 -->

# Fend Optical Diode v4.3.0

Released: 09/30/2026

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-3-0#featureschanges)

1. Added UDP Multicast support.
2. Added support for diode-generated syslog with delivery over UDP or TCP. This feature replaces legacy diagnostics.
3. Renamed existing output side protocol called "MQTT Client", that was exclusive to the Fend Cloud service, now simply called "Fend Cloud".
4. Added a new "MQTT Publisher" protocol to the output side that can be used with any MQTT broker.
5. Added support for Modbus/BACnet/LonIP JSON conversion to new MQTT Publisher.

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-3-0#fixes)

1. Fixed an issue where BACnet would fail to process certain properties.
