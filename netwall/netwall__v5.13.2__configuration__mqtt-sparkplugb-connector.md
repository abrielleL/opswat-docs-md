<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/configuration/mqtt-sparkplugb-connector -->

# MQTT SparkPlugB Connector

Sparkplug B is an open-source specification that provides for a standardized framework for industrial applications using MQTT. It provides for defined topic namespaces, state management (birth/death certificates), and payload definitions to ensure interoperability, scalability, and context for data between edge devices and SCADA systems.

MQTT SparkPlugB Connector allows you to transfer SparkPlugB data unidirectionally across the MetaDefender Security Gateway (hereinafter Security Gateway). The SparkPlugB Connector is configured on the Security Gateway BLUE and RED sides.

The SparkPlugB Connector acts as an MQTT client on both BLUE and RED sides, performing both publishing and subscribing roles simultaneously on the BLUE and RED sides. The data is transferred to the MQTT client configured on the SparkPlugB Connector on the Optical Diode RED. That MQTT client forwards the MQTT data to a defined MQTT broker on the RED network.

### [Security Gateway BLUE](/docs/netwall/v5.13.2/configuration/mqtt-sparkplugb-connector#security-gateway-blue)

Info

A security dongle must be inserted in the BLUE and RED servers to change configuration.

1. Navigate to **Connectors -> SparkPlug B**.
2. Select **Edit** button.
3. Type values in the following boxes:

   1. **Broker IP or Hostname:** Include here the Broker IP address or the Hostname.
   2. **Broker Port**: Broker's Port number. Default value is 1883 or 8883 if TLS encryption is selected.
   3. **Client ID:** Include here the Client ID. The Client Identifier identifies the Client to the Server. Each Client connecting to the Server has a unique ClientID.
   4. **Primary Host Application ID:** Unique ID that identified the central application consuming data from SparkPlugB edge nodes devices. Max length 1,000. /# and + are not allowed.
   5. **Keep Alive (sec):** Maximum time interval that is permitted to elapse between the point at which the Client finishes transmitting one MQTT Control Packet and the point it starts sending the next. A Keep Alive **value of 0** has the effect of turning off the Keep Alive mechanism. Default value is 300, valid values are 0-65535.
   6. **Version:** MQTT Protocol Version
   7. **Receive Maximum:** Maximum number of concurrent QOS1 and QOS2 publications that will be processed. Default value is 20, valid values are 1-65535.
   8. **Send Maximum:** Maximum number of outgoing QOS1 and QOS2 messages that the client will attempt to have in flight at once. Default value is 20, valid values are 1-65535.
   9. **Connect Delay (sec):** Elapsed time between connection attempts. Default value is 5
   10. **Reorder Timeout:** Configurable grace window to recover out of order messages before NCMD Rebirth (seconds). Default:5, Range 0-3,600.
   11. **Reconnect:** This checkbox controls the behavior of the MQTT client when it is unexpectedly disconnected. The default behavior is to attempt reconnection every second until the connection is successful. Marking the checkbox allows the user to change this parameters.
   12. **Reconnect Delay (sec):** Delay between successive reconnection attempts. Default value is 2, valid values are 1-60.
   13. **Reconnect Delay Max:** Set an upper bound to the delay. Default value is 2, valid values are 1-60. A value greater than Reconnect Delay is recommended.
   14. **Authentication/Encryption:** Select authentication/encryption to apply, once the preferred option is selected extra fields will be displayed to include further information for the authentication/encryption as credentials and certificates. Default option is None, other options are:

       1. None
       2. User/Password.
       3. Server Authentication.
       4. Mutual Authentication.
       5. TLS-PSK.
       6. User/Password + Server Auth.
       7. User/Password + Mutual Auth.
       8. User/Password + TLS-PSK.
   15. **Group ID:** Physical/logical grouping of Edge Nodes. The Group ID combined with Edge Node ID must be unique. Max length: 1,000. / # and + are not allowed.
   16. **Edge Node ID:** An Edge Node in SparkPlugB is an MQTT client responsible for interfacing with one or more physical devices and for communicating their data to the MQTT broker using the SparkPlugB topic namespace and payload structure. Max length 1,000. / # and + are not allowed.
   17. **Enabled:** This checkbox should be marked to enable MQTT connector.
4. Click on **Submit** button to save the changes.

### [Security Gateway RED](/docs/netwall/v5.13.2/configuration/mqtt-sparkplugb-connector#security-gateway-red)

Info

A security dongle must be inserted in the BLUE and RED servers to change configuration.

1. Navigate to **Connectors -> SparkPlug B**.
2. Select **Edit** button.
3. **Type values in the following boxes:**
4. 1. **Broker IP or Hostname:** Include here the Broker IP address or the Hostname.
   2. **Broker Port**: Broker's Port number. Default value is 1883 or 8883 if TLS encryption is selected.
   3. **Keep Alive (sec):** Maximum time interval that is permitted to elapse between the point at which the Client finishes transmitting one MQTT Control Packet and the point it starts sending the next. A Keep Alive **value of 0** has the effect of turning off the Keep Alive mechanism. Default value is 300, valid values are 0-65535.
   4. **Version:** MQTT Protocol Version
   5. **Receive Maximum:** Maximum number of concurrent QOS1 and QOS2 publications that will be processed. Default value is 20, valid values are 1-65535.
   6. **Send Maximum:** Maximum number of outgoing QOS1 and QOS2 messages that the client will attempt to have in flight at once. Default value is 20, valid values are 1-65535.
   7. **Connect Delay (sec):** Elapsed time between connection attempts. Default value is 5
   8. **Reconnect:** This checkbox controls the behavior of the MQTT client when it is unexpectedly disconnected. The default behavior is to attempt reconnection every second until the connection is successful. Marking the checkbox allows the user to change this parameters.
   9. **Reconnect Delay (sec):** Delay between successive reconnection attempts. Default value is 2, valid values are 1-60.
   10. **Reconnect Delay Max:** Set an upper bound to the delay. Default value is 2, valid values are 1-60. A value greater than Reconnect Delay is recommended.
   11. **Authentication/Encryption:** Select authentication/encryption to apply, once the preferred option is selected extra fields will be displayed to include further information for the authentication/encryption as credentials and certificates. Default option is None, other options are:

       1. User/Password.
       2. Server Authentication.
       3. Mutual Authentication.
       4. TLS-PSK.
       5. User/Password + Server Auth.
       6. User/Password + Mutual Auth.
       7. User/Password + TLS-PSK.
   12. **Enabled:** This checkbox should be marked to enable MQTT connector.
5. Click on Submit button to save the changes.
