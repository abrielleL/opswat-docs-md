<!-- source: https://www.opswat.com/docs/fenddiode/appendices -->

# Appendix I: Recommended Transfer Timings by Protocol

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Because of the unidirectional nature of a data diode, confirmation of data receipt cannot be sent upstream to the originating device. Based on the quantity and size of the data being sent and the speed of the local network, different protocols require different cycle times to ensure that data flows in an optimal manner. The tables below show suggested timings for different protocol configurations:

## [FTP / FTPS / SFTP Buffered (Non-Streaming) Transfer Timings](/docs/fenddiode/appendices#ftp--ftps--sftp-buffered-non-streaming-transfer-timings)

Suggested Buffered Mode Minimum Wait Times Between Files (in seconds)

| Size of File (kB) | FTP Wait Times (s) | FTPS Wait Times (s) | SFTP Wait Times (s) | Max Files Buffered Mode |
| --- | --- | --- | --- | --- |
| 1 | 0 - 1 | 0 - 1 | 0 - 1 | 60000 |
| 100 | 0 - 1 | 0 - 1 | 0 - 1 | 600 |
| 500 | 0 - 1 | 0 - 1 | 2 - 3 | 128 |
| 1000 | 0 - 1 | 1- 2 | 3- 4 | 64 |
| 5000 | 0 - 1 | 3 - 4 | 15 - 16 | 12 |
| 10000 | 0 - 1 | 6 – 8 | 29 – 32 | 6 |
| 30000 | 0 - 1 | 25 - 30 | 86 - 90 | 2 |
| 40000 | 0 - 1 | 80 - 85 | 114 - 120 | 1 |
| 50000 | 5 – 7 | 90 - 95 | 143 - 150 | 1 |
| 60000 | 20– 23 | 110 - 115 | 172 - 180 | 1 |

1. *Wait times are measured as the time between the end of a successful file transfer to the input side of the diode and the beginning of the next file transfer to the input side of the diode. They are essentially a pause between file transfers to allow the output side of the diode to pass the file through.*
2. Max files buffered only applies when using the diode in “buffered” mode. There is no maximum file size or file count when not buffering files on the diode. See [Diode Output Side FTP/FTPS settings](https://www.opswat.com/docs/fenddiode/configuration-settings/output-side-protocol-settings#ftp-client).

## [BACnet to AWS Publish Cycle Timings](/docs/fenddiode/appendices#bacnet-to-aws-publish-cycle-timings)

| Number of Registers | Suggested Polling Time (s) |
| --- | --- |
| <=10 | 1-2 seconds |
| 100 | 5 - 20 seconds |
| 250 | 10 - 45 seconds |
| 500 | 30 - 85 seconds |
| 750 | 45 - 125 seconds |
| 1000 | 60 - 175 seconds |

## [Modbus Polling Cycle Timings](/docs/fenddiode/appendices#modbus-polling-cycle-timings)

Modbus supports up to 40,000 registers. Minimum polling times for target register counts are indicated below. Polling times may need to be increased above the minimum based on network conditions and Modbus equipment speeds.

### [Modbus to AWS](/docs/fenddiode/appendices#modbus-to-aws)

| Number of Registers | Suggested Minimum Polling Time (s) |
| --- | --- |
| <=10 | 1 second |
| 100 | 6 - 10 seconds |
| 250 | 14 - 25 seconds |
| 500 | 30 - 45 seconds |
| 750 | 45 - 60 seconds |
| 1000 | 60 - 90 seconds |
| 3000 | 170 – 280 seconds |
| 5000 | 280 – 460 seconds |
| 10000 | 560 – 920 seconds |

### [Modbus to TCP JSON](/docs/fenddiode/appendices#modbus-to-tcp-json)

| Number of Registers | Suggested Minimum Polling Time (s) |
| --- | --- |
| <=3000 | 1 second |
| 5000 | 2 seconds |
| 8000 | 3 seconds |
| 10000 | 4 seconds |
| 40000 | 12 seconds |

### [Modbus to Modbus](/docs/fenddiode/appendices#modbus-to-modbus)

| Number of Registers | Suggested Minimum Polling Time (s) |
| --- | --- |
| <=40000 | 1 second |

## [TCP and UDP Protocol Interface and Timings](/docs/fenddiode/appendices#tcp-and-udp-protocol-interface-and-timings)

Data sent via the TCP and UDP features does not require wait times, but the program interfacing with the input side of the diode must wait to receive an acknowledgment of successful data receipt before sending more data.

Data being sent through the diode must be “chunked” into packets. The recommended packet size is 1460 bytes (the size of a single ethernet frame). After the diode has received and processed a packet, it will return an ACK in the form of the ASCII string “OK\r\n”. The ACK is optional in UDP mode, but strongly recommended.

If the source TCP/UDP client connected to the input side of the diode waits for the ACK from the diode, data can be streamed continuously with no additional timing delays or limitations.

For examples on how to setup a TCP/UDP client and server to interface with the diode please download example scripts from the support section of your Fend Cloud web account.
