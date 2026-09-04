<!-- source: https://www.opswat.com/docs/fenddiode/configuration-settings/output-side-protocol-settings -->

# Output Side Protocol Settings

## [Protocol Selections](/docs/fenddiode/configuration-settings/output-side-protocol-settings#protocol-selections)

The options in this section will dynamically update based on the communications interface selected (RS485, Ethernet, or Cellular) and will display the protocol options compatible with the selected communication interface. The diode operates in a single protocol mode at a time based on this selection (for example: FTP or Modbus, but not both simultaneously). Once a protocol selection is made, the settings for that protocol will be displayed below.

### [RS485 Protocol Options](/docs/fenddiode/configuration-settings/output-side-protocol-settings#rs485-protocol-options)

- Modbus RTU Slave/Server – Sets the output side to act as a Modbus RTU slave/server for outbound serial data communication

### [Ethernet Protocol Options](/docs/fenddiode/configuration-settings/output-side-protocol-settings#ethernet-protocol-options)

- Modbus TCP Slave/Server - Sets the output side to act as a Modbus TCP slave/server for outbound Ethernet data communication
- FTP Client - Sets the output side to act as an FTP client for outbound Ethernet data communication
- FTPS Client - Sets the output side to act as an FTPS client for outbound Ethernet data communication
- SFTP Client – Sets the output side to act as an SFTP client for outbound Ethernet data communication
- MQTT Client - Sets the output side to act as an MQTT client (to Fend Cloud-AWS) for outbound Ethernet data communication
- TCP Client (JSON Protocol Conversion) – Sets the output side to format incoming BACnet, LON, or Modbus as JSON for transmission via TCP client for outbound Ethernet data communication
- TCP Client – Sets the output side to act as a TCP client for outbound Ethernet data communication
- UDP Client – Sets the output side to act as a UDP client for outbound Ethernet data communication

### [Cellular Protocol Options](/docs/fenddiode/configuration-settings/output-side-protocol-settings#cellular-protocol-options)

- MQTT Client - Sets the output side to use MQTT (to Fend Cloud-AWS) for outbound cellular data communication

## [FTP Client](/docs/fenddiode/configuration-settings/output-side-protocol-settings#ftp-client)

