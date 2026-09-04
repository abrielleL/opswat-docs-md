<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v4-2-4 -->

# Fend Optical Diode v4.2.4

Released: 3/20/2025

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-4#featureschanges)

1. Added support for SFTP rename and delete commands in buffered mode
2. Added support for FTP / FTPS delete command in buffered and streaming modes
3. Added support for larger BACnet message sizes, up to a full single frame (1500 bytes). Multi-frame messages not supported.
4. Added an info-level diagnostic message reporting the diode firmware version at start-up

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v4-2-4#fixes)

1. Fixed an issue that would cause the slow performance over TCP-based protocols on networks with long round-trip times (RTT) such as cellular networks
2. Fixed an issue in FTP, FTPS, SFTP, and MQTT where the output side status LEDs would incorrectly display "connection successful" when no connection to the target server had been attempted.
3. Changed the startup behavior of FTP, FTPS, and SFTP output side clients, which now connect to the server at bootup to confirm the connection instead of waiting for a file to be received. This is now similar to other protocols.
