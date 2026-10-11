<!-- source: https://www.opswat.com/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns -->

# Appendix V: Status Indicator Light Patterns

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This section contains tables for cross-referencing status indicator patterns from the Red/Yellow/Green Status Indicator LED bank. Bank A is the status indicator bank for the input side of the diode. Bank C is the status indicator bank for the output side of the diode.

## [Mode-Dependent Sequences](/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns#mode-dependent-sequences)

During certain operations, the diode status indicator lights enter a mode-dependent sequence that indicates progress through a process. These mode-dependent sequences occur during initial bootup, while in configuration mode, and during firmware updates. If a fault/error occurs during any of these processes, the status lights will exit the sequence mode and display a permanent fault indicator pattern. See the [Fault Indicator Patterns](https://www.opswat.com/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns#fault-indicator-patterns) section below.

Note: A slow blink is 1 blink per second (500ms on 500ms off), a fast blink is 5 blinks per second (100ms on 100ms off)

### [Bootup Sequences (Applies to Input and Output Sides)](/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns#bootup-sequences-applies-to-input-and-output-sides)

| Red | Yellow | Green | Process Step |
| --- | --- | --- | --- |
| On for 2 seconds | On for 2 seconds | On for 2 seconds | Power On / LED test |
| Off | Off | Slow | ***Standard Runtime - No Errors (Continuous)*** |

### [Configuration Mode Sequences (Applies to the Input Side Only)](/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns#configuration-mode-sequences-applies-to-the-input-side-only)

| Red | Yellow | Green | Process Step |
| --- | --- | --- | --- |
| Flash Twice | Flash Twice | Flash Twice | Entering Config Mode |
| Off | Slow Blink | Off | ***Config Mode On (Continuous)*** |
| Off | Slow Blink | *Blink on Tx/Rx* | Config Data Transmit Successful |
| Flash Three Times | Flash Three Times | Flash Three times | Config Session Ended |

### [Firmware Update Sequences (Applies to Input and Output Sides)](/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns#firmware-update-sequences-applies-to-input-and-output-sides)

| Red | Yellow | Green | Process Step |
| --- | --- | --- | --- |
| On | Off | Off | ***Firmware Update Mode On (Continuous)*** |
| On | Fast Blink | Off | Firmware Transmission Being Received |
| Fast Blink | Fast Blink | Fast Blink | Firmware Update Success |
| Fast Blink | Off | Off | Firmware Update Fail |

### [Factory Restore Sequences (Applies to the Input Side Only)](/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns#factory-restore-sequences-applies-to-the-input-side-only)

Blinks red, then yellow, then green (waterfall) in quick succession 5 times to indicate a successful factory restore then reboots the diode.

## [Fault Indicator Patterns](/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns#fault-indicator-patterns)

| Red | Yellow | Green | Error Code | Description |
| --- | --- | --- | --- | --- |
| Off | Off | Slow | N/A | ***Standard Runtime - No Errors (Continuous)*** |
| Off | Fast | Off | 8 | Output Side Memory Full |
| Off | Fast | Slow | 9 | Input Side Data Receive Error |
| Off | Fast | Fast | 10 | Cellular Modem Error (CE models only) |
| Off | Fast | On | 11 | Ethernet Interface Down |
| Off | On | Slow | 13 | Network Time Protocol (NTP) Error |
| Off | On | Fast | 14 | Domain Name System (DNS) Error |
| Slow | Off | Off | 16 | Heartbeat Loss (Data Not Being Received by Output Side) |
| Slow | Off | Slow | 17 | Power Loss [1] |
| Slow | Slow | Slow | 21 | General Application Fault |
| Slow | Slow | Fast | 22 | Application Unable to Communicate with Target Destination |
| Slow | Slow | On | 23 | TLS Certificate Error |
| Slow | Fast | On | 27 | Listen Mode Sees No Valid Data |
| Slow | On | Off | 28 | Application Receiving Invalid Data |
| On | Fast | On | 59 | Power On Self-Test Fail (Hardware Failure) [2] |
| On | On | Fast | 62 | Tamper Event Detected [3] |
| On | On | On | 63 | Failed to Boot / Load Configuration |

1. This status indicator is for informational purposes only. When the 12V DC connection to the diode is lost, the diode will register this as a power fault. For 12 hours the diode will display this LED pattern to notify the user that, within the last 12 hours, there was a power fault. During this time the diode will continue to function normally. The status indicator will clear itself after 12 hours. This indicator can be disabled and/or the time for clearing the message changed via the diode configuration.
2. If a diode fails its internal hardware checks it may not operate as intended. Please contact Fend Support at [support@fend.tech](mailto:support@fend.tech).
3. When the diode detects a tamper event it locks down and becomes unusable. No protocols will be functional. If a diode has been tampered with, contact Fend Support at [support@fend.tech](mailto:support@fend.tech).
