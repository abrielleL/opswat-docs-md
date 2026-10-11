<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/tcp-client-server-examples -->

# TCP Client/Server Examples

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The TCP feature allows for the transfer of protocol-independent data over a traditional TCP client/server connection. This feature accepts any and all data that can be sent over TCP. All data sent through the diode using this protocol will appear to the target TCP server as though it originated from the diode. All information from layers 1-4 will be stripped when ingested by the diodes TCP server.

## [Customer Requirements](/docs/fenddiode/deployment-examples/tcp-client-server-examples#customer-requirements)

For this feature, an existing TCP client and server must be present. Similar to the FTP/FTPS modes, the diode acts as a “bump in the wire” inserting itself in between these two devices.

The input side TCP connection requires flow control, as follows:

- Data being sent through the diode must be “chunked” into packets; the recommended packet size is 1460 bytes (the size of a single ethernet frame)
- After the diode has received and processed a packet, it will return an ACK in the form of the ASCII string “OK\r\n”. TCP client program interfacing with the input side of the diode must wait to receive “OK” before sending more data.

For details on how to interface with the diode in TCP client/server mode see [**Appendix I, TCP Passthrough Interface Protocol and Timings**](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol#tcp-and-udp-protocol-interface-and-timings).

For an example script of a TCP client and server that interface with the diode, please see the support downloads section in your Fend Cloud web account (<https://app.fend.tech/login>).

## [Diode Settings for TCP Client/Server](/docs/fenddiode/deployment-examples/tcp-client-server-examples#diode-settings-for-tcp-clientserver)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/tcp-client-server-examples#diode-input-side-settings)

To configure the diode in TCP client/server mode, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.

   1. Note: This is the IP address that the source TCP Client will use to connect to the diode’s TCP Server.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select TCP Server from the dropdown and set the following:

4. Set the “Diode TCP Server Port” to be any port that is available on your host system, just make sure to remember what is entered. This port number will be required when configuring the source TCP client to communicate with the diode’s TCP server.
5. Set the “Diode TCP Server Socket Timeout” to be any time you desire 0-255 seconds. This is the idle time allowed before the diode will close the socket. Note: a selection of “0” seconds disables the socket timeout. Meaning the diode will never close the socket. A “0” setting should be used with caution, however, as there is only one socket available on the diode. So, if the network connection is terminated unexpectedly, the diode will not accept new socket connections without a reset.

### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/tcp-client-server-examples#diode-output-side-settings)

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network.

Under Output Side -> Protocol Settings -> Select TCP Client from the dropdown and set the following fields:

2. Set the “Target TCP Server IP” to be that of the existing target TCP server on the network.
3. Set the “Target TCP Server Port” to be the port the existing target TCP server is listening on.

Finally, when done updating all settings press the “Save & Exit” button located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/tcp-client-server-examples#installing-the-data-diode-after-configuration)

1. Connect the input side of the diode to the network where the source TCP client is running.
2. Connect the output side of the diode to the network where the target TCP server is running.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing from the client to the server.

## [Setting Up TLS on TCP Client/Server](/docs/fenddiode/deployment-examples/tcp-client-server-examples#setting-up-tls-on-tcp-clientserver)

For added security, you may wish to enable TLS on the TCP Client/Server feature. Doing so will encrypt all data sent to and from the diode. This feature requires the input side TCP server to be configured with a certificate key pair. This can be a key pair managed by your organization or one you generate yourself. Below we will go over how to create a basic key pair using OpenSSL.

### [Generating a TLS Certificate and Key Pair](/docs/fenddiode/deployment-examples/tcp-client-server-examples#generating-a-tls-certificate-and-key-pair)

The following example uses OpenSSL on Linux. The same commands can be used in Windows using OpenSSL. To generate a private key and certificate for the input side diode TCP server perform the following 3 commands, replacing file names as desired.

Example 1Example 2Copyopenssl genpkey -algorithm RSA -out example.keyopenssl req -new -key example.key -out csr.pemopenssl req -x509 -days 365 -key example.key -in csr.pem -out example.crt# Non-interactive and 10 years expirationopenssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -sha256 -days 3650 -nodes -subj "/C=XX/ST=StateName/L=CityName/O=CompanyName/OU=CompanySectionName/CN=CommonNameOrHostname"

The second command will prompt for a few questions, this information will be visible in the certificate generated. See below for a full example of the commands above.

## [Diode Settings for Enabling TLS for TCP Client/Server](/docs/fenddiode/deployment-examples/tcp-client-server-examples#diode-settings-for-enabling-tls-for-tcp-clientserver)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/tcp-client-server-examples#diode-input-side-settings)

To enable TLS for the TCP server mode, navigate to: Input Side -> Protocol Settings -> Select TCP Server from the dropdown and perform the following:

1. Enable TLS by selecting the checkbox labeled “Enable TLS”
2. Under the Certificate tab, upload the certificate generated in the previous step.
3. Under the Private Key tab, upload the key generated in the previous step.
4. Finally, give the same certificate to the external TCP client (data source) that will be connecting to the diode input side server for the purposes of server identity verification.

### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/tcp-client-server-examples#diode-output-side-settings)

To enable TLS for the TCP client mode, navigate to: Output Side -> Protocol Settings -> Select TCP Client from the dropdown and perform the following:

1. Enable TLS by selecting the checkbox labeled “Enable TLS”
2. Under the Certificate tab, upload the certificate from your target TCP server (data destination). This will allow the output side to verify the identity of the target server.

Finally, when done updating all settings press the “Save & Exit” button located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/tcp-client-server-examples#installing-the-data-diode-after-configuration)

1. Connect the input side of the diode to the network where the source TCP/TLS client is running.
2. Connect the output side of the diode to the network where the target TCP/TLS server is running.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing from the client to the server.
