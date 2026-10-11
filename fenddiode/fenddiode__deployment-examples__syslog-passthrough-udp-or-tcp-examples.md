<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/syslog-passthrough-udp-or-tcp-examples -->

# Syslog Passthrough (UDP or TCP) Examples

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The UDP and TCP client/server features allow for the transfer of syslog. While the diode does not currently generate its own syslog, it is fully capable of facilitating a one-way transfer of syslog to a target syslog server

## [Customer Requirements](/docs/fenddiode/deployment-examples/syslog-passthrough-udp-or-tcp-examples#customer-requirements)

For this feature, an existing syslog client and syslog server must be present.

## [Diode Settings for Syslog over UDP Client/Server](/docs/fenddiode/deployment-examples/syslog-passthrough-udp-or-tcp-examples#diode-settings-for-syslog-over-udp-clientserver)

For instructions on setting up Syslog over UDP please refer to the section [UDP Client/Server Installation Instructions](https://www.opswat.com/docs/fenddiode/deployment-examples/udp-client-server-examples), with the following adjustments:

1. For the input side, set the:

   1. Diode IP address to be the address where the devices on the network are configured to send their syslog messages.
   2. “Diode UDP Server Port” to 514
   3. Disable the “Reply with an ACK” option.
2. For the output side, set the

   1. “Target UDP Server IP” to match the target syslog server
   2. “Target UDP Server Port” to 514

## [Diode Settings for Syslog over TCP Client/Server](/docs/fenddiode/deployment-examples/syslog-passthrough-udp-or-tcp-examples#diode-settings-for-syslog-over-tcp-clientserver)

For instructions on setting up syslog over TCP please refer to the section [TCP Client/Server Installation Instructions](https://www.opswat.com/docs/fenddiode/deployment-examples/tcp-client-server-examples), with the following adjustments:

1. For the input side, set the:

   1. Diode IP address to be the address where the devices on the network are configured to send their syslog messages.
   2. “Diode TCP Server Port” to 6514
2. For the output side, set the

   1. “Target TCP Server IP” to match the target syslog server
   2. “Target TCP Server Port” to 6514

## [Syslog Bandwidth Considerations](/docs/fenddiode/deployment-examples/syslog-passthrough-udp-or-tcp-examples#syslog-bandwidth-considerations)

Please note that there is no flow control for syslog implementation. Therefore, if the volume of syslog messages exceeds the diode’s bandwidth, messages in excess of the diode’s bandwidth will be dropped.
