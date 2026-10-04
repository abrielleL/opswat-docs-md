<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/bacnet-examples -->

# BACnet Examples

## [Network/System Requirements](/docs/fenddiode/deployment-examples/bacnet-examples#networksystem-requirements)

The Fend Diode currently supports listen mode for BACnet networks. Listen mode gathers all supported traffic passing over a network and sends it through the diode to a designated MQTT, Fend Cloud, or TCP server endpoint. For a list of BACnet commands currently supported see [Appendix IV: List of Supported BACnet Commands](https://www.opswat.com/docs/fenddiode/appendices/appendix-iv-list-of-supported-bacnet-commands). To install a diode in BACnet listen mode, the BACnet network traffic needs to be port mirrored to the input side of the diode, as follows:

## [Example 1: Diode Settings for BACnet Listen Mode to Local TCP Server](/docs/fenddiode/deployment-examples/bacnet-examples#example-1-diode-settings-for-bacnet-listen-mode-to-local-tcp-server)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/bacnet-examples#diode-input-side-settings)

To configure the diode in BACnet listen mode, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.
4. Under Input Side -> Protocol Settings -> Select BACnet IP from the dropdown.

### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/bacnet-examples#diode-output-side-settings)

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using a static IP:

   1. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the network.

Under Output Side -> Protocol Settings -> Select TCP Client (JSON Protocol Conversion) from the dropdown and set the following:

1. “Target IP Address” will be the IP Address of the computer running the Fend TCP Server Tool.
2. “Target Port” will be the port number set in the Fend TCP Server Tool.
3. For additional information on setting up the Fend TCP Server Tool see [**Fend TCP Server Tool Instructions**](https://www.opswat.com/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#setting-up-the-fend-tcp-server-tool).

Finally, when done updating all settings **press the “Save & Exit” button** located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/bacnet-examples#installing-the-data-diode-after-configuration)

1. See [**Fend TCP Server Tool Instructions**](https://www.opswat.com/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#setting-up-the-fend-tcp-server-tool) for details about setting up the Server Tool.
2. Connect the diode’s input side to the mirrored port on the BACnet network.
3. Connect the diode’s output side to the computer or network containing the computer running the TCP Server Tool.
4. Plug in power to both sides of the diode.
5. Verify data is received on the outbound network.

## [Example 2: Diode Settings for BACnet Listen Mode to Fend Cloud](/docs/fenddiode/deployment-examples/bacnet-examples#example-2-diode-settings-for-bacnet-listen-mode-to-fend-cloud)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/bacnet-examples#diode-input-side-settings)

To configure the diode in BACnet listen mode, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select BACnet IP Listen from the dropdown and set the following:

4. Set the “Protocol Mode” dropdown to “Listen”

### [Diode Output Side Settings (Ethernet)](/docs/fenddiode/deployment-examples/bacnet-examples#diode-output-side-settings-ethernet)

If you are a Fend Cloud subscriber, you can send BACnet data to the Fend AWS Cloud using the following settings:

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network
2. Set the DNS Server to 1.1.1.1 or to a DNS server of your choice
3. Set the NTP Server time.nist.gov or to a DNS server of your choice

Under Output Side -> Protocol Settings -> Select Fend Cloud from the dropdown and set the following fields:

4. Set the Publish Cycle Time interval to 1 second

Finally, when done updating all settings **press the “Save & Exit”** button located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Diode Output Side Settings (Cellular)](/docs/fenddiode/deployment-examples/bacnet-examples#diode-output-side-settings-cellular)

Fend data diodes are able to be used in cellular mode only if they have a Fend Cloud subscription. To enable a diode for cellular usage, select “Cellular” under Output Side > Interface Settings. The protocol settings are preconfigured from Fend, and will be ready for use when cellular is selected. For Cellular outbound, see [Configuring a Diode for Cellular Communication](https://www.opswat.com/docs/fenddiode/deployment-examples/configuring-a-diode-for-cellular-communication).

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/bacnet-examples#installing-the-data-diode-after-configuration)

1. Connect BACnet source network to the input side of the diode with an ethernet cable.
2. Connect the destination network (with internet access) to the output side of the diode with an ethernet cable.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing into AWS using your Fend web app login.

## [Example 3: Diode Settings for BACnet Listen Mode to MQTT Publisher](/docs/fenddiode/deployment-examples/bacnet-examples#example-3-diode-settings-for-bacnet-listen-mode-to-mqtt-publisher)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/bacnet-examples#diode-input-side-settings)

To configure the diode in BACnet listen mode, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select BACnet IP Listen from the dropdown and set the following:

4. Set the “Protocol Mode” dropdown to “Listen”

### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/bacnet-examples#diode-output-side-settings)

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

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/bacnet-examples#installing-the-data-diode-after-configuration)

1. Connect BACnet source network to the input side of the diode with an ethernet cable.
2. Connect the destination network, with access to the target broker, to the output side of the diode with an ethernet cable.
3. Plug in power to both sides of the diode.
4. Confirm that data is arriving at your destination broker.
