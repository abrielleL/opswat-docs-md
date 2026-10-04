<!-- source: https://www.opswat.com/docs/fenddiode/configuration-settings/input-side-protocol-settings -->

# Input Side Protocol Settings

## [Protocol Selections](/docs/fenddiode/configuration-settings/input-side-protocol-settings#protocol-selections)

The options in this section will dynamically update based on the communications interface selected (RS485 or Ethernet) and will display the protocol options compatible with the selected communication interface. The diode operates in a single protocol mode at a time based on this selection (for example: FTP or Modbus, but not both simultaneously). Once a protocol selection is made, the settings for that protocol will be displayed below.

## [RS485 Protocol Options](/docs/fenddiode/configuration-settings/input-side-protocol-settings#rs485-protocol-options)

- BACnet MSTP Listen – Sets the input side to listen for and pass through inbound BACnet MSTP serial data communication.
- Modbus RTU Master/Client – Sets the input side to act a Modbus RTU master/client for inbound serial data communication
- Modbus RTU Listen – Sets the input side to listen for and pass through inbound Modbus RTU for serial data communication

## [Ethernet Protocol Options](/docs/fenddiode/configuration-settings/input-side-protocol-settings#ethernet-protocol-options)

- BACnet IP Listen – For use with port mirroring, sets the input side to listen for and pass through inbound BACnet Ethernet data communication
- Modbus TCP Master/Client - Sets the input side to act a Modbus TCP master/client for inbound Ethernet data communication
- Modbus TCP Listen - For use with port mirroring, sets the input side to listen for and pass through inbound Modbus TCP for Ethernet data communication
- FTP Server - Sets the input side to act as an FTP server for inbound Ethernet data communication
- FTPS Server - Sets the input side to act as an FTPS server for inbound Ethernet data communication
- SFTP Server – Sets the input side to act as an SFTP server for inbound Ethernet data communication
- LON Listen - For use with port mirroring, sets the input side to listen for and pass through inbound LON IP for Ethernet data communication
- TCP Server – Sets the input side to act as a TCP server for inbound Ethernet data communication
- UDP Server – Sets the input side to act as a UDP server for inbound Ethernet data communication

## [FTP Server](/docs/fenddiode/configuration-settings/input-side-protocol-settings#ftp-server)

- Diode FTP Server Username – Sets the username that will be used by the external FTP client to log into the FTP server on the diode. The external client must have a matching username.

  - [UTF8 string, max 32 characters]
- Diode FTP Server Password – Sets the password that will be used by the external FTP client to log into the FTP server on the diode. The external client must have a matching password.

  - [UTF8 string, max 32 characters]
- Port Number Min – Sets a minimum value in the range for the random port number to be opened for the FTP data channel. For use with firewall configurations.

  - [1-65535]
- Port Number Max – Sets a maximum value in the range for the random port number to be opened for the FTP data channel. For use with firewall configurations.

  - [1-65535]

## [FTPS Server](/docs/fenddiode/configuration-settings/input-side-protocol-settings#ftps-server)

- Implicit / Explicit Mode – Sets which FTPS mode should be used when establishing a connection.

  - [Explicit (Port 21), Implicit (Port 990)]
- Diode FTP Server Username – Sets the username that will be used by the external FTP client to log into the FTP server on the diode. The external client must have a matching username.

  - [UTF8 string, max 32 characters]
- Diode FTP Server Password – Sets the password that will be used by the external FTP client to log into the FTP server on the diode. The external client must have a matching password.

  - [UTF8 string, max 32 characters]
- Port Number Min – Sets a minimum value in the range for the random port number to be opened for the FTP data channel. For use with firewall configurations.

  - [1-65535]
- Port Number Max – Sets a maximum value in the range for the random port number to be opened for the FTP data channel. For use with firewall configurations.

  - [1-65535]

### [FTPS Certificate Tab](/docs/fenddiode/configuration-settings/input-side-protocol-settings#ftps-certificate-tab)

