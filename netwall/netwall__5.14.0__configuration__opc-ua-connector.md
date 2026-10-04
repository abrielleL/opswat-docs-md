<!-- source: https://www.opswat.com/docs/netwall/5.14.0/configuration/opc-ua-connector -->

# OPC UA Connector

The OPC UA connector enables the MetaDefender Security Gateway (USG/BSG) (hereinafter Security Gateway) to retrieve OPC UA data from a customer-owned OPC UA server in the BLUE zone, transfer the data across the Security Gateway, and replicate the data to customer-owned clients in the RED zone. The OPC UA Connector resides on the Security Gateway BLUE and RED nodes.

On Security Gateway BLUE, the OPC UA Connector acts as a client. It extracts data from a customer-owned OPC UA server in the BLUE zone and transfers that information to the Security Gateway RED. On Security Gateway RED, the OPC UA Connector acts as a server. It receives information from the Security Gateway BLUE and makes the information available to customer-owned OPC UA clients in the RED zone. The OPC UA connector supports connecting to up to 5 OPC UA servers simultaneously, in a 1:1 relationship.

## [Security Gateway BLUE](/docs/netwall/5.14.0/configuration/opc-ua-connector#security-gateway-blue)

Important

A security dongle should be inserted in order to perform any configuration change.

This procedure configures MetaDefender Security Gateway BLUE to communicate with the customer’s OPC UA server in the BLUE zone.

### [Initial Configuration](/docs/netwall/5.14.0/configuration/opc-ua-connector#initial-configuration)

Navigate to the **OPC UA menu item** under the **Connectors** menu, In the **Action** menu, select **Add Configuration**. Fill in the following fields:

1. **Channel #:** Assign a channel number for the configured data flow. Note that the OPC UA channel number must be the same on BLUE and RED.
2. **Name:** Assign a "Friendly Name" for the OPC UA configuration (not mandatory).
3. **UA Server IP**: Type the IP address of the customer’s OPC UA server in the UA Server IP box.
4. **Port**: Type the port number of the customer’s OPC UA server in the Port Number box.
5. **Click on the Discover button**. Optical Diode BLUE connects to the OPC UA server. Available connections will appear in the Connection Options box. Select the connection to be configured and the security mode and policy supported by that server will appear in the boxes below.
6. **Security mode**. The Security Mode and (if applicable), the Security Policy will be auto populated based on the Connection selected.
7. **Statistics Rate:** Type a value in the **Statistics Rate** box to generate OPC UA statistics. This value determines how often statistics are output to the Events log. If you type 0, statistics will not be generated.
8. **Publish Rate:** Type a value in the **Publish Rate** box to determine the rate (in milliseconds) that the OPC UA client on Optical Diode BLUE can receive data from the customer-owned OPC UA server in the BLUE zone. Default value is 1000.
9. **Authentication Mode**: Select Anonymous to allow all users. Select Username to allow a specific user. If you select Username, the Username and Password fields enable. Type the username and associated password you want to allow.
10. **Root Node Filter:** To replicate data from only certain nodes on the OPC UA server in the BLUE zone, type one or more node names in the **Root Node** **Filter** box. Data will be retrieved from each typed node, and all of their child nodes, for replication to the RED zone. If the box is left blank (default), OPC UA data is retrieved from all nodes on the server.
11. **Description:** Key in a detailed description of the configuration (not mandatory).
12. **Max Browse Blocks per Second:** Type the rate at which the OPC UA schema is sent from Blue To Red. Recommended value is 15 blocks per second. If stack overflow syslog messages start appearing on either Red or Blue, reduce the block count to 10 blocks per second.
13. **Max Tags per Subscription:** Max Tags involves the capability of the individual OPC UA Server that we are connecting to from BLUE. OPC UA Servers have a limit on the number of tags per subscription, as well as the number of subscriptions. The default value is 4000. If syslog reports an error of **max subscriptions reached**, increase the Max Tags to 6000 and try again. If syslog reports an error of **subscription too large,** reduce the Max Tags value.
14. **Auto Rebrowse:** Enable/disable periodic rebrowse.
15. **Rebrowse Delay:** Time between each automatic rebrowse. Valid range: 0 - 604800. Default: 60
16. **Rebrowse Scope:** Defines which node (and sub-tree) to rebrowse, can be left empty to rebrowse all. Max length: 200 characters.
17. **File Resend:** Check to enable/ disable file resend at set time interval (Used for only OPC UA Part 20 File Transfer).

Note

- All filter values are case-insensitive.
- You can type multiple node names in the Root Node Filter box.
- You can type only one node name in the Trace Node box.
- Separate multiple node names with a semi-colon.
- Changing filter information restarts MetaDefender Security Gateway BLUE. This process takes about one minute.

Note

