<!-- source: https://www.opswat.com/docs/netwall/configuration/mqtt-connector -->

# MQTT Connector

MQTT Connector allows you to transfer MQTT data unilaterally across MetaDefender Security Gateway. MQTT Connector is configured on the MetaDefender Security Gateway BLUE and RED nodes.

The OPSWAT MQTT connector defines subscribers which collects data from a customer-owned MQTT Broker in BLUE network. This data is transferred the MQTT publishers configured on the MQTT connector in MetaDefender Security Gateway RED. These publishers will send the information to a defined MQTT Broker in the RED network.

### [Security Gateway BLUE](/docs/netwall/configuration/mqtt-connector#security-gateway-blue)

Important

To configure MQTT Connector, a security dongle should be inserted in the BLUE server.

1. Login into MetaDefender Security Gateway BLUE.
2. Go to MQTT menu deploy Action button and select Add Subscriber.
3. Type values in the following boxes:

   1. **Channel #:**
   2. **Broker IP or Hostname:** Include here the Broker IP address or the Hostname.
   3. **Broker Port**: Broker's Port number. Default value is 1883 or 8883 if TLS encryption is selected.
   4. **Client ID:** Include here the Client ID. The Client Identifier identifies the Client to the Server. Each Client connecting to the Server has a unique ClientID.
   5. **Keep Alive (sec):** Maximum time interval that is permitted to elapse between the point at which the Client finishes transmitting one MQTT Control Packet and the point it starts sending the next. A Keep Alive **value of 0** has the effect of turning off the Keep Alive mechanism. Default value is 300, valid values are 0-65535.
   6. **Version:** MQTT Protocol Version
   7. **Receive Maximum:** Maximum number of concurrent QOS1 and QOS2 publications that will be processed. Default value is 20, valid values are 1-65535.
   8. **Send Maximum:** Maximum number of outgoing QOS1 and QOS2 messages that the client will attempt to have in flight at once. Default value is 20, valid values are 1-65535.
   9. **Connect Delay (sec):** Elapsed time between connection attempts. Default value is 5.
   10. **Reconnect:** This checkbox controls the behavior of the MQTT client when it is unexpectedly disconnected. The default behavior is to attempt reconnection every second until the connection is successful. Marking the checkbox allows the user to change this parameters.
   11. **Reconnect Delay (sec):** Delay between successive reconnection attempts. Default value is 2, valid values are 1-60.
   12. **Reconnect Delay Max:** Set an upper bound to the delay. Default value is 2, valid values are 1-60. A value greater than Reconnect Delay is recommended.
   13. **Authentication/Encryption:** Select authentication/encryption to apply, once the preferred option is selected extra fields will be displayed to include further information for the authentication/encryption as credentials and certificates. Default option is None, other options are:

       1. None
       2. User/Password.
       3. Server Authentication.
       4. Mutual Authentication.
       5. TLS-PSK.
       6. User/Password + Server Auth.
       7. User/Password + Mutual Auth.
       8. User/Password + TLS-PSK.
   14. **Topic Filter:** An expression contained in a Subscription to indicate an interest in one or more topics. Maximum lenght is 1000 characters.
   15. **Quality of Service:** Define the Quality of Service (QoS) level:

       1. Level 0: At most once delivery. Messages are delivered according to the best efforts of theoperating environment. The message arrives at the receiver either once ornot at all.
       2. Level 1: At least once delivery. It ensures that the message arrives at the receiver at least once.
       3. Level 2: Exactly once delivery. This is the highest Quality of Service level, for use when neither loss nor duplication of messages are acceptable
   16. **Enabled:** This checkbox should be marked to enable MQTT connector.
4. Click on Submit button to save the changes.

### [Security Gateway RED](/docs/netwall/configuration/mqtt-connector#security-gateway-red)

Important

To configure MQTT Connector, a security dongle should be inserted in the RED server

1. Login into MetaDefender Security Gateway RED.
2. Go to MQTT menu deploy Action button and select Add Publisher.
3. **Type values in the following boxes:**

   1. **Channel #:**
   2. **Broker IP or Hostname:** Include here the Broker IP address or the Hostname.
   3. **Broker Port**: Broker's Port number. Default value is 1883 or 8883 if TLS encryption is selected.
   4. **Client ID:** Include here the Client ID. The Client Identifier identifies the Client to the Server. Each Client connecting to the Server has a unique ClientID.
   5. **Keep Alive (sec):** Maximum time interval that is permitted to elapse between the point at which the Client finishes transmitting one MQTT Control Packet and the point it starts sending the next. A Keep Alive **value of 0** has the effect of turning off the Keep Alive mechanism. Default value is 300, valid values are 0-65535.
   6. **Version:** MQTT Protocol Version
   7. **Clean Session:** Specify whether the connection starts a new Session (box checked) or is a continuation of an existing session (box unchecked).
   8. **Topic Name:** if this field is blank, topic names from BLUE side will be used. If a topic name is included here, this will override the topic in BLUE.
   9. **Receive Maximum:** Maximum number of concurrent QOS1 and QOS2 publications that will be processed. Default value is 20, valid values are 1-65535.
   10. **Send Maximum:** Maximum number of outgoing QOS1 and QOS2 messages that the client will attempt to have in flight at once. Default value is 20, valid values are 1-65535.
   11. **Connect Delay (sec):** Elapsed time between connection attempts. Default value is 5
   12. **Reconnect:** This checkbox controls the behavior of the MQTT client when it is unexpectedly disconnected. The default behavior is to attempt reconnection every second until the connection is successful. Marking the checkbox allows the user to change this parameters.
   13. **Reconnect Delay (sec):** Delay between successive reconnection attempts. Default value is 2, valid values are 1-60.
   14. **Reconnect Delay Max:** Set an upper bound to the delay. Default value is 2, valid values are 1-60. A value greater than Reconnect Delay is recommended.
   15. **Authentication/Encryption:** Select authentication/encryption to apply, once the preferred option is selected extra fields will be displayed to include further information for the authentication/encryption as credentials and certificates. Default option is None, other options are:

       1. User/Password.
       2. Server Authentication.
       3. Mutual Authentication.
       4. TLS-PSK.
       5. User/Password + Server Auth.
       6. User/Password + Mutual Auth.
       7. User/Password + TLS-PSK.
   16. **Quality of Service:** Define the Quality of Service (QoS) level:

       1. Level 0: At most once delivery. Messages are delivered according to the best efforts of the operating environment. The message arrives at the receiver either once or not at all.
       2. Level 1: At least once delivery. It ensures that the message arrives at the receiver at least once.
       3. Level 2: Exactly once delivery. This is the highest Quality of Service level, for use when neither loss nor duplication of messages are acceptable
   17. **Enabled:** This checkbox should be marked to enable MQTT connector.
4. Click on Submit button to save the changes.
