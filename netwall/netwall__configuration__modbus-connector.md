<!-- source: https://www.opswat.com/docs/netwall/configuration/modbus-connector -->

# MODBUS Connector

The Modbus Connector enables transfer of Modbus data unidirectionally across the MetaDefender Security Gateway USG/BSG (hereinafter Security Gateway). The Modbus Connector is configured on the Security Gateway on both the BLUE and RED sides.

Configuring the Modbus Connector on Security Gateway BLUE creates a Modbus client on the BLUE side and a Modbus server on the RED side.

The Modbus client on Security Gateway BLUE collects data from customer-owned Modbus servers on the BLUE side and transfers data to the Modbus server, configured on Security Gateway RED. Customer-owned Modbus clients on the RED side connect to the Modbus server to collect the transferred data.

## [Security Gateway BLUE](/docs/netwall/configuration/modbus-connector#security-gateway-blue)

Important

A security dongle must be inserted in the BLUE and RED servers to change configuration.

In the Modbus Connector, all Poll records are zero based.

1. Navigate to the **Modbus menu item** under the **Connectors** menu, In the **Action** menu, select **Add Poll Rec**.
2. On the Modbus menu click on the Action button and select Add Poll Rec.
3. Type values in the following boxes:

   1. **IP Address**: IP address of the customer-owned Modbus server the OPSWAT Modbus client will collect data from.
   2. **Port**: Modbus port on the OPSWAT Modbus server.
   3. Enter the following Modbus-specific information to configure Modbus Poll records:

      - **Unit ID**: This field is used for intra-system routing purpose. It is typically used to communicate to a MODBUS+ or a MODBUS serial line slave through a gateway between an Ethernet TCP-IP network and a MODBUS serial line. This field is set by the MODBUS Client in the request and must be returned with the same value in the response by the server. The Unit Identifier is used to communicate via devices such as bridges, routers and gateways that use a single IP address to support multiple independent MODBUS end units.
      - **Unit ID (Red)**: Same as before but for the RED side
      - **Start Addr:** Start address for the Poll record
      - **# of Elements:** Number of elements the poll will check
      - **Poll rate** (in milliseconds)
      - **Command** (select from dropdown)
4. Click on Submit button to save the changes.

Important

When configuring Poll Record, notice that it won't be possible to configure two or more Poll records, checking the same register. Over lapping poll records will be rejected when creating it.

### [Configure Response Timeout Value](/docs/netwall/configuration/modbus-connector#configure-response-timeout-value)

1. Navigate to the **Request Config** tab
2. Type values in the following boxes:

   1. **Request Timeout:** a timeout in seconds for every request per IP and Port. Default value is 5. Valid range 5 - 60.
   2. **Poll Delay:** Poll delay in milliseconds per IP and Port. A value greater than 0 will overwrite the value of "Poll Rate" of every poll record with the same IP and Port. Leave 0 to honor each "Poll Rate" value in Modbus poll records. Default 0 (or 1,000 for non-0 value), valid range 10 - 30,000.

### [Statistics (BLUE)](/docs/netwall/configuration/modbus-connector#statistics-blue)

View Modbus BLUE statistics by clicking on the **Statistics** tab:

## [Security Gateway RED](/docs/netwall/configuration/modbus-connector#security-gateway-red)

Important

To configure Modbus Connector, a security dongle should be inserted in the RED server

1. Login into MetaDefender Security Gateway RED.
2. Go to Modbus menu deploy Action button and select Add Poll Rec.
3. **Allowed IPs**: IP addresses of the customer-owned Modbus clients in the RED zone that will connect to the OPSWAT Modbus server and monitor the Modbus data sent across MetaDefender Security Gateway. You can enter multiple addresses, separated by a semicolon.
4. **Port**: Modbus port on the OPSWAT Modbus client
5. Click on **Submit** to save the changes.

## [Edit/Delete poll records](/docs/netwall/configuration/modbus-connector#editdelete-poll-records)

1. Navigate to the **Modbus menu item** under the **Connectors** menu.
2. In the **Action** menu, select **Add Poll Rec**.
3. Click on **Edit or Delete** menu and edit the fields.
4. Click S**ubmit** to save the changes.
5. Click on Delete or Edit the record. A confirmation pane displays. Click Yes to confirm your action.

##