For example, if a tag on the OPC UA server changes 10 times/second (100 ms), and the Publish Rate is 1000 ms, the client receives one value/second. If the Publish Rate is 50 ms, the client could receive 20 values/second. However, since the tag only changes 10 times/second, the client receives 10 values/second.

Click the Submit button to send the changes. After you click Submit, if all connections are correct, the boxes in the OPC UA Status area should populate after about one minute and the certificate will be available to download.

### [Trusted Certificates](/docs/netwall/5.14.0/configuration/opc-ua-connector#trusted-certificates)

You must install trusted certificates on both the OPC UA client on MetaDefender Security Gateway BLUE and on the OPC UA server in the BLUE zone. Refer to Pages 27 and 28 of the OPC Unified Architecture document, authored by the OPC Foundation, for information on management and transfer of certificate information between the OPC UA server and OPC UA client.

The BLUE Client Certificate is generated by OPSWAT and located on MetaDefender Security Gateway BLUE. You must place this certificate on the OPC UA server. Click the Export button to locate the certificate on MetaDefender Security Gateway BLUE and save it to your desktop. Then, transfer the certificate to the OPC UA server.

You must generate the UA Server Certificate and place it on MetaDefender Security Gateway BLUE. After generating the certificate and saving it to your desktop, click the Import button to locate the certificate and place it on MetaDefender Security Gateway BLUE.

Click to enable the Allow Untrusted Server Certificates checkbox if you want to allow untrusted certificates on the OPC UA server. The default is disabled.

### [Configure Multiple OPC UA Servers BLUE](/docs/netwall/5.14.0/configuration/opc-ua-connector#configure-multiple-opc-ua-servers-blue)

On BLUE, navigate to the **OPC UA menu item** under the **Connectors** menu, Select **Add Configuration** from the **Action** menu.

Repeat the steps outlined in the Initial BLUE Configuration section above to add additional OPC UA servers.

Note

A maximum of 5 OPC UA servers can be configured on rack mount server form factors.

### [Refresh Tags](/docs/netwall/5.14.0/configuration/opc-ua-connector#refresh-tags)

When names of the tags are changed on the BLUE side customer-owned OPC UA server, the tags need to be refreshed so that the OPC UA BLUE client can collect data for the changed tags. Click on the **Refresh Tags** button to clear the cache allowing the correct transfer of tag information.

## [Security Gateway RED](/docs/netwall/5.14.0/configuration/opc-ua-connector#security-gateway-red)

Important

A security dongle should be inserted in order to perform any configuration change.

This section describes configuration of the Optical Diode OPC UA RED server to transfer OPC UA data to the customer-owned OPC UA client(s) in the RED zone.

### [Initial configuration](/docs/netwall/5.14.0/configuration/opc-ua-connector#initial-configuration)

Navigate to the OPC UA section under the Connectors menu. On the right hand side "**Action**" menu select "**Add Configuration**".

Fill in the following fields:

1. **Channel Number:** Assign a Channel Number for the configured data flow. Note that the OPC UA channel number must be the same on BLUE and RED.
2. **Name:** Assign a friendly name (not mandatory)
3. **IP Address:** IP Address dropdown. Lets a user choose which IP address the OPC-UA server will listen on RED side. Or **ANY** to allow connections on any interface/IP.
4. **Server Port**: Type the Optical Diode RED port number in the Port box. The customer-owned OPC UA clients will connect to this node.
5. **Statistics Rate:** Type a value in the **Statistics Rate** box if you want to generate OPC UA statistics. If you type 0, statistics will not be generated.
6. **Trace Node:** if you want to trace data generated from an individual node, type the name of a node on the OPC UA server in the BLUE zone in the **Trace Node** box. This field is not mandatory and can be empty.
7. **Preserve Node ID Structure:** Click the **Preserve Node ID Structure** checkbox if you want to preserve the Node ID structure for each tag on the customer-owned OPC UA server in the BLUE zone. If you do not click this checkbox, the OPC UA server on the Optical Diode RED will create its own Node ID references for each tag.

### [Trusted certificate](/docs/netwall/5.14.0/configuration/opc-ua-connector#trusted-certificate)

You must install a trusted certificate on the MetaDefender Security Gateway RED OPC UA server. Generate the certificate on your OPC UA client and transfer it to your desktop.

Click the Import button to locate the certificate on your desktop and transfer it to MetaDefender Security Gateway RED.

### [Configure Multiple OPC UA Servers RED](/docs/netwall/5.14.0/configuration/opc-ua-connector#configure-multiple-opc-ua-servers-red)

1. On Optical Diode RED, navigate to the **OPC UA menu item** under the **Connectors** menu.
2. Select **Add Configuration** from the **Action** menu.
3. Repeat the steps outlined in the Initial RED Configuration section above to add additional OPC UA servers.

Note

A maximum of 5 OPC UA servers can be configured on rack mount server form factors.
