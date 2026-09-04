<!-- source: https://www.opswat.com/docs/fenddiode/deployment-examples/lon-ip-examples -->

# LON IP Examples

## [Network/System Requirements](/docs/fenddiode/deployment-examples/lon-ip-examples#networksystem-requirements)

The Fend Diode currently supports listen mode for LON IP networks. Listen mode gathers all supported traffic passing over a network and sends it through the diode to a designated MQTT (AWS) or TCP server endpoint. To install a diode in LON IP listen mode, the LON IP network traffic needs to be port mirrored to the input side of the diode, as follows:

## [Example 1: Diode Settings for LON IP Listen Mode to Local TCP Server](/docs/fenddiode/deployment-examples/lon-ip-examples#example-1-diode-settings-for-lon-ip-listen-mode-to-local-tcp-server)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/lon-ip-examples#diode-input-side-settings)

To configure the diode in LON IP listen mode, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.

Under Input Side -> Protocol Settings -> Select LON IP Listen from the dropdown.

### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/lon-ip-examples#diode-output-side-settings)

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using a static IP:

   1. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the network.

Under Output Side -> Protocol Settings -> Select TCP Client (JSON Protocol Conversion) from the dropdown and set the following:

2. “Target IP Address” will be the IP Address of the computer running the Fend TCP Server Tool.
3. “Target Port” will be the port number set in the Fend TCP Server Tool.
4. For additional information on setting up the Fend TCP Server Tool see [Fend TCP Server Tool Instructions](https://www.opswat.com/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#setting-up-the-fend-tcp-server-tool).

Finally, when done updating all settings press the “Save & Exit” button located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/lon-ip-examples#installing-the-data-diode-after-configuration)

1. See [Fend TCP Server Tool Instructions](https://www.opswat.com/docs/fenddiode/deployment-examples/fend-tcp-json-server-tool-examples#setting-up-the-fend-tcp-server-tool) for details about setting up the Server Tool.
2. Connect the diode’s input side to the mirrored port on the LON network.
3. Connect the diode’s output side to the computer or network containing the computer running the TCP Server Tool.
4. Plug in power to both sides of the diode.
5. Verify data is received on the outbound network.

## [Example 2: Diode Settings for LON Listen Mode to MQTT (AWS)](/docs/fenddiode/deployment-examples/lon-ip-examples#example-2-diode-settings-for-lon-listen-mode-to-mqtt-aws)

### [Diode Input Side Settings](/docs/fenddiode/deployment-examples/lon-ip-examples#diode-input-side-settings)

To configure the diode in LON IP listen mode, start with the input-side diode settings

Under Input Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set the “DHCP Mode” to “Static IP”.
2. Set the Diode IP Address of the diode to ensure that it has a unique address on the network.
3. Set the Subnet Mask and Gateway IP Address appropriately for the diode to communicate on the protected network.
4. Under Input Side -> Protocol Settings -> Select LON IP from the dropdown

### [Diode Output Side Settings](/docs/fenddiode/deployment-examples/lon-ip-examples#diode-output-side-settings)

If you are a Fend Cloud subscriber, you can send LON data to the Fend AWS Cloud using the following settings:

Under Output Side -> Interface Settings -> Select the Ethernet radio button and set the following:

1. Set DHCP mode as needed for the local network. If using static IPs

   1. Set the Diode IP Address for the output side to ensure that it has a unique address on the network.
   2. Set the Subnet Mask and Gateway IP Address as needed for the local network.
2. Set the DNS Server to 1.1.1.1 or a DNS server of your choice
3. Set the NTP Server time.nist.gov or to a DNS server of your choice

Under Output Side -> Protocol Settings -> Select MQTT dropdown and set the following fields:

4. Set the Publish Cycle Time interval to 1 second

Finally, when done updating all settings press the “Save & Exit” button located at the top right of the Diode Web Configuration tool window to close your session and allow the diode to reboot to ensure the new settings are loaded.

### [Diode Output Side Settings (Cellular)](/docs/fenddiode/deployment-examples/lon-ip-examples#diode-output-side-settings-cellular)

Fend data diodes are able to be used in cellular mode only if they have a Fend Cloud subscription. To enable a diode for cellular usage, select “Cellular” under Output Side > Interface Settings. The protocol settings are preconfigured from Fend, and will be ready for use when cellular is selected. For Cellular outbound, see [**Configuring a Diode for Cellular Communication**](https://www.opswat.com/docs/fenddiode/deployment-examples/configuring-a-diode-for-cellular-communication).

### [Installing the Data Diode after Configuration](/docs/fenddiode/deployment-examples/lon-ip-examples#installing-the-data-diode-after-configuration)

1. Connect LON source network to the input side of the diode with an ethernet cable.
2. Connect the destination network (with internet access) to the output side of the diode with an ethernet cable.
3. Plug in power to both sides of the diode.
4. Confirm that data is flowing into AWS using your Fend web app login.