- Target FTP Server Address – Sets the IP address of target FTP external server.

  - [IP address in format: ###.###.###.### or URL UTF8 string, max 32 characters]
- Target FTP Server Username – Sets the user ID that the diode will use to log into the target external FTP server. The external server must support a matching username.

  - [UTF8 string, max 32 characters]
- Target FTP Server Password – Sets the password that the diode will use to log into the target external FTP server. The external server must support a matching password.

  - [UTF8 string, max 32 characters]
- Data Mode – Sets the data mode of the diode FTP client. The recommended default is binary.

  - [Binary, Text]
- Data Socket Mode – Sets the FTP data socket mode, passive or active. The recommended default is passive.

  - [Passive, Active]
- Socket Timeout (s) - The length of time in seconds that a socket operation, such as send and receive, will wait until it returns an error.

  - [1-255 seconds]
- Retry timer (min) – The length of time in minutes that the diode waits before retrying a file transfer if a previous attempt is unsuccessful.

  - [0: No retry. On fail, move to next file, 1-65534 wait time (in minutes), 65535 Retry forever. Do not move to the next file]
- Log File Save Directory – Sets a directory where diode log files will be stored in the target FTP server machine.

  - [UTF8 string, max 32 characters]
- Log File Enabled – Enables or disables logging events such as failed FTP transfers or power events to the Log File Save Directory.

  - [Checked, Unchecked]
- Streaming Enabled – If checked, the diode will deliver FTP data as it is received. In this mode there is no file size limitation, but if the network is unstable, it can increase the potential for data loss. If unchecked, the diode will buffer files on the output side, only sending data to the Target FTP Server when a complete file has been uploaded to the diode. This is better in unstable networks but limits the maximum size and number of files that can be sent at any given time. See [Appendix I: Recommended Transfer Timings by Protocol](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol) for more information.

  - [Checked, Unchecked]
- Relative Pathing Enabled – If checked, the FTP client will assume all directory change requests are relative to the initial home or login directory of the user on the server. For example, if you log into an FTP server with user ‘test’ and upon login you are in the ‘test’ users home directory (something like ‘/home/test/’), all directory changes will be relative that directory and you cannot go above that directory in the file system during a session. If this option is unchecked, all change directory requests will be treated as absolute directories relative to the server’s concept of root. For most Windows-based FTP servers, this option has little impact because of how they handle pathing. For Linux FTP servers, we recommend enabling relative pathing, otherwise the diode will attempt to put files in OS root by default.

  - [Checked, Unchecked]

## [FTPS Client](/docs/fenddiode/configuration-settings/output-side-protocol-settings#ftps-client)

- Implicit / Explicit Mode – Sets which FTPS mode should be used when establishing a connection.

  - [Explicit (Port 21), Implicit (Port 990)]
- Target FTP Server Address – Sets the IP address of target FTP external server.

  - [IP address in format: ###.###.###.### or URL UTF8 string, max 32 characters]
- Target FTP Server Username – Sets the user ID that the diode will use to log into the target external FTP server. The external server must support a matching username.

  - [UTF8 string, max 32 characters]
- Target FTP Server Password – Sets the password that the diode will use to log into the target external FTP server. The external server must support a matching password.

  - [UTF8 string, max 32 characters]
- Data Mode – Sets the data mode of the diode FTP client. The recommended default is binary.

  - [Binary, Text]
- Data Socket Mode – Sets the FTP data socket mode, passive or active. The recommended default is passive.

  - [Passive, Active]
- Socket Timeout (s) - The length of time in seconds that a socket operation, such as send and receive, will wait until it returns an error.

  - [1-255 seconds]
- Retry timer (min) – The length of time in minutes that the diode waits before retrying a file transfer if a previous attempt is unsuccessful.

  - [0: No retry. On fail, move to next file, 1-65534 wait time (in minutes), 65535 Retry forever. Do not move to the next file]
- Log File Save Directory – Sets a directory where diode log files will be stored in the target FTP server machine.

  - [UTF8 string, max 32 characters]
- Log File Enabled – Enables or disables logging events such as failed FTP transfers or power events to the Log File Save Directory.

  - [Checked, Unchecked]
- Streaming Enabled – If checked, the diode will deliver FTPS data as it is received. In this mode there is no file size limitation, but if the network is unstable, it can increase the potential for data loss. If unchecked, the diode will buffer files on the output side, only sending data to the Target FTPS Server when a complete file has been uploaded to the diode. This is better in unstable networks but limits the maximum size and number of files that can be sent at any given time. See [Appendix I: Recommended Transfer Timings by Protocol](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol) for more information.

  - [Checked, Unchecked]
- Relative Pathing Enabled – If checked, the FTP client will assume all directory change requests are relative to the initial home or login directory of the user on the server. For example, if you log into an FTP server with user ‘test’ and upon login you are in the ‘test’ users home directory (something like ‘/home/test/’), all directory changes will be relative that directory and you cannot go above that directory in the file system during a session. If this option is unchecked, all change directory requests will be treated as absolute directories relative to the server’s concept of root. For most Windows-based FTP servers, this option has little impact because of how they handle pathing. For Linux FTP servers, we recommend enabling relative pathing, otherwise the diode will attempt to put files in OS root by default.

  - [Checked, Unchecked]

### [FTPS Certificate Tab](/docs/fenddiode/configuration-settings/output-side-protocol-settings#ftps-certificate-tab)

FTPS Certificate – Strongly Encouraged. If you wish for the FTPS client to verify the identity of the server it connects to before delivering data, provide the FTPS certificate here. NOTE: If this field is left blank, the diode will automatically accept any public server as valid and will not attempt to verify the identity of the target server. The connection will still be encrypted. NOTE: FTPS certs have a max supported file size of 4096 bytes.

- Open – Loads a new certificate from file.

  - [x509 PEM “.crt” file]
- Clear – Clears the current certificate.

## [SFTP Client](/docs/fenddiode/configuration-settings/output-side-protocol-settings#sftp-client)

### [SFTP Tab](/docs/fenddiode/configuration-settings/output-side-protocol-settings#sftp-tab)

- Target SFTP Server Address – Sets the address of target SFTP external server.

  - [IP address in format: ###.###.###.### or URL UTF8 string, max 32 characters]
- Authentication Mode – Sets whether the SFTP client will authenticate with the Target SFTP server using password authentication, public key authentication or either.

  - [Password, Public Key, Password & Public Key]
- Target SFTP Server Username – Sets the user ID that the diode will use to log into the target external SFTP server. Must match a valid username on the external server.

  - [UTF8 string, max 32 characters]
- Target SFTP Server Password – Sets the password that the diode will use to log into the target external FTP server. Must match a valid password for the given username on the external server.

  - [UTF8 string, max 32 characters]
- Retry timer (min) – The length of time in minutes that the diode waits before retrying a file transfer if a previous attempt is unsuccessful.

  - [0: No retry. On fail, move to next file, 1-65534 wait time (in minutes), 65535 Retry forever. Do not move to the next file]
- Socket Timeout (s) - The length of time in seconds that a socket operation, such as send and receive, will wait until it returns an error.

  - [1-255 seconds]
- Log File Save Directory – Sets a directory where diode log files will be stored in the target SFTP server machine.

  - [UTF8 string, max 32 characters]
- Log File Enabled – Enables or disables logging events such as failed SFTP transfers or power events to the Log File Save Directory.

  - [Checked, Unchecked]
- Streaming Enabled – If checked, the diode will deliver SFTP data as it is received. In this mode there is no file size limitation, but if the network is unstable, it can increase the potential for data loss. If unchecked, the diode will buffer files on the output side, only sending data to the Target SFTP Server when a complete file has been uploaded to the diode. This is better in unstable networks but limits the maximum size and number of files that can be sent at any given time. See [Appendix I: Recommended Transfer Timings by Protocol](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol) for more information.

  - [Checked, Unchecked]
- Relative Pathing Enabled – If checked, the FTP client will assume all directory change requests are relative to the initial home or login directory of the user on the server. For example, if you log into an FTP server with user ‘test’ and upon login you are in the ‘test’ users home directory (something like ‘/home/test/’), all directory changes will be relative that directory and you cannot go above that directory in the file system during a session. If this option is unchecked, all change directory requests will be treated as absolute directories relative to the server’s concept of root. For most Windows-based FTP servers, this option has little impact because of how they handle pathing. For Linux FTP servers, we recommend enabling relative pathing, otherwise the diode will attempt to put files in OS root by default.

  - [Checked, Unchecked]

### [SFTP Private Auth Key Tab](/docs/fenddiode/configuration-settings/output-side-protocol-settings#sftp-private-auth-key-tab)

SFTP Private Auth Key – **Required**. SFTP clients require a public/private key pair for establishing the secure connection. SFTP keys have a max supported file size of 4096 bytes.

- Open – Loads a new key from file.

  - [SSH Private Key file]
- Clear – Clears the current key.

### [SFTP Public Auth Key Tab](/docs/fenddiode/configuration-settings/output-side-protocol-settings#sftp-public-auth-key-tab)

SFTP Public Auth Key – **Required**. SFTP clients require a public/private key pair for establishing the secure connection and for logging into the server if using public key authentication. If using public key authentication, the public authentication key of the server must match this key. SFTP keys have a max supported file size of 4096 bytes.

- Open – Loads a new key from file.

  - [SSH Public Key file]
- Clear – Clears the current key.

### [SFTP Public Host Key Tab](/docs/fenddiode/configuration-settings/output-side-protocol-settings#sftp-public-host-key-tab)

SFTP Public Host Key – **Strongly Encouraged**. This key is used to verify the identity of the target SFTP server. It must match the public host key of the SFTP server you will be connecting to. NOTE: If this field is left blank, the diode will automatically accept any public server host key as valid and will not attempt to verify the identity of the target server. The connection will still be encrypted. SFTP keys have a max supported file size of 4096 bytes.

- Open – Loads a new key from file.

  - [SSH Public Key file]
- Clear – Clears the current key.

### [Supplied SSH Key Pair](/docs/fenddiode/configuration-settings/output-side-protocol-settings#supplied-ssh-key-pair)

All Fend Diodes that shipped with firmware version 4.2.5+ come with pre-installed unique default keys for SFTP mode. For the output side SFTP Client, the keys provided are the Private and Public Auth Keys. The provided key type is ed25519. If your organization’s key management policies require different keys, you can clear the defaults and provide custom keys that meet your policies per the supported key types listed above.

## [Modbus TCP Slave/Server](/docs/fenddiode/configuration-settings/output-side-protocol-settings#modbus-tcp-slaveserver)

- TCP Socket Timeout (s) – Sets the length of time before an idle Modbus client connection will be logged out of the diode’s output side Modbus server.

  - [0-255, in seconds, a “0” setting means the connection will never timeout]

## [Modbus RTU Slave/Server](/docs/fenddiode/configuration-settings/output-side-protocol-settings#modbus-rtu-slaveserver)

There are no additional settings for Modbus RTU at this time. In Modbus RTU mode the outbound side of the diode will act as a Modbus device.

## [MQTT Client](/docs/fenddiode/configuration-settings/output-side-protocol-settings#mqtt-client)

- Device ID – Displays the unique ID that identifies the diode in the cloud.
- Topic – Cloud topic to publish. If using Fend Cloud, this should be set at the factory.

  - [UTF8 string, max 32 characters]
- Endpoint – Endpoint URL to publish. If using Fend Cloud, this should be set at the factory.

  - [UTF8 string, max 64 characters]
- Publish Cycle Time (s) – How often the diode should publish data to the MQTT endpoint. This setting should be adjusted based on the volume of data and the speed of the local connection. See [Appendix I: Recommended Transfer Timings by Protocol](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol)

  - [0 – 255 seconds]
- Port – Sets the port over which MQTT data is uploaded

  - [443 (HTTPS) or 8883 (MQTT)]

### [MQTT Client Certificate Authority Tab](/docs/fenddiode/configuration-settings/output-side-protocol-settings#mqtt-client-certificate-authority-tab)

CA – Required. This certificate comes preloaded on all Fend diodes and should generally be left as is. In the event a change in certificates is needed, a Fend support notification will be sent out with specific instructions. NOTE: Max supported file size of 4096 bytes.

- Open – Loads a new certificate from file.

  - [x509 PEM “.ca” file]
- Clear – Clears the current certificate.

## [TCP Client (JSON Protocol Conversion)](/docs/fenddiode/configuration-settings/output-side-protocol-settings#tcp-client-json-protocol-conversion)

- Target IP Address – Sets the IP address of the target external TCP server.

  - [IP address in format: ###.###.###.###]
- Target Port – Sets the port of the target external TCP server.

  - [1-65535]

## [TCP Client](/docs/fenddiode/configuration-settings/output-side-protocol-settings#tcp-client)

- Target TCP Server IP Address – Sets the IP address of the target external TCP server.

  - [IP address in format: ###.###.###.###]
- Target TCP Server Port – Sets the port of the target external TCP server.

  - [1-65535]
- Enable TLS – Enables or disables TLS over TCP.

### [TCP TLS Certificate Tab](/docs/fenddiode/configuration-settings/output-side-protocol-settings#tcp-tls-certificate-tab)

TLS Certificate – Strongly Encouraged. If you wish for the TCP client to verify the identity of the server it connects to before delivering data, provide the TLS certificate here. This certificate must match the TLS certificate on the TCP server. NOTE: If this field is left blank, the diode will automatically accept any public server as valid and will not attempt to verify the identity of the target server. The connection will still be encrypted. NOTE: Max supported file size of 4096 bytes.

- Open – Loads a new certificate from file.

  - [x509 PEM “.crt” file]
- Clear – Clears the current certificate.

## [UDP Client](/docs/fenddiode/configuration-settings/output-side-protocol-settings#udp-client)

- Target UDP Server IP Address – Sets the IP address of the target external UDP server.

  - [IP address in format: ###.###.###.###]
- Target UDP Server Port – Sets the port of the target external UDP server.

  - [1-65535]
