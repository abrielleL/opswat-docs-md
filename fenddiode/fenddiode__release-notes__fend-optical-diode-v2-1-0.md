<!-- source: https://www.opswat.com/docs/fenddiode/release-notes/fend-optical-diode-v2-1-0 -->

# Fend Optical Diode v2.1.0

Released: 11/15/2022

## [Features/Changes:](/docs/fenddiode/release-notes/fend-optical-diode-v2-1-0#featureschanges)

1. Improved diode throughput by 25%.
2. Improved and expanded diagnostic messages, providing more useful information upfront. Updated message level descriptions to "Info", "Warning", and "Error".
3. Added sequence numbers to Modbus TCP and RTU R/R JSON outputs (AWS and TCP/JSON).
4. Added support for Modbus exception codes and timeout communications. The diode now sends exception codes and timeouts to the output side, displays an exception code when input side is down, displays exception codes when target device is down. Please refer to the user's manual for more details under "Example 2: Diode Settings for Modbus TCP Request/Response to Modbus TCP (Passthrough Mode)"

## [Fixes:](/docs/fenddiode/release-notes/fend-optical-diode-v2-1-0#fixes)

1. Fixed an issue where the Bank B green LED did not blink properly during data transmission in config mode.
2. Improved the process for setting the factory restore point for users upgrading from FW 1.0.X. See user's manual section "Resetting your Diode (5-Series)" for more details.
3. Fixed an issue with oversized certs and clearing of certs on both input and output side.
4. Fixed an issue where the output side power LED would not clear properly.
