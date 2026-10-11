<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/modbus-examples -->

# Modbus Examples

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [General](/docs/fenddiode/deployment-examples/modbus-examples#general)

The Fend Data Diode is capable of communicating directly with Modbus RTU and TCP devices. There are many different ways one can set up the diode, just as there are many ways to set up a Modbus network. This section will provide an overview of the many possible Modbus setups and provides instructions for specific examples. The Fend Data Diode supports the following configuration modes, which are detailed further below.

## [Input Side Options](/docs/fenddiode/deployment-examples/modbus-examples#input-side-options)

The input side of the Fend Data Diode has two ways of communicating with your Modbus network.

### [Option 1: Modbus Master/Client Mode](/docs/fenddiode/deployment-examples/modbus-examples#option-1-modbus-masterclient-mode)

In Master/Client mode the input side of the diode acts as a Modbus Master/Client and actively polls Modbus devices on the target network. **Important Note: Modbus RTU** ***serial*** **networks cannot have more than one active master on the network at a time. If there is another master on a serial Modbus RTU network, you must use Listen mode (see below). This does** ***not*** **apply to Modbus TCP.**

### [Option 2: Listen Mode (Passive Tap)](/docs/fenddiode/deployment-examples/modbus-examples#option-2-listen-mode-passive-tap)

Listen mode requires a tapped connection (or port mirror) from an existing Modbus network with its own active Modbus Clients and Servers to send data to the diode. The traffic is passively captured and then forwarded by the diode.

## [Output Side Options](/docs/fenddiode/deployment-examples/modbus-examples#output-side-options)

### [Option 1: Modbus Slave/Server](/docs/fenddiode/deployment-examples/modbus-examples#option-1-modbus-slaveserver)

In this mode the output side of the diode is acting as a Modbus Slave/Server holding data and waiting to be polled by a Modbus Master/Client on the outside network. This operating mode can be used with input side Master/Client or Listen modes. This allows the flexibility of interacting with the Modbus network, or passively creating a gateway to the network. Here are two diagrams outlining these configurations:

### [Option 2: Modbus Protocol Converter - MQTT Publisher, TCP Client (JSON Protocol Conversion), or Fend Cloud](/docs/fenddiode/deployment-examples/modbus-examples#option-2-modbus-protocol-converter---mqtt-publisher-tcp-client-json-protocol-conversion-or-fend-cloud)

In protocol conversion mode, the output side of the diode is converting the original Modbus data into a JSON format to be sent to Fend Cloud, over MQTT Publisher, or to a local TCP server for logging. This operating mode can be used with input side Master/Client (Request/Response) or Listen modes. Here are two diagrams outlining these configurations:

## [Fend Diode Modbus Compatibility](/docs/fenddiode/deployment-examples/modbus-examples#fend-diode-modbus-compatibility)

The Fend Data Diode currently supports function codes 1, 2, 3, and 4 along with the following variable types:

| Data Type | Description |
| --- | --- |
| U8 | 8-bit Unsigned Integer |
| S8 | 8-bit Signed Integer |
| U16 | 16-bit Unsigned Integer |
| S16 | 16-bit Signed Integer |
| U32 | 32-bit Unsigned Integer |
| S32 | 32-bit Signed Integer |
| U64 | 64-bit Unsigned Integer |
| S64 | 64-bit Signed Integer |
| Float32 | 32-bit Floating Point |
| Float64 | 64-bit Floating Point |
| String32 | 32-bit String (Max 4 Chars) |
| String64 | 32-bit String (Max 8 Chars) |

Note: Function codes 1 and 2 support binary states (1 or 0) only. If using function codes 1 or 2 leave the data type on the default selection, “U16”.

## [Modbus Master/Client Setup Examples](/docs/fenddiode/deployment-examples/modbus-examples#modbus-masterclient-setup-examples)

When setting up a diode for Modbus Master/Client mode please use the following table for the number of devices, groups and registers supported.

[Appendix I: Modbus Polling Cycle Timings](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol#modbus-polling-cycle-timings)

### [Example 1: Diode Settings for Modbus TCP Master/Client to Fend Cloud (AWS)](/docs/fenddiode/deployment-examples/modbus-examples#example-1-diode-settings-for-modbus-tcp-masterclient-to-fend-cloud-aws)

#### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-input-side-settings)

To configure the diode to act as a Modbus TCP controller, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select Modbus TCP Master/Client from the dropdown and set the following:

1. Check the “Read/Transmit Timeout” setting. This is the length of time the diode will wait for a response from the target Modbus device before timing out. The default value is 100msec. Change as needed.
2. Set the polling time (how often the diode will request updated values from the targeted Modbus devices) using the **AWS Publish Cycle Timings** found in [**Appendix I: Recommended Transfer Timings by Protocol**](https://www.opswat.com/docs/fenddiode/appendices/appendix-i-recommended-transfer-timings-by-protocol)**.**
3. Click the green plus symbol to add a target Modbus device for monitoring. Up to 32 devices are supported.
4. A new item will be listed below that will look similar to “01 1 192.168.1.100 (0)”. Double click it to configure the device. A new window will appear.
5. In the “Target Modbus Unit ID” field, enter in the target Modbus Unit ID.
6. If you wish to re assign the Unit ID of the target Modbus device, so it appears differently on the output side of the diode, you can do so via the Mapping Enabled option. Enable this setting and assign a ‘Map ID’ which will be the new Modbus Unit ID in the Modbus JSON data delivered to Fend Cloud.
7. Enter the target Modbus device’s IP address in the “Target IP Address” field.
8. Set the byte order and word order settings.
9. Clicking the green plus button below “IP” will add a new register group for the open device. There can be a maximum of 500 register groups across all devices.

10. There are four modifiable group fields. First is the function code, followed by the starting read register, the number of consecutive registers to poll starting at the starting read register value and last is the data type for the variable. Note: Modbus register address’ are 0-based. Meaning the first valid address for any given function code is 0.
11. After editing the range value, the starting register field will change accordingly to display the full range. Each device group allows up to 65535 registers. Note: All registers in a given group must all be valid registers or the call will fail. For example, if the target device has registers 0-999 and 2000 to 2999, a group with a starting address of 0 and a read count of 3000 would not work because registers 1000 to 1999 would be invalid. To successfully poll this set of registers, you would make two separate groups: One with a starting address of 0 and a read count of 1000 and a second with a starting address of 2000 and a read count of 1000.
12. Select the appropriate data type for the range. Note: If there is more than one data type on the device use a separate register group for each data type
13. Click “Ok” to accept the changes.

#### [Diode Output Side Settings (Ethernet)](/docs/fenddiode/deployment-examples/modbus-examples#diode-output-side-settings-ethernet)

If you are a Fend Cloud subscriber, you can send Modbus data to the Fend AWS Cloud using the following settings:

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network
2. Set the DNS Server to 1.1.1.1 or a DNS server of your choice
3. Set the NTP Server time.nist.gov or to a DNS server of your choice

Under Output Side -> Protocol Settings -> Select Fend Cloud from the dropdown and set the following fields:

1. Set the Publish Cycle Time interval to 1 second

Finally, when done updating all settings press the “Save & Exit” button located at the top right of the Diode Web Configuration tool to close your session and allow the diode to reboot to ensure the new settings are loaded.

#### [Diode Output Side Settings (Cellular)](/docs/fenddiode/deployment-examples/modbus-examples#diode-output-side-settings-cellular)

Fend data diodes are able to be used in cellular mode only if they have a Fend Cloud subscription. To enable a diode for cellular usage, select “Cellular” under Output Side > Interface Settings. The protocol settings are preconfigured from Fend, and will be ready for use when cellular is selected. For Cellular outbound, see [Configuring a Diode for Cellular Communication](https://www.opswat.com/docs/fenddiode/deployment-examples/configuring-a-diode-for-cellular-communication).

#### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/modbus-examples#installing-the-data-diode-after-configuration)

1. Connect Modbus source network to the input side of the diode with an ethernet cable.
2. Connect the destination network (with internet access) to the output side of the diode with an ethernet cable.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing into AWS using your Fend web app login.

### [Example 2: Diode Settings for Modbus TCP Master/Client to Modbus TCP Slave/Server](/docs/fenddiode/deployment-examples/modbus-examples#example-2-diode-settings-for-modbus-tcp-masterclient-to-modbus-tcp-slaveserver)

#### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-input-side-settings)

To configure the diode to act as a Modbus TCP master/client, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select Modbus TCP Master/Client from the dropdown and set the following:

1. Check the “Read/Transmit Timeout” setting. This is the length of time the diode will wait for a response from the target Modbus device before timing out. The default value is 100msec. Change as needed.
2. Set the polling time (how often the diode will request updated values from the targeted Modbus devices).
3. Click the green plus symbol to add a target Modbus device for monitoring. Up to 32 devices are supported.
4. A new item will be listed below that will look similar to “01 1 192.168.1.100 (0)”. Double click it to configure the device. A new window will appear.
5. In the “Target Modbus Unit ID” field, enter in the target Modbus device ID.
6. If you wish to re assign the Unit ID of the target Modbus device, so it appears differently on the output side of the diode, you can do so via the Mapping Enabled option. Enable this setting and assign a ‘Map ID’ which will be the new Modbus Unit ID used for accessing the device data on from the output side Modbus Slave.
7. Enter the target Modbus device’s IP address in the “Target IP Address” field.
8. Set the byte order and word order settings.
9. Clicking the green plus button below “IP” will add a new register group for the open device. There can be a maximum of 500 register groups across all devices.
10. There are four modifiable group fields. First is the function code, followed by the starting read register, the number of consecutive registers to poll starting at the starting read register value and last is the data type for the variable. Note: Modbus register address’ are 0-based. Meaning the first valid address for any given function code is 0.
11. After editing the range value, the starting register field will change accordingly to display the full range. Each device group allows up to 65535 registers. Note: All registers in a given group must all be valid registers or the call will fail. For example, if the target device has registers 0-999 and 2000 to 2999, a group with a starting address of 0 and a read count of 3000 would not work because registers 1000 to 1999 would be invalid. To successfully poll this set of registers, you would make two separate groups: One with a starting address of 0 and a read count of 1000 and a second with a starting address of 2000 and a read count of 1000.
12. Select the appropriate data type for the range. Note: If there is more than one data type on the device use a separate register group for each data type
13. Click “Ok” to accept the changes.

**Please note: Step 6 above is important. When the output side of the diode is in Modbus mode, the diode is acting as a Modbus gateway. So, the data from the Modbus devices on the input side network will not be addressable by their IP addresses. Therefore, the Modbus devices must have unique device IDs for the data to be available on the output side.** For example, if you have two Modbus devices at 192.168.1.11 and 192.168.1.12 and each have 1 register at location 40001 and the output side of your diode is set to IP address 192.168.1.50. The Modbus device connecting to the output side of the diode will only see the new IP of the diode when it polls and will not be able to see the original IP addresses. So in order to differentiate between the register on the device at 192.168.1.11 and at 192.168.1.12, you’ll need to assign 192.168.1.11 a Device ID of 1 and 192.168.1.12 a device ID of 2 (or something similar). This will result in the diode holding both registers at 192.168.1.50 for device 1, 40001 and device 2, 40001. Alternatively, you can use unique non-overlapping register rangers across all input devices.

Additionally, with the output side of the diode in Modbus mode, exception codes generated on the input side network will be reflected on the output side of the diode for the devices polling it. For example, if the input side polls a device and the device returns exception code 2 (illegal address), a polling request of the same type made to the output side will result in the same exception code. All Modbus codes will be passed along exactly as they are from the input side, with a notable distinction for exception code 10. This code has been chosen to indicate that the input side of the diode is in a non-operational state. This might occur, for example, if the input side of the diode has lost power.

#### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-output-side-settings)

To set up the output side of the diode as a Modbus TCP slave/server device, do the following:

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network

Under **Output Side -> Protocol Settings -> Select Modbus TCP** from the dropdown and set the following fields:

1. Enter the socket timeout for the diode output side Modbus slave device. This sets the length of time before an idle Modbus client connection will be logged out of the diode’s output side Modbus server.

Finally, when done updating all settings **press the “Save & Exit”** button located at the top right of the Diode Web Configuration tool to close your session and allow the diode to reboot to ensure the new settings are loaded.

#### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/modbus-examples#installing-the-data-diode-after-configuration)

1. Connect primary Modbus network (source) to the input side of the diode with an ethernet cable.
2. Connect the output side of the diode to the secondary Modbus network.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing from the primary network to the secondary network.

### [Example 3: Diode Settings for Modbus TCP Master/Client to MQTT Publisher](/docs/fenddiode/deployment-examples/modbus-examples#example-3-diode-settings-for-modbus-tcp-masterclient-to-mqtt-publisher)

#### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-input-side-settings)

To configure the diode to act as a Modbus TCP master/client, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select Modbus TCP Master/Client from the dropdown and set the following:

1. Check the “Read/Transmit Timeout” setting. This is the length of time the diode will wait for a response from the target Modbus device before timing out. The default value is 100msec. Change as needed.
2. Set the polling time (how often the diode will request updated values from the targeted Modbus devices).
3. Click the green plus symbol to add a target Modbus device for monitoring. Up to 32 devices are supported.
4. A new item will be listed below that will look similar to “01 1 192.168.1.100 (0)”. Double click it to configure the device. A new window will appear.
5. In the “Target Modbus Unit ID” field, enter in the target Modbus device ID.
6. If you wish to re assign the Unit ID of the target Modbus device, so it appears differently on the output side of the diode, you can do so via the Mapping Enabled option. Enable this setting and assign a ‘Map ID’ which will be the new Modbus Unit ID used for accessing the device data on from the output side Modbus Slave.
7. Enter the target Modbus device’s IP address in the “Target IP Address” field.
8. Set the byte order and word order settings.
9. Clicking the green plus button below “IP” will add a new register group for the open device. There can be a maximum of 500 register groups across all devices.
10. There are four modifiable group fields. First is the function code, followed by the starting read register, the number of consecutive registers to poll starting at the starting read register value and last is the data type for the variable. Note: Modbus register address’ are 0-based. Meaning the first valid address for any given function code is 0.
11. After editing the range value, the starting register field will change accordingly to display the full range. Each device group allows up to 65535 registers. Note: All registers in a given group must all be valid registers or the call will fail. For example, if the target device has registers 0-999 and 2000 to 2999, a group with a starting address of 0 and a read count of 3000 would not work because registers 1000 to 1999 would be invalid. To successfully poll this set of registers, you would make two separate groups: One with a starting address of 0 and a read count of 1000 and a second with a starting address of 2000 and a read count of 1000.
12. Select the appropriate data type for the range. Note: If there is more than one data type on the device use a separate register group for each data type
13. Click “Ok” to accept the changes.

#### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-output-side-settings)

To set up the output side of the diode as an MQTT Publisher, do the following:

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network

Under **Output Side -> Protocol Settings -> Select MQTT Publisher** from the dropdown and set the following fields:

1. Configure the Publishers Client ID. This needs to be unique to the broker you are connecting to. If there is an overlap, the broker will kick the diode. **NOTE**: when using the industrial protocol to json conversion feature, this Client ID will be present in the delivered JSON. Use this field to assign an identifiable key. See [Appendix VII: Industrial Protocol to JSON Conversion Examples](/docs/fenddiode/appendices/appendix-vii-fend-cloud---tcp-json-examples) for more detail.
2. Set the IP address or hostname of the target broker IP. Hostname requires the output side DNS Server to be set, or the output side to be in DHCP mode.
3. Set the Broker Port to the listening port of the broker.
4. Configure the Keep Alive as needed. This sets the max idle time the publisher can be connected to the broker before being kicked.
5. Configuring the Authentication/Encryption properly is important. This will be dependent on how your broker is configured. We support the following authentication methods:

   1. None
   2. User/Password.
   3. Server Authentication.
   4. Mutual Authentication.
   5. TLS-PSK.
   6. User/Password + Server Auth.
   7. User/Password + Mutual Auth.
   8. User/Password + TLS-PSK.
6. If you are using an authentication with Username and Password, configure the user and password.
7. If you are using an authentication with TLS PSK, configure your pre-shared key and id.
8. Configure a connect delay as needed. Default is 2 seconds.
9. Set the MQTT version. 3.1.1 recommended.
10. Check whether you want the diode to connect to the broker with a fresh/clean session or not.
11. Set the aggregate topic now.
12. Set the Quality of Service for the aggregate topic now.

#### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/modbus-examples#installing-the-data-diode-after-configuration)

1. Connect Modbus source network to the input side of the diode with an ethernet cable.
2. Connect the destination network, with access to the target broker, to the output side of the diode with an ethernet cable.
3. Plug in power to both sides of the diode.
4. Confirm that data is arriving at your destination broker.

## [Modbus Listen Mode Examples](/docs/fenddiode/deployment-examples/modbus-examples#modbus-listen-mode-examples)

### [Diode Input Options](/docs/fenddiode/deployment-examples/modbus-examples#diode-input-options)

A diode in listen mode on the input is able to capture all traffic in a Modbus network unobtrusively. For RTU devices this can be achieved through tapping the serial lines. In the case of Modbus TCP, the Modbus network will need to be port mirrored for the diode to capture the data. All traffic from the Modbus controller and devices will be captured by the diode and sent to its destination on the world side.

For the best results, the input side of the diode will need to be configured with the Modbus network topology. If the input side of the diode is set to Modbus Listen mode with output side set to Fend Cloud or JSON conversion and no Modbus network configuration is given, the output data will be sent as raw hexadecimal only. In order to provide data types and final calculated values you must setup the diode in a similar manner to Master/Client (Request/Response) mode as outlined in [Example 3](https://www.opswat.com/docs/fenddiode/deployment-examples/modbus-examples#example-3-diode-settings-for-modbus-tcp-listen-mode-to-local-tcp-server---tcp-client-json-protocol-conversion) below.

### [Diode Output Options](/docs/fenddiode/deployment-examples/modbus-examples#diode-output-options)

With the input side in Listen mode, the diode can output the data in one of three formats:

1. The output side of the diode can act as a Modbus device on an external Modbus network, essentially “passing-through” the data to another Modbus controller. In this mode, an external Modbus controller can poll the diode and request the Modbus data being sent across the diode from the protected network
2. The output side of the diode can act as a protocol converter, converting the original Modbus data into JSON format and send that JSON to an external TCP server for logging.
3. The output side of the diode can convert the original Modbus data into JSON format and send that JSON over MQTT to the Fend AWS Cloud for access via API.

### [Example 4: Diode Settings for Modbus TCP Listen Mode to Local TCP Server - TCP Client (JSON Protocol Conversion)](/docs/fenddiode/deployment-examples/modbus-examples#example-4-diode-settings-for-modbus-tcp-listen-mode-to-local-tcp-server---tcp-client-json-protocol-conversion)

#### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-input-side-settings)

To configure the diode in Modbus listen mode, start with the input-side diode settings

Under **Input Side -> Interface Settings** select the Ethernet radio button and set the following:

1. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
2. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under **Input Side -> Protocol Settings -> Select Modbus TCP/IP Listen** from the dropdown and set the following:

1. Check the “Read/Transmit Timeout” setting. This is the length of time the diode will wait for a response from the target Modbus device before timing out. The default value is 100msec. Change as needed.
2. Click the green plus symbol to add a target Modbus device for monitoring. Up to 32 devices are supported.
3. A new item will be listed below that will look similar to “01 1 192.168.1.100 (0)”. Double click it to configure the device. A new window will appear.
4. In the “Target Modbus Unit ID” field, enter in the target Modbus Unit ID.
5. If you wish to re assign the Unit ID of the target Modbus device, so it appears differently on the output side of the diode, you can do so via the Mapping Enabled option. Enable this setting and assign a ‘Map ID’ which will be the new Modbus Unit ID in the Modbus JSON data delivered to your TCP Server.
6. Enter the target Modbus device’s IP address in the “Target IP Address” field.
7. Set the byte order and word order settings.
8. Clicking the green plus button below “IP” will add a new register group for the open device. There can be a maximum of 500 register groups for across all devices. There are four modifiable group fields. First is the function code, followed by the starting read register, the number of consecutive registers to poll starting at the starting read register value and last is the data type for the variable. Note: Modbus register address’ are 0-based. Meaning the first valid address for any given function code is 0.
9. After editing the range value, the starting register field will change accordingly to display the full range. Each device group allows up to 65535 registers. Note: All registers in a given group must all be valid registers or the call will fail. For example, if the target device has registers 0-999 and 2000 to 2999, a group with a starting address of 0 and a read count of 3000 would not work because registers 1000 to 1999 would be invalid. To successfully poll this set of registers, you would make two separate groups: One with a starting address of 0 and a read count of 1000 and a second with a starting address of 2000 and a read count of 1000.
10. Select the appropriate data type for the range. Note: If there is more than one data type on the device use a separate register group for each data type
11. Click “Ok” to accept the changes.

#### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-output-side-settings)

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using a static IP:

   1. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the network.

Under Output Side -> Protocol Settings -> Select TCP Client (JSON Protocol Conversion) from the dropdown and set the following:

1. “Target IP Address” will be the IP Address of the computer running the Fend TCP Server Tool.
2. “Target Port” will be the port number set in the Fend TCP Server Tool.
3. For additional information on setting up the Fend TCP Server Tool see [Fend TCP Server Tool Instructions](https://www.opswat.com/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#setting-up-the-fend-tcp-server-tool).

Finally, when done updating all settings press the “Save & Exit” button located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

#### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/modbus-examples#installing-the-data-diode-after-configuration)

1. See [Fend TCP Server Tool Instructions](https://www.opswat.com/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#setting-up-the-fend-tcp-server-tool) for details about setting up the Server Tool.
2. Connect the diode’s input side to the mirrored port on the Modbus network.
3. Connect the diode’s output side to the computer or network containing the computer running the TCP Server Tool.
4. Plug in power to both sides of the diode.
5. Verify data is received on the outbound network.

### [Example 5: Diode Settings for Modbus RTU Listen Mode to Modbus TCP Slave/Server (Modbus RTU to IP Conversion)](/docs/fenddiode/deployment-examples/modbus-examples#example-5-diode-settings-for-modbus-rtu-listen-mode-to-modbus-tcp-slaveserver-modbus-rtu-to-ip-conversion)

#### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-input-side-settings)

To configure the diode in Modbus RTU listen mode, start with the input-side diode settings

Under **Input Side -> Interface Settings** select the RS485 radio button and set the following:

1. Set the Baud rate of the diode to match the baud rate of the existing Modbus RTU network.
2. Set the parity, data bits, and stop bits to match the existing Modbus RTU network. The standard defaults for Modbus RTU are:

   1. Parity: Odd
   2. Data Bits: 8
   3. Stop Bits: 1

Under **Input Side -> Protocol Settings -> Select Modbus RTU Listen** from the dropdown and set the following:

1. Check the “Read Timeout” setting. This is the length of time the diode will wait after receiving the last byte of a response from a Modbus device to determine that the message has ended. The default value Modbus RTU is 2ms. Change as needed to match your network settings.
2. Check the "Transmit Timeout" setting. This is the length of time the diode will wait after seeing a Modbus request to receive a response from the target Modbus device before timing out. The default value Modbus RTU is 200ms. Change as needed to match your network settings.
3. The "Polling" setting is not used in listen mode.
4. Click the green plus symbol to add a target Modbus device for monitoring. Up to 32 devices are supported.
5. A new item will be listed below that will look similar to “1 | 1 | (0)”. Double click it to configure the device. A new window will appear.
6. In the “Target Modbus Unit ID” field, enter in the target Modbus Unit ID.
7. If you wish to re assign the Unit ID of the target Modbus device, so it appears differently on the output side of the diode, you can do so via the Mapping Enabled option. Enable this setting and assign a ‘Map ID’ which will be the new Modbus Unit ID in the Modbus JSON data delivered to your TCP Server.
8. Set the byte order and word order settings.
9. Clicking the green plus button will add a new register group for the open device. There can be a maximum of 500 register groups for across all devices. There are four modifiable group fields. First is the function code, followed by the starting read register, the number of consecutive registers to poll starting at the starting read register value and last is the data type for the variable. Note: Modbus register address’ are 0-based. Meaning the first valid address for any given function code is 0.
10. After editing the range value, the starting register field will change accordingly to display the full range. Each device group allows up to 65535 registers. Note: All registers in a given group must all be valid registers or the call will fail. For example, if the target device has registers 0-999 and 2000 to 2999, a group with a starting address of 0 and a read count of 3000 would not work because registers 1000 to 1999 would be invalid. To successfully poll this set of registers, you would make two separate groups: One with a starting address of 0 and a read count of 1000 and a second with a starting address of 2000 and a read count of 1000.
11. Select the appropriate data type for the range. Note: If there is more than one data type on the device use a separate register group for each data type
12. Click “Ok” to accept the changes.

#### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/modbus-examples#diode-output-side-settings)

To set up the output side of the diode as a Modbus TCP slave/server device, do the following:

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network

Under **Output Side -> Protocol Settings -> Select Modbus TCP** from the dropdown and set the following fields:

1. Enter the socket timeout for the diode output side Modbus slave device. This sets the length of time before an idle Modbus client connection will be logged out of the diode’s output side Modbus server.

Finally, when done updating all settings **press the “Save & Exit”** button located at the top right of the Diode Web Configuration tool to close your session and allow the diode to reboot to ensure the new settings are loaded.

#### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/modbus-examples#installing-the-data-diode-after-configuration)

1. Connect primary Modbus network (source) to the input side of the diode with an ethernet cable.
2. Connect the output side of the diode to the secondary Modbus network.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing from the primary network to the secondary network.

## [Modbus Frequently Asked Questions](/docs/fenddiode/deployment-examples/modbus-examples#modbus-frequently-asked-questions)

### [Q: Why am I getting intermittent polling requests with timeouts in Modbus RTU serial mode?](/docs/fenddiode/deployment-examples/modbus-examples#q-why-am-i-getting-intermittent-polling-requests-with-timeouts-in-modbus-rtu-serial-mode)

A: After checking your device configuration and verifying that the Device ID, register addresses, and timeouts are all correct as outlined in [**Fend Diode Modbus Compatibility**](https://www.opswat.com/docs/fenddiode/deployment-examples/modbus-examples#fend-diode-modbus-compatibility) and [**Modbus RTU Settings**](https://www.opswat.com/docs/fenddiode/configuration-settings/input-side-protocol-settings#modbus-rtu-masterclient), please also ensure that only one RTU master is present on the serial network at a time. Modbus RTU serial networks cannot have more than one active master on the network at a time. If there is another master on a serial Modbus RTU network, you must use the data diode in Listen mode. This does not apply to Modbus TCP networks.

### [Q: When using the Fend diode for Modbus TCP data, how many unique Modbus TCP clients can connect to the output side Modbus server on the diode to collect data?](/docs/fenddiode/deployment-examples/modbus-examples#q--when-using-the-fend-diode-for-modbus-tcp-data-how-many-unique-modbus-tcp-clients-can-connect-to-the-output-side-modbus-server-on-the-diode-to-collect-data)

A: The Modbus server on the output side of the diode allows a single connection at a time. If you wish to have more than one client request data from the output side, each client must disconnect when it has finished polling the diode. If multiple clients try to connect at the same time, the first will connect and the others will receive a timeout error while the first diode remains connected.