FTPS Certificate – **Required**. FTPS servers require a certificate and key to generate the encrypted data channel. NOTE: FTPS certs have a max supported file size of 4096 bytes.

- Open – Loads a new certificate from file.

  - [x509 PEM “.crt” file]
- Clear – Clears the current certificate.

### [FTPS Private Key Tab](/docs/fenddiode/configuration-settings/input-side-protocol-settings#ftps-private-key-tab)

FTPS Private Key – **Required**. This is the private key paired with the certificate above. Max supported file size of 4096 bytes.

- Open – Loads a new key from file.

  - [x509 PEM “.key” file]
- Clear – Clears the current key.

| FTPS Server TLS Public/Private Key Support | |
| --- | --- |
| Key Algorithm | Key Size |
| RSA | Min: 1024, Max: 4096 |
| ECDSA | 256, 384, 521 |
| ECDH | 256, 384, 521 |
| FTPS Server TLS Certificate Signature Support | |
| Signature Hash | SHA256, SHA384 and SHA512 |

### [Supplied FTPS Certificate + Private Key Pair](/docs/fenddiode/configuration-settings/input-side-protocol-settings#supplied-ftps-certificate--private-key-pair)

All Fend Diodes that shipped with firmware version 4.2.5+ come with pre-installed unique default keys for FTPS mode. For the input side FTPS Server we provide a Certificate and Private Key. If your organization’s certificate management policies conflict with the use of the certificate provided, please clear and provide a certificate and private key that meets your policies. The properties of the provided pair are the following:

- Signature Algorithm: ecdsa-with-SHA256
- Public Key Algorithm: id-ecPublicKey (384 bit)
- Valid for 100 years

## [SFTP Server](/docs/fenddiode/configuration-settings/input-side-protocol-settings#sftp-server)

- Authentication Mode – Sets whether the SFTP server will allow password authentication, public key authentication or either.

  - [Password, Public Key, Password & Public Key]
- Diode SFTP Server Username – Sets the username that will be used by the external SFTP client to log into the SFTP server on the diode. The external client must have a matching username.

  - [UTF8 string, max 32 characters]
- Diode SFTP Server Password – Sets the password that will be used by the external SFTP client to log into the SFTP server on the diode. The external client must have a matching password.

  - [UTF8 string, max 32 characters]
- Idle Timeout – Sets the SFTP server idle timeout. When the set time has expired the connection with the SFTP client will be terminated.

### [SFTP Private Host Key Tab](/docs/fenddiode/configuration-settings/input-side-protocol-settings#sftp-private-host-key-tab)

SFTP Private Host Key – **Required**. SFTP servers require a public/private host key pair for establishing a secure encrypted connection and verifying the identity of the server to a client attempting to connect. SFTP keys have a max supported file size of 4096 bytes.

- Open – Loads a new key from file.

  - [SSH Private Key file]
- Clear – Clears the current key.

### [SFTP Public Host Key Tab](/docs/fenddiode/configuration-settings/input-side-protocol-settings#sftp-public-host-key-tab)

SFTP Public Host Key – **Required**. SFTP servers require a public/private host key pair for establishing a secure encrypted connection and verifying the identity of the server to a client attempting to connect. The public host key of the connecting client must match this key. SFTP keys have a max supported file size of 4096 bytes.

- Open – Loads a new key from file.

  - [SSH Public Key file]
- Clear – Clears the current key.

### [SFTP Public Auth Key Tab](/docs/fenddiode/configuration-settings/input-side-protocol-settings#sftp-public-auth-key-tab)

SFTP Public Auth Key – Optional if using username/password for authentication. Required if using public key authentication mode. This must match the public authentication key of the SFTP client you will be using to connect to the diode. SFTP keys have a max supported file size of 4096 bytes.

- Open – Loads a new key from file.

  - [SSH Public Key file]
- Clear – Clears the current key.

