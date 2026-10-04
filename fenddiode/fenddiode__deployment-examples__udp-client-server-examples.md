<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/udp-client-server-examples -->

# UDP Client/Server Examples

The UDP client/server feature allows for the transfer of protocol-independent data using UDP. This feature accepts any and all data that can be sent over UDP. All data sent through the diode using this protocol will appear to the target UDP Server as though it originated from the diode. All information from layers 1-4 will be stripped when ingested by the diodes UDP Server.

## [Customer Requirements](/docs/fenddiode/deployment-examples/udp-client-server-examples#customer-requirements)

For this feature, an existing UDP client and server must be present. Similar to the FTP/FTPS modes, the diode acts as a “bump in the wire” inserting itself in between these two devices.

Data being sent through the diode must be “chunked” into packets; the recommended packet size is 1460 bytes (the size of a single ethernet frame)

While UDP is inherently un-managed, the diode input-side UDP server provides a flow control option to ensure that the amount of data sent to the diode does not exceed the diode’s throughput. To enable flow control, check the option (“Reply with an ACK”) in the input side UDP settings. In this mode, after the diode has received and processed a packet, it will return an ACK in the form of the ASCII string “OK\r\n”. The source UDP client interfacing with the input side of the diode should be programmed to wait to receive “OK” before sending the next datagram.

For details on how to interface with the diode in UDP client/server mode see [**Appendix I, TCP Passthrough Interface Protocol and Timings**](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol#tcp-and-udp-protocol-interface-and-timings).

For an example script of a UDP client and server that interface with the diode, please see the support downloads section in your Fend Cloud web account (<https://app.fend.tech/login>).

## [Example 1: Unicast UDP Client/Server](/docs/fenddiode/deployment-examples/udp-client-server-examples#example-1-unicast-udp-clientserver)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/udp-client-server-examples#diode-input-side-settings)

To configure the diode in UDP client/server mode, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.

   1. Note: This is the IP address that the source UDP client will use to connect to the diode’s UDP server.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select UDP Server from the dropdown and set the following:

4. Set the “Diode UDP Server Port” to be any port that is available on your host system, just make sure to remember what is entered. This port number will be required when configuring the source UDP client to communicate with the diode’s UDP server.
5. Disable "Enable Multicast"
6. Enable the “Reply with an ACK” option as needed. The default/recommended option is enabled.

### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/udp-client-server-examples#diode-output-side-settings)

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network.

Under Output Side -> Protocol Settings -> Select UDP Client from the dropdown and set the following fields:

2. Set the “Target UDP Server IP” to match the existing UDP server on the network.
3. Set the “Target UDP Server Port” to be the port the existing UDP server is listening on.

Finally, when done updating all settings press the “Save & Exit” button located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/udp-client-server-examples#installing-the-data-diode-after-configuration)

1. Connect the input side of the diode to the network where the source UDP client is running.
2. Connect the output side of the diode to the network where the target UDP server is running.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing from the client to the server.

## [Example 2: Multicast UDP Client/Server](/docs/fenddiode/deployment-examples/udp-client-server-examples#example-2-multicast-udp-clientserver)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/udp-client-server-examples#diode-input-side-settings)

To configure the diode in Multicast UDP client/server mode, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.

   1. Note: This is the IP address that the source UDP client will use to connect to the diode’s UDP server.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select UDP Server from the dropdown and set the following:

4. Set the “Diode UDP Server Port” to be any port that is available on your host system, just make sure to remember what is entered. This port number will be required when configuring the source UDP client to communicate with the diode’s UDP server.
5. Enable "Enable Multicast"
6. Enter the IP Address of the multicast group you wish to join.

### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/udp-client-server-examples#diode-output-side-settings)

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network.

Under Output Side -> Protocol Settings -> Select UDP Client from the dropdown and set the following fields:

2. Set the “Target UDP Server IP” to target the multicast group on the network.
3. Set the “Target UDP Server Port” to be the port the existing UDP server is listening on.

Finally, when done updating all settings press the “Save & Exit” button located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/udp-client-server-examples#installing-the-data-diode-after-configuration)

1. Connect the input side of the diode to the network where the source UDP client is running.
2. Connect the output side of the diode to the network where the target UDP server is running.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing from the client to the server.