| SFTP Server Public/Private Host Key Support | |
| --- | --- |
| Key Algorithm | Key Size |
| RSA | Min: 1024, Max: 4096 |
| ECDSA | 256, 384 |
| DSA | 1024 |
| EdDSA 25519 | N/A |

| SFTP Server Public Auth Key Support | |
| --- | --- |
| Key Algorithm | Key Size |
| ECDSA | 256, 384 |

### [Supplied SSH Key Pair](/docs/fenddiode/configuration-settings/input-side-protocol-settings#supplied-ssh-key-pair)

All Fend Diodes that shipped with firmware version 4.2.5+ come with pre-installed unique default keys for SFTP mode. For the input side SFTP Server, the keys provided are the Private and Public Host Keys. The provided key type is ed25519. If your organization’s key management policies require different keys, you can clear the defaults and provide custom keys that meet your policies per the supported key types listed above.

## [TCP Server](/docs/fenddiode/configuration-settings/input-side-protocol-settings#tcp-server)

- Diode TCP Server Port – The port the diode will open and listen on to receive connections from a TCP Client on the protected network

  - [1-65535]
- Diode TCP Server Socket Timeout (s) – The idle time allowed before the diode closes a TCP connection.

  - [0-9999, in seconds, a “0” setting means the connection will never timeout]
- Enable TLS – Enables or disables TLS over TCP.

  - [Checked: TLS enabled, Unchecked: TLS disabled]

### [TCP TLS Certificate Tab](/docs/fenddiode/configuration-settings/input-side-protocol-settings#tcp-tls-certificate-tab)

TLS Certificate – Required for TLS. TLS servers require a certificate and key to encrypt data. NOTE: TLS certs have a max supported file size of 4096 bytes.

- Open – Loads a new certificate from file.

  - [x509 PEM “.crt” file]
- Clear – Clears the current certificate.

### [TCP TLS Private Key Tab](/docs/fenddiode/configuration-settings/input-side-protocol-settings#tcp-tls-private-key-tab)

TLS Private Key – Required for TLS. This is the private key paired with the certificate above. Max supported file size of 4096 bytes.

- Open – Loads a new key from file.

  - [x509 PEM “.key” file]
- Clear – Clears the current key.

| TCP Server TLS Public/Private Key Support | |
| --- | --- |
| Key Algorithm | Key Size |
| RSA | Min: 1024, Max: 4096 |
| ECDSA | 256, 384, 521 |
| ECDH | 256, 384, 521 |
| TCP Server TLS Certificate Signature Support | |
| Signature Hash | SHA256, SHA384 and SHA512 |

### [Supplied TLS Certificate + Private Key Pair](/docs/fenddiode/configuration-settings/input-side-protocol-settings#supplied-tls-certificate--private-key-pair)

All Fend Diodes that shipped with firmware version 4.2.5+ come with pre-installed unique default keys for TCP + TLS mode. For the input side TCP+TLS Server we provide a Certificate and Private Key. If your organization’s key management policies require different keys, you can clear the defaults and provide custom keys that meet your policies per the supported key types listed above. The properties of the provided pair are the following:

- Signature Algorithm: ecdsa-with-SHA256
- Public Key Algorithm: id-ecPublicKey (384 bit)
- Valid for 100 years

## [UDP Server](/docs/fenddiode/configuration-settings/input-side-protocol-settings#udp-server)

- Diode UDP Server Port – The port the diode will open and listen on to receive datagrams from a UDP Client on the protected network

  - [1-65535]
- Enable Multicast - Enables or disables multicast for the UDP server. Disables `Reply with and ACK`

  - [Checked: Enable multicast and join the group listed below, Unchecked: Use Unicast for UDP Server]
- Multicast Group - The multicast group you wish to receive multicast data on.

  - [IP address in format: ###.###.###.###]
- Reply with an ACK – Configures whether the UDP server will respond with an acknowledgement to each datagram. If checked, after the diode has received and processed a packet, it will return an ACK in the form of the ASCII string “OK\r\n”.

  - [Checked: Send ACK, Unchecked: Do not send ACK]

## [Modbus TCP Master/Client](/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-tcp-masterclient)

### [Global Modbus TCP Device Settings](/docs/fenddiode/configuration-settings/input-side-protocol-settings#global-modbus-tcp-device-settings)

- Read/Transmit Timeout – Length of time the diode will wait for a response from the target Modbus device before timing out.

  - [1 – 32,000, in increments of 1 millisecond]
- Polling –Time interval that diode waits between polling events.

  - [1 – 65,535, in seconds]
- Add a device [+] – Creates a new Modbus TCP device which shows up in the device list. Double click on the newly listed device to configure it. See the next section Individual Modbus TCP Device Settings for more details.

  - [Maximum: 32 devices]
- Remove a device [x] – **Removes the selected Modbus TCP device in the list window.**
- Devices – Displays the total count of configured Modbus TCP devices.

  - [0 – 32]
- Register Groups – Displays the total count of configured register groups across all TCP devices.

  - [0 – 500]
- Registers – Displays the total count of configured registers across all groups on all TCP devices.

  - [0 – 40,000]
- Device list window - A list of Modbus TCP devices that are being monitored by the diode. Double click on a device entry in the list to configure that device.

### [Individual Modbus TCP Device Settings](/docs/fenddiode/configuration-settings/input-side-protocol-settings#individual-modbus-tcp-device-settings)

- Device UID – Fend assigned unique ID for the Modbus device. This number is used internally by the diode to track Modbus devices.
- Target Modbus Unit ID – The Modbus unit ID of the target Modbus device to be monitored

  - [1 - 255]
- Unit ID Mapping Enabled – Enable or disable remapping Modbus unit ID’s when sent through the diode. With this feature you can give a Modbus device a different Modbus unit ID on the output side of the diode than it has on the input side network. Helpful for distinguishing between multiple devices on a network with overlapping register ranges when they are all coming from a single IP address on the output side of the diode.

  - [Enabled, Disabled]
- Map ID – The new Modbus unit ID to be assigned on the output side of the data diode for this device.

  - [1-255]
- Target IP Address - The IP address of the target Modbus device to be monitored

  - [IP address in format: ###.###.###.###]
- Target Port - The port number that the target Modbus device is listening on. The default Modbus port is 502.

  - (1-65535]
- High Word First – Specifies the word order of the source data for the Modbus device. Applies to all register groups listed for the device. If you have register ranges on a single device with differing word/byte orders, then you will need to create a separate “device” with the same IP address to apply different word/byte settings to those ranges.

  - [Checked = True (High Word First), Unchecked = False (Low Word First)]
- High Byte First – Specifies the byte order of the source data for the Modbus device. Applies to all register groups listed for the device. If you have register ranges on a single device with differing word/byte orders, then you will need to create a separate “device” with the same IP address to apply different word/byte settings to those ranges.

  - [Checked = True (High Word First), Unchecked = False (Low Word First)]
- Add a register group [+] – Creates a new register group for the Modbus TCP device, which shows up in the register group list window below.
- Remove a register group [x] – **Removes the selected register group from the Modbus TCP device in the list window.**
- Register Groups – Displays the total count of all register groups for the current TCP device.

  - [Maximum: 500 groups (across all TCP devices)]

#### [Modbus TCP Register Group List Window](/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-tcp-register-group-list-window)

- Register group list window – List of groups of register addresses to be queried on the target device

- Function Code – The red highlighted box in the image above. Specifies which function code this group will read registers from.

  - [1: Read Coils, 2: Read Discrete Inputs, 3: Read Holding Registers and 4: Read Input Registers]
- Register Address – The orange highlighted box in the image above. Specifies the starting register for the group. Enter the first register in the series that you wish to poll. Note: Starting with firmware version 4.2.0, Fend data diodes use Modbus standard 0-based addressing. Meaning the first valid address for any given function code is 0.

  - [0-65535]
- Read Count – The blue highlighted box in the image above. Enter the number of consecutive registers to be read on the device starting from the read register address. For example, a starting register address of 0 and a register read count of 4 will set the diode to poll registers 0 – 3 (inclusive). Depending on the data type selection, only certain intervals are allowed in the count. See Register Group Data Type below. Note: While the Modbus protocol restricts the number of registers in a single polling request to 125. The Modbus register groups in the Fend Diode do not have this same restriction. If a group is configured with a register read count larger than 125 the diode will automatically break up the group into multiple Modbus-compliant requests when polling.

  - [1 - 65535]
- Register Group Data Type –The green highlighted box in the image above. Select the data type of the source data in the selected range. The selection here will restrict the “Consecutive Register Read Count” selection to ensure the correct number of registers is selected. Function codes 1 and 2 support binary values (1 or 0) only. If using function codes 1 or 2 leave the data type on the default selection, “U16”. For function codes 3 and 4, the following data types are supported along with their intervals:

| **Data Type** | **Description** | **Register Read Count Interval** |
| --- | --- | --- |
| U8 | 8-bit Unsigned Integer | 1 |
| S8 | 8-bit Signed Integer | 1 |
| U16 | 16-bit Unsigned Integer | 1 |
| S16 | 16-bit Signed Integer | 1 |
| U32 | 32-bit Unsigned Integer | 2 |
| S32 | 32-bit Signed Integer | 2 |
| U64 | 64-bit Unsigned Integer | 4 |
| S64 | 64-bit Signed Integer | 4 |
| Float32 | 32-bit Floating Point | 2 |
| Float64 | 64-bit Floating Point | 4 |
| String32 | 32-bit String (Max 4 Chars) | 2 |
| String64 | 32-bit String (Max 8 Chars) | 4 |

**Important Note:** In some Modbus addressing approaches the function codes are not explicitly listed. Instead, the different function codes are inferred by using different 1-based non-overlapping register ranges as follows:

- Coil registers (function code 1) span from 00001 to 09999
- Discrete input registers (function code 2) span from 10001 to 19999
- Input registers (function code 4) span from 30001 to 39999
- Holding registers (function code 3) span from 40001 to 49999.

If you are interfacing with a device that uses this addressing approach, you’ll need to translate to explicit function codes and 0-based register addressing.

For example: to address a single 16-bit holding register at “40001”, select function code “3: Read Holding Registers”, set the starting Read Address to “0”, and Read Count to “1”.

## [Modbus TCP Listen](/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-tcp-listen)

For listen mode, no additional settings are required. When the diode is connected to a port mirror or SPAN port that is forwarding an active Modbus networks traffic, the diode will begin forwarding all traffic to the output side. This means basic Modbus data will be available in Fend Cloud or on the output side Modbus slave/server just like that!

However, if you wish to get extra functionality out of the diode you can provide some optional settings.

For protocol conversion setups (i.e. Modbus to Fend Cloud or Modbus to TCP Client JSON) a default blank Modbus Listen setup will deliver JSON that only includes the following register information:

- Target Device IP
- Target Device Unit ID
- Request Function Code
- Request Register Address
- Request Register Raw Value

By entering the configuration of the source Modbus network into the diode as described in the settings overview for [Modbus TCP Master/Client](https://www.opswat.com/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-tcp-masterclient) and in the installation examples shown in [Modbus Installation Instructions](https://www.opswat.com/docs/fenddiode/deployment-examples/modbus-examples), the listen-mode diode will be able to append additional meta data fields to the raw Modbus data including:

- Data Type
- Byte Order
- Word Order
- Converted Value

Please see [Appendix VII: Fend Cloud / TCP JSON Examples](https://www.opswat.com/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples) for output.

## [BACnet IP Listen](/docs/fenddiode/configuration-settings/input-side-protocol-settings#bacnet-ip-listen)

There are no additional settings for BACnet IP Listen at this time.

## [LON Listen](/docs/fenddiode/configuration-settings/input-side-protocol-settings#lon-listen)

There are no additional settings for LON Listen at this time.

## [Modbus RTU Master/Client](/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-rtu-masterclient)

### [Global Modbus RTU Device Settings](/docs/fenddiode/configuration-settings/input-side-protocol-settings#global-modbus-rtu-device-settings)

- Read Timeout – Length of time the diode will wait after receiving a response from the target Modbus device to determine that the message has ended. The Modbus RTU standard prescribes a silent period corresponding to 3.5 characters between each message to determine where one message ends and the next one starts. The length of time corresponding to 3.5 characters varies based on baud rate, but per Modbus spec should never be set lower than 1.75ms. **When configuring the read timeout, start with the default of 2ms.** In most cases, this will be appropriate. If you are experiencing errors, or the diode is having trouble reading the data properly, see the table below for suggested settings. If a device does not adhere to Modbus spec, timings may be different.

  - [1 – 20, in increments of 1 millisecond]
  - Baud Rate Suggested Timing (for 3.5 Characters)

    - 9600 - 4ms
    - 19200 - 2ms
    - 38400 - 2ms
    - 57600 - 2ms
    - 115200 - 2ms
- Transmit Timeout – Length of time the diode will wait to receive a response from the target Modbus device before timing out. Specifically, this is how long the diode will wait after transmitting a request to receive the first byte of the response.

  - [1 – 32,000, in increments of 1 millisecond]
- Polling –Time interval that diode waits between polling events.

  - [1 -999, in seconds]
- Add a device [+] – Creates a new Modbus RTU device which shows up in the device list window below. Double click on the newly listed device to configure it. See the next section Individual Modbus RTU Device Settings.

  - [Maximum: 32 devices]
- Remove a device [x] – Removes the last (bottom-most) Modbus RTU device in the list window.
- Devices – Displays the total count of configured Modbus RTU devices.

  - [0 – 32]
- Register Groups – Displays the total count of configured register groups across all RTU devices.

  - [0 – 500]
- Registers – Displays the total count of configured registers across all groups on all RTU devices.

  - [0 – 40,000]
- Device list window - A list of RTU devices that are being monitored by the diode. Double click on a device entry in the list to configure that device.

### [Individual Modbus RTU Device Settings](/docs/fenddiode/configuration-settings/input-side-protocol-settings#individual-modbus-rtu-device-settings)

- Device UID – Fend assigned unique ID for the Modbus device. This number is used internally by the diode to track Modbus devices.

  - [0 – 65535]
- Target Modbus Unit ID – The unit Modbus ID of the target Modbus device to be monitored

  - [1 - 255]
- Unit ID Mapping Enabled – Enable or disable remapping Modbus unit ID’s when sent through the diode. With this feature you can give a Modbus device a different Modbus unit ID on the output side of the diode than it has on the input side network.

  - [Enabled, Disabled]
- Map ID – The new Modbus unit ID to be assigned on the output side of the data diode for this device.

  - [1-255]
- High Word First – Specifies the word order of the source data for the Modbus device. Applies to all register groups listed for the device. If you have register ranges on a single device with differing word/byte orders, then you will need to create a separate “device” with the same IP address to apply different word/byte settings to those ranges.

  - [Checked = True (High Word First), Unchecked = False (Low Word First)]
- High Byte First – Specifies the byte order of the source data for the Modbus device. Applies to all register groups listed for the device. If you have register ranges on a single device with differing word/byte orders, then you will need to create a separate “device” with the same IP address to apply different word/byte settings to those ranges.

  - [Checked = True (High Word First), Unchecked = False (Low Word First)]
- Add a register group [+] – Creates a new register group for the Modbus RTU device, which shows up in the register group list window below.
- Remove a register group [x] – Removes the selected register group from the Modbus RTU device in the list window.
- Register Groups – Total count of register groups for the current device.

  - [Maximum: 500 groups (across all RTU devices)]

#### [Modbus RTU Register Group List Window](/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-rtu-register-group-list-window)

- Register group list window – List of groups of register addresses to be queried on the target device
- Function Code – The red highlighted box in the image above. Specifies which function code this group will read registers from.

  - [1: Coils, 2: Discrete Inputs, 3: Holding Registers and 4: Input Registers]
- Register Address – The orange highlighted box in the image above. Specifies the starting register for the group. Enter the first register in the series that you wish to poll. Note: Starting with firmware version 4.2.0, Fend data diodes use Modbus standard 0-based addressing. Meaning the first valid address for any given function code is 0.

  - [0-65535]
- Read Count – The blue highlighted box in the image above. Enter the number of consecutive registers to be read on the device starting from the read register address. For example, a starting register of 0 and a register read count of 4 will set the diode to poll registers 0 – 3 (inclusive). Depending on the data type selection, only certain intervals are allowed in the count. See Register Group Data Type below. Note: While the Modbus protocol restricts the number of registers in a single polling request to 125. The Modbus register groups in the Fend Diode do not have this same restriction. If a group is configured with a register read count larger than 125 the diode will automatically break up the group into multiple Modbus compliant requests when polling.

  - [1 - 65535]
- Register Group Data Type – The green highlighted box in the image above. Select the data type of the source data in the selected range. The selection here will restrict the “Consecutive Register Read Count” selection to ensure the correct number of registers is selected. Function codes 1 and 2 support binary values (1 or 0) only. If using function codes 1 or 2 leave the data type on the default selection, “U16”. For function codes 3 and 4, the following data types are supported along with their intervals:

| **Data Type** | **Description** | **Register Read Count Interval** |
| --- | --- | --- |
| U8 | 8-bit Unsigned Integer | 1 |
| S8 | 8-bit Signed Integer | 1 |
| U16 | 16-bit Unsigned Integer | 1 |
| S16 | 16-bit Signed Integer | 1 |
| U32 | 32-bit Unsigned Integer | 2 |
| S32 | 32-bit Signed Integer | 2 |
| U64 | 64-bit Unsigned Integer | 4 |
| S64 | 64-bit Signed Integer | 4 |
| Float32 | 32-bit Floating Point | 2 |
| Float64 | 64-bit Floating Point | 4 |
| String32 | 32-bit String (Max 4 Chars) | 2 |
| String64 | 32-bit String (Max 8 Chars) | 4 |

## [Modbus RTU Listen](/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-rtu-listen)

For listen mode, no additional settings are required. When the diode is connected to a port mirror or SPAN port that is forwarding an active Modbus networks traffic, the diode will begin forwarding all traffic to the output side. This means Modbus data will be available in Fend Cloud or on the output side’s Modbus Slave just like that! However, if you wish to get extra functionality out of the diode you can provide some optional settings.

For protocol conversion setups (i.e. Fend Cloud or TCP Client JSON Protocol Conversion) a default blank Modbus Listen setup will deliver JSON that only includes the following register information:

- Target Device Unit ID
- Request Function Code
- Request Register Address
- Request Register Raw Value

By entering the configuration of the source Modbus network into the diode as described in the settings overview for [Modbus RTU Master/Client](https://www.opswat.com/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-rtu-masterclient) and in the installation examples shown in [Modbus Installation Instructions](https://www.opswat.com/docs/fenddiode/deployment-examples/modbus-examples), the listen-mode diode will be able to append additional meta data fields to the raw Modbus data including:

- Data Type
- Byte Order
- Word Order
- Converted Value

Please see [Appendix VII: Fend Cloud / TCP JSON Examples](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples) for output.

## [BACnet MSTP Listen](/docs/fenddiode/configuration-settings/input-side-protocol-settings#bacnet-mstp-listen)

There are no additional settings for BACnet MSTP Listen at this time.
