<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector -->

# NetWall OPC DA Connector

## [Introduction](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#introduction)

The NetWall OPC Connector allows you to configure an OPC client and OPC server to transfer OPC DA and A&E data across NetWall product family (Optical Diode, Unidirectional and Bilateral Security Gateways).

An OPC client collects data from one or more customer-owned OPC DA or A&E servers in the NetWall BLUE zone (source servers) and provides a unidirectional transfer of that data to the OPC server in the NetWall RED zone. Customer-owned OPC clients in the RED zone (destination servers) connect to the OPC server to create a read-only instance of one or more replicated OPC servers in a non-secure environment.

### [Supported Features](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#supported-features)

The OPC Connector provides the following features:

- Supports collection from multiple OPC servers
- Supports data scan rates as low as 2 msec
- Replicates all standard and custom OPC properties
- Supports OPC browsing
- Supports Deadband and individual point scan rates
- Detects communications loss and reflects it across the NetWall
- High Availability failover for redundant OPC DA servers and flanking servers.

### <Deployment>

The OPC Connector is installed on a separate flanking servers from the NetWall BLUE and RED nodes in one of the following deployments:

- Installation on the same machine as a customer-owned OPC server. Additional communication software is not needed.
- Installation on a separate machine from a customer OPC server. DCOM is used to allow the servers and clients to communicate.

The machines where the OPC connector software is installed are referred to as the BLUE and RED flanking servers, respectively.

For either deployment, installing the OPC Connector software creates a OPC client on the BLUE flanking server and a OPC server on the RED flanking server.

The NetWall BLUE and RED zones can have different deployments. For example, the OPC client could be on the same machine as a customer-owned server in the BLUE zone, and the OPC server could be on a different machine than the customer-owned server in the RED zone.

Each OPC Connector installation creates an OPC instance. Multiple instances can be configured on the same machine, differing by the NetWall Port number that is entered during configuration.

The following figure shows a deployment where the OPC Connector is installed on different servers in the BLUE and RED zones.

The following configuration applies:

1. The OPC client uses DCOM to communicate with customer-owned OPC servers (sources) in the NetWall BLUE zone.
2. The OPC client collects OPC data to creates a unidirectional TCP stream and sends the stream across NetWall.
3. The OPC server in the NetWall RED zone receives the TCP stream and replicates the OPC data.
4. The customer-owned OPC clients (destinations) in the RED zone use DCOM to communicate with the OPC server and read the data.

### [Time Stamps](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#time-stamps)

The OPC Connector deviates from the OPC Foundation DA Server specifications for time stamp. According to the specification, the time stamp for an OPC value should be in relation to the OPC server that provides the Time Stamp. The OPC Connector maintains the time stamp from the OPC client. This timestamp is propagated unchanged through NetWall, to the OPC server.

## [Install OPC Connector](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#install-opc-connector)

### <Prerequisites>

- You must have admin rights on any machine where you want to install the OPC Connector.
- Install Microsoft NET Framework 4.5 on the BLUE and RED flanking servers.
- If the OPC servers and clients are on separate machines, configure DCOM on the servers and on the customer-owned OPC clients.

## [Install on BLUE Flanking Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#install-on-blue-flanking-server)

You will receive a folder containing the .*msi* files shown below. Install these files on any machine in the BLUE zone where you want to create a OPC client.

- Graphical Interface: *OPSWAT_OPCDA_BLUE_Config_UI_Install.msi*
- OPC service: *OPSWAT_OPCDA_BLUE_Service.msi*

### [Update Installation](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#update-installation)

If you are updating an existing installation, halt the OPC service and uninstall the following applications, using the Windows Control Panel:

- *OPSWAT OPCDA BLUE Config UI*
- *OPSWAT OPCDA BLUE Service*

### [Install User Interface](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#install-user-interface)

Double-click *OPSWAT_OPCDA_BLUE_Config_UI_Install.msi* to open the wizard. Accept the defaults until the installation is complete.

### [Install OPC Service](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#install-opc-service)

Double click *OPSWAT_OPCDA_BLUE_Service.msi* to open the wizard.

Accept the defaults until you reach the *Set Service Login* screen. Then, select a Username that will have access to your OPC servers.

Important

Make sure to preclude the Username with a “.\”.

Set the appropriate password. Click on **OK** and continue the installation, accepting the defaults until the installation is complete.

## [Install on RED Flanking Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#install-on-red-flanking-server)

Info

Before installing OPSWAT_OPCDA_ RED_Service.msi you need:

1. .NET 2.0 / .NET 3.0 feature on Windows must be enabled. Click here for some help [Install .NET Framework 3.5 on Windows - .NET Framework | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/framework/install/dotnet-35-windows)
2. OPC Core Components redistributable v3.X must be installed. Click here for more information [Classic - OPC Foundation](https://opcfoundation.org/developer-tools/samples-and-tools-classic/core-components/)

You will receive a folder containing the .*msi* files shown below. Install these files on any machine in the RED zone where you want to create a OPC server.

- OPC Server Wrapper: *OPSWAT_OPCDA_RED_Service.msi.*

### [Update Installation](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#update-installation)

If you are updating an existing installation, uninstall *OPSWAT OPCDA RED Service*, using the Windows Control panel.

### [Install Server Wrapper](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#install-server-wrapper)

The Server Wrapper creates the OPC Configurator, which is used to configure the OPC server on the RED flanking server.

Double-click *OPSWAT_OPCDA_RED_Service.msi* to open the wizard. Accept the defaults until the installation is complete.

Important

For best operability with existing software, *OPSWAT_OPCDA_RED_Service.msi* has been intentionally made 32-bit. Most existing DA clients are 32-bit software. However, it is likely that some users run *OPSWAT_OPCDA_RED_Service.msi* on a 64-bit machine. Please check [DCOM Configuration in RED side](https://app.developerhub.io/netwall/v5.2.0/opc-connector/netwall-opc-connector#dcom-configuration-in-red-side)

### [Install OPC Client](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#install-opc-client)

Install your customer-owned OPC client on all computers that will communicate with the OPC server.

This chapter describes how to configure the OPC client on the BLUE flanking server to collect data from an OPC source and transmit that data across NetWall.

Important

You must download any configuration changes made on the OPC client to the OPC service before they take effect. Refer to “Download configuration” for more information.

The general configuration process is:

1. Add a server: Defines an OPC source for data collection.
2. Add a group: Defines a container where database points from the source will be stored.
3. Add points to the group: Adds database points to the defined group.

Click the OPC icon on the OPC client. The OPC *Main Form* pane displays.

## [Configure OPC Client](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#configure-opc-client)

This section describes how to configure the OPSWAT NetWall OPC client on the BLUE flanking server to collect data from an OPC source and transmit that data across NetWall.

Important

You must download any configuration changes made on the OPC client to the OPC service before they take effect. Refer to “Download configuration” for more information.

The general configuration process is:

1. **Add a Server:** Defines an OPC source for data collection.
2. **Add a Group:** Defines a container where database points from the source will be stored.
3. **Add Points to the Group:** Adds database points to the defined group.

Click the OPC icon on the OPSWAT OPC client. The OPC *Main Form* pane displays.

Backup or Restore Configuration

We recommend you back up your current configuration before making any modifications.

Select **Backup/Restore** from the **File** menu.

### [Add Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#add-server)

This procedure describes how to add an OPC source server to the data collection.

1. Select **Add Server** from the **Servers** menu. The *Select OPC Server* pane displays. $plugin[46abjlxpbbf]
2. Select the type of server you want to install from the dropdown list.
3. Click **Browse for Servers** to locate available customer-owned servers of the selected type. **Local Servers** (OPC servers on the same machine as the OPC client) and **Local Network** servers (OPC servers on different machines in the same network) display. $plugin[upqb01mc3sx]
4. Expand a node on the local network to show OPC servers that are accessible on different machines on that network. If a node turns red when you try to expand it, OPC servers are not available. If the node turns green, OPC servers are available, and a list of the servers displays. $plugin[1opjhb8fnde]
5. Click the server you want to add. $plugin[9lznogwpll7]
6. Type the following values:

   - **NetWall IP address:** NetWall BLUE IP address
   - **NetWall Port Number**: TCP port number that was allocated for OPC during streaming configuration. Refer to the *NetW__all User Guide* for more information.
7. Click the **OK** button.
8. Select another server and repeat step 6 for each source you want to add to the data collection. The servers will display on the *OPC Main Form*.

## [Configure Remote Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#configure-remote-server)

You can add remote OPC servers to your local network. Right-click **Local Network** to display the configuration menu.

### [Add Remote Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#add-remote-server)

Select **Add Server** to add a server to your local network. A popup displays.

Type the server information and click **OK**. The server displays in the Local Network list.

### [Edit Remote Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#edit-remote-server)

Select **Credentials** to edit the server. The popup shown in **Add remote server** displays. Edit the settings as necessary and click **OK**.

### [ReScan](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#rescan)

Select **ReScan** to re-examine the network for OPC servers. Any new servers that are located during the scan are displayed in the list.

### [Delete Remote Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#delete-remote-server)

Select **Delete Server** to remove the server from your local network.

### [Modify or Delete Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#modify-or-delete-server)

To change the server IP address or port number or delete the server, right-click the server on the *OPC Main Form* and select **Modify Server** or **Delete Server**, respectively.

### [Add Group](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#add-group)

This procedure describes how to add a group to an OPC source server. A group defines the data collection parameters for the database points that will be added.

1. Right-click the OPC server on the *OPC Main Form* and select **Add Group**. The *AddGroup* pane displays. $plugin[vnkg2n6l0vj]
2. Enter the following information:

   1. **Name**: Name for the group
   2. **Active**: Click to allow data to be collected for the group.
   3. **Update Rate**: Click to use Asynchronous Notification (OPC Server Data Callback). The box is selected by default. If selected, the OPC server pushes data to the OPC Service for this group whenever data changes, based on the Update Rate.

      1. Select the maximum update rate your group will support for Data Callback. The default is 1000ms. If this rate is not set correctly, data loss can occur. For example, if the OPC server processes values at 250ms and you set the **Update Rate** to 1000ms, you will only receive every 4th change from the OPC server.
   4. **Polling Rate**: Click to use Synchronous Polling. This value sets the rate at which group values are polled from the OPC source. Synchronous Polling can be used in addition to Data Callback.
   5. **Keep Alive Rate**: Keep-alive time for a subscription to cause the server to provide client callbacks on the subscription when there are no new events to report.
   6. **Deadband OPC**: Percent change in an item value that will cause a subscription callback for that value to a client. This option only applies to items in the group that have a numeric value (as opposed to a state) and is only valid if **Update Rate** is selected.
   7. **Watchdog Timer**: Click the checkbox, then set the desired time in minutes. If enabled, the OPC Connector monitors activity for this group. If there is no activity for the amount of time specified, the application closes and then re-opens its connection to the specified OPC source.
   8. **Locale:** Time zone for the Watchdog Timer. Click the checkbox, then select the desired time zone.
3. Click the **OK** button to add the group.

### [Add Points to Group](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#add-points-to-group)

This procedure describes how to add database points to your group.

The *BuildGroup* pane displays after you add a new group, or you can right-click a group on the *Main OPC Form* and select **Modify Group**.

Complete the following information:

1. Click to **Enable Forced Reset**, if desired. If clicked, set the time, in hours, after which you want the OPC Connector to disconnect and reconnect. When the time elapses, the OPC Connector disconnects from and immediately reconnects to the OPC source.
2. Click the **Connect** button to connect to the OPC source you just added. If the server supports the Browse function, the list of database points on that server displays. $plugin[f5effe31bhg]
3. Expand the folder on the left and click to select individual points, or select an entire folder by right-clicking the folder and selecting **Select Children**. If you **Select Children**, the OPC Connector extracts OPC attributes for each point in the selection. When completed, the selected points display in the **Item ID** pane on the right. $plugin[4jbpjokv543]
4. Click **Save** to return to the *OPC Main Form*.

### [Modify Group](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#modify-group)

Click the **Modify** button to make changes to a group. The *AddGroup* pane displays, and you can edit the values. Refer to “Add group” for definitions of the values. You can also change the name of the group in the *AddGroup* pane to add a new group or make changes to a group other than the one selected when you opened the *BuildGroup* pane.

You can modify any group by right-clicking the group on the *OPC Main Form* and selecting **Modify Group**.

### [Refresh Group](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#refresh-group)

Click the **Refresh** button on the *BuildGroup* pane to get the newest data for the group.

### [Import File](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#import-file)

Instead of connecting to the OPC server and selecting each point, you can use buttons on the *BuildGroup* pane to import a saved group as a *.xml* or .*csv* file. The contents of the file will be displayed as a group and its associated points.

#### [Import .xml file](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#import-xml-file)

1. Click the **Import File** button. The *C:\ProgramData\OPSWAT\XmlExport* directory displays.
2. Browse to locate the *.xml* file.
3. Select the file and click **Open**. The contents of the file will merge with the current window content as a group and its points.

#### [Import .csv file](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#import-csv-file)

A .*csv* file is generally created by hand, separately from the OPC connector. This file can contain detailed information and attributes on the points in a group.

1. Click the **Connect** button. After the server connects, the **Import CSV** button becomes active.
2. Click the **Import CSV** button. The *CSV Import* pane displays.
3. Click the **Search** button to locate the .*csv* file.
4. Click the **OK** button to import the file. The import status displays in the **Status** bar. Any errors in import display in the **Errors** section.

When the import is complete, the contents of the .*csv* file merge as a group, points, and attributes with the contents of the *BuildGroup* pane.

### [Export File](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#export-file)

You can export a group from an OPC server as an *.xml* file and then import that file to a different OPC server.

1. Click the **Connect** button. After the server connects, the **Export File** button becomes active.
2. Click the **Export File** button. The *C:\ProgramData\OPSWAT\XmlExport* directory displays.
3. Enter a name for the .*xml* file and click **OK** to create the file.

### [Edit Points](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#edit-points)

There are two ways to edit points in a group:

- Right-click a point in the *BuildGroup* pane and select a value from the menu. $plugin[20ma1uisitt]
- Double-click a point on the *OPC Main Form* and click a button in the resulting menu. $plugin[iprbamhm3f6]

You can perform the same tasks from either menu.

#### [View Properties](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#view-properties)

Select **View Properties** or **View** to display properties for the selected point. Properties are specific to the OPC source.

#### [Delete Point](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#delete-point)

Select **Delete** to delete the selected point from the group.

#### [Trace](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#trace)

Tracing monitors all transactions for a selected point. Whenever the value of the point changes, the following is logged:

- Time of the change
- New value of the point
- Point status

Select **Trace** to display the *TraceEnable* pane.

1. Click **Select** for the Trace Point 1-6 that you want to use.
2. Click **Trace Enabled** to enable trace for that point.
3. Click **Accept** to accept your changes.

After approximately 15 seconds, point values for the point being traced display in the Trace Log, located in *C:\ProgramData\NraOPC\TraceFiles*. An entry is logged into the Trace Files when the selected point is updated from either a Poll command or a Data Event Callback.

Note

The *TraceFiles* folder is not created until actual values exist for the point being traced.

Each line of Trace data displays as follows:

`12/01 07:13:03.266 SVR320-DEVOPC.NraTestOpcServer.NET.DaServer.Wrapped,Dynamic/Analog Types/dbt0003,22.3849607955237,Good,DataChange`

The data sampling time is registered to the Millisecond level. The last field (DataChange) gives the origin of the data. DataChange is data from a Data Event Callback or Asynchronous Data. Poll would represent data from a Synchronous Poll issued by the OPC Connector.

Note

To view all traces configured for a group, right-click the group on the *OPC Main Form* and select Point Trace.

***OPC Main Form*** **and select Point Trace.**

#### [Edit](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#edit)

Select **Edit** to change the default attributes of the point. The *Edit Items* pane displays.

You can type new values for **Item Name** or **Item Path**. For all other boxes, you must click the checkbox before you can edit the values.

- **Requested Type**: Possible OPC values for that point
- **Active**: Click to enable or disable data collection for the point
- **Deadband**: Percent change in an item value that will cause a subscription callback for that value to a client. This parameter only applies to items in the group that have a numeric value and is only valid if Data Callback is selected.
- **Sampling Rate**: Polling rate for that point

Click the **OK** button to save your changes.

## [Complex Item](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#complex-item)

To view a complex item (if available on your OPC server):

1. Right-click the group that contains the item on the *OPC Main Form*.
2. Select **Modify Group**. The *BuildGroup* pane displays.
3. Click the **Connect** button.
4. Right-click the item on the left side of the *BuildGroup* pane and select **View Complex Item**.

## [Delete a Group](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#delete-a-group)

To delete a group, right-click the group on the *OPC Main Form* and select **Delete Group**. Click **Yes** to confirm your action.

## [OPC DA BLUE Flanker Redundancy](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#opc-da-blue-flanker-redundancy)

The NetWall OPC DA Connector supports redundant OPC DA flankers on Blue. One flanker is deemed Primary. The primary flanker will always be the flanker in control if both flankers are operational. If the Primary flanker fails, the Secondary flanker assumes control. When the Primary flanker becomes available, the Secondary flanker relinquishes control, and the Primary flanker assumes control.

The Secondary flanker receives the OPC DA Server configuration from the Primary Flanker. The OPC DA Server configuration cannot be modified by the Secondary Flanker. Server Configuration can only be done by the Primary Flanker.

The Redundant OPC DA flankers communicate with each other via TCP/IP.

### [Configure Primary OPC DA Flanker for Redundancy](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#configure-primary-opc-da-flanker-for-redundancy)

1. Login into OPC DA BLUE Config UI and select **Redundancy** from the top menu.
2. Type values in the following boxes:

   1. **Enable Flanker Redundancy:** Tick checkbox to enable/disable Flanker Redundancy.
   2. **Primary Flanker:** Tick checkbox to designate as the primary Flanker
   3. **Port Number:** Port number to use for TCP communication between Primary and Secondary flankers.
   4. **Secondary IP:** - IP Address of the Secondary Flanker. Either the IP Address or the Host name of the Secondary Flanker can be used.
   5. Click on **OK** button to save the changes.

Primary Blue Flanker Redundancy

### [Configure Secondary OPC DA Flanker for Redundancy](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#configure-secondary-opc-da-flanker-for-redundancy)

1. Login into OPC DA BLUE Config UI and select **Redundancy** from the top menu.
2. Type values in the following boxes:

   1. **Enable Flanker Redundancy:** Tick checkbox to enable/disable Redundancy
   2. **Primary Flanker:** Checkbox to designate the Primary Blue Flanker (unchecked for Secondary)
   3. **Port Number:** Port number to use for TCP communication between Primary and Secondary flankers.
   4. **Secondary IP:** IP Address of the Secondary Flanker. No value needed for the Secondary Flanker configuration. It is defined by the primary.
   5. Click on **OK** button to save the changes.

Secondary Flanker Redundancy

### [View Flanker Configuration Status](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#view-flanker-configuration-status)

1. Once configured, the Home screen will display the configuration of the Flanker (Primary Flanker or Redundant Flanker).

Flanker Status Main Screen

### [Primary Flanker Redundancy Status](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#primary-flanker-redundancy-status)

1. Select **Status** on the Home screen on the Primary Flanker to view the current status of redundancy.
2. In the example below, the Secondary Flanker is operational. The HA Heartbeat is a message that is sent from the Primary to the Secondary Flanker, telling the Secondary Flanker that the Primary is operational.

Flanker Redundancy Status (Secondary OK)

1. If the Primary Flanker is unable to communicate with the Secondary Flanker ,the display will look as follows:

Flanker Redundancy Status (Secondary Fail)

### [Secondary Flanker Redundancy Status](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#secondary-flanker-redundancy-status)

1. Select **Status** on the Home screen on the Secondary Flanker to view the current status of redundancy.
2. In the example below, the Primary Flanker is operational. The HA Heartbeat is a message that is sent from the Primary to the Secondary Flanker, telling the Secondary Flanker that the Primary is operational.

Secondary Flanker Redundancy Status (Primary OK)

1. If the Primary Flanker is unable to communicate with the Secondary Flanker, the display will look as follows:

Secondary Flanker Redundance Status (Primary Fail)

### [Windows Event Logs](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#windows-event-logs)

1. When the Secondary Flanker takes control of the OPC servers, the Windows Event Log will show that the Secondary Flanker has taken control.

Secondary Flanker Taking Control of OPC Servers

1. When the Primary Flanker becomes available, the Windows Event Log will show that the Secondary Flanker is relinquishing control of the OPC DA servers.

Secondary Flanker Relinquishing Control of OPC DA Servers

## [OPC DA Server Redundancy](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#opc-da-server-redundancy)

The NetWall OPC DA connector can specify redundant OPC DA Servers. The following conditions must be met for redundant OPC DA Servers:

1. The schema for both OPC DA Servers must be identical
2. The Flanker must have DCOM access to both OPC DA Servers
3. If redundant flankers are implemented, both flankers must have DCOM access to the OPC DA Servers.

There is no Primary server in a redundant OPC DA Server pair. The Blue Flanker will attempt to connect to one of the pair members, and it will stay with that member as long as it is successful in collecting data from that member.

There is no specific configuration on Red for Redundant OPC DA Servers. If two ports are specified for a given Blue OPC DA Server (see next section), then two Red Flankers can be configured. Each Red Flanker will receive the same Blue Schema/Data, and each Red Flanker will have live data available.

### [Configuring an OPC DA Server for Redundancy](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#configuring-an-opc-da-server-for-redundancy)

1. Login into OPC DA BLUE Config UI and select **Severs** from the top menu.
2. Select an OPC DA Server
3. Type values in the following boxes:

   1. **Server:** OPC DA server selected for redundant configuration.
   2. **NetWall IP:** Address of the NetWall BLUE machine.
   3. **Port Numbers:** Port Numbers that the Blue Flanker will use for its NetWall connection. Up to two port numbers can be specified. If two port numbers are specified, the OPC DA data/schema transmissions will be replicated on the second port.
   4. **DA Server IP Address:** With redundant DA servers, we specify the IP address of each server. The IP Address that appears first will always be the first server that the Flanker will attempt to connect to.
   5. **HA Heartbeat Tag:** Name of a tag in the OPC server. The tag can be any valid type (INT, FLOAT, etc.). When present, the Blue Flanker will monitor this tag for changes in value. If the value of the tag does not change within the timeframe specified in the *HA Heartbeat Timeout* field, the Blue Flanker code will switch to the opposing OPC Server.
   6. **Disable Point Fail:** Under normal circumstances, the Blue Flanker will set the status of all OPC points to FAIL if it is unable to process values from an OPC Server. Selecting this box will prevent the Blue Flanker from failing all OPC Points.
   7. **Enable Debug:** When selected, this causes a large amount of debugging information to be placed into the Windows Event Log for the OPC Server. This normally is left unchecked.
   8. **Enable Shallow Browsing:** When selected, the Blue Flanker will only collect minimal required attributes (tag name, value type, value status) from the OPC server. It will not browse for attributes on the OPC Server.
   9. Click on **OK** button to save the changes.

OPC DA Server Modify Screen

### [Testing OPC Servers](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#testing-opc-servers)

OPC Da Server testing can be performed on both the Primary and Secondary Flanker. If redundant OPC Servers are present, both OPC Servers will be tested. The testing procedure can be performed from the Secondary Blue Flanker as well, if redundancy is enabled.

Select Testing for OPC Servers

## [Configure A&E Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#configure-ae-server)

If you add an A&E OPC server, you can configure an Events subscription from the *OPC Main Form*. Creating a subscription lets you monitor events specific to the A&E server.

OPC A&E Events Setup

1. Right-click the server and select **AE Events Setup**. A browse pane displays. $plugin[5ekjlsbz9z0]
2. Click the **Connect** button to connect to the selected server or use the **Browse** button to locate and then connect to a different server.
3. Click **<new subscription>** to create a new subscription. A popup displays. $plugin[enfjssbaxmq]
4. Enter a name and click **OK**. A *Create Subscription* pane displays. $plugin[ngo7erj8jde]
5. Select the **Categories** of events you want the subscription to track. All **Attributes** display on the right side of the pane and depend on the configuration of your A&E server.
6. Select the type of filters you want the subscription to run and enter High and Low **Severity** values.
7. Click **Next** to display the Qualified Name and Node Type for your OPC A&E server.
8. Click **Done** to create the subscription.

### [Configure Subscription](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#configure-subscription)

Click the name of the subscription on the Browse pane to display a menu that allows you to test, modify, or delete the subscription.

OPC A&E Configure Subscription

1. Select **Test Subscription** to run the subscription and pick up any A&E events.
2. Select **Delete** to delete the subscription immediately.
3. Select **Modify** to change the subscription parameters.

### [View A&E Server Information](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#view-ae-server-information)

After connecting to the A&E server, you can view server information from the Browse pane. Click the **Server** menu to display the options.

OPC A&E View Server Information

#### [Server Status](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#server-status)

1. Select **Server Status** to view information about the server. A display pane opens.
2. The screen shows:

   1. **Start , Current, Update Time:** Time that the OPC A&E server was Startes, Current and Update time.
   2. **Server State:** Show that the server is running
   3. **Status:** Status of data being passed by the server.
   4. **Vendor:** OPC A&E Server Vendor
   5. **Version:** Version of OPC A&E server.
   6. **Update:** Click the **Update** button to refresh the information.

OPC A&E View Server Status

#### [Show Categories](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#show-categories)

###

Show Categories

Select **Server Categories** to display the categories that were selected for the subscription.

### [Show Filters](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#show-filters)

Select **Show Filters** to displays filters that were selected for the subscription.

#### [Add Subscription](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#add-subscription)

Select **Add Subscription** to go to the **<new_subscription>** option and add a subscription to the A&E server.

#### [Browse Address Space](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#browse-address-space)

Select **Browse Address Space** to go to the address space for the A&E server and see if there are other A&E servers on the network.

#### [Save](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#save)

Select **Save** to save any changes you made to the subscription.

## [Test Connectivity](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#test-connectivity)

The OPC Connector contains a built-in test client. You can use this client to verify connectivity to a server.

1. Select **Test DA Servers** from the **Servers** menu on the *OPC Main Form*. OPC sources and their associated groups display on the left. If the server name is green, the test client could connect to the server. If the server name is red, the test client could not connect to the server. $plugin[tuuqgqth4er]
2. Click on a group to start collecting data from that group. You can click different groups and servers. Values display in the panel on the right. $plugin[y3l9003w65w]
3. Click the **Done** button when finished.

## [Download Configuration](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#download-configuration)

You must download all configuration changes on the OPC client to the OPC service before the changes take effect.

The OPC service (*BshoreOPCTxSvc*) is a Windows service that runs unattended on the OPC client. This service collects data from the specified OPC sources and sends that data across NetWall.

If the service is not running, the **Status** and **Download** menus are greyed out on the *OPC Main Form*. When the service is running, select **Download Config to OPC TX Service** from the **Download** menu. An *Update Server* pane displays.

Click **Yes** to send the configuration to the service. The download status displays on the *OPC Main Form*.

## [View Client Events](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#view-client-events)

Click **Events** on the *OPC Main Form* to view events on the OPC client. The Events log displays.

Use the appropriate buttons to **Refresh**, **Clear**, or **Save** the event log. Click the **Done** button to exit the log.

## [View Connection Status](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#view-connection-status)

Click **Status** on the *OPC Main Form* to display the status of the OPC connection.

Click on an OPC source to display the status of the OPC connection and the current number of values received for the last 2-second interval.

## [Configure OPSWAT OPC Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#configure-opswat-opc-server)

This section describes how to configure the OPC server on the RED flanking server to receive data sent across NetWall by the OPC client on the BLUE flanking server.

Installing the OPC Connector on the RED flanking server creates a OPC server instance. Customer-owned OPC clients (destinations) can connect to that instance to receive read-only data from OPC sources in the NetWall BLUE zone.

Multiple instances can be created, differing in the NetWall Port Number where each instance connects.

Click the OPC Config tool icon on the OPC server. The *OPC Server Configurator* displays:

Click a radio button at the top to determine the data that displays:

- **Registered Servers:** Servers that have been selected to receive OPC data.
- **Wrapper Processes:** Processes installed on the RED flanking server by the Server Wrapper
- **.NET OPC Servers:** OPC servers that are available to be registered

### [Add Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#add-server)

1. Select **Register Server** from the **Tasks** menu. The *Register .NET OPC Server* pane displays. $plugin[bijvik25dgb]
2. Type information in the following boxes (some boxes are auto-populated, but you can change the values):

   1. **.NET OPC Server**: Select a DA or A&E server from the dropdown or click the **Browse** button to locate a different OPC server.
   2. **Wrapper Process**: Select the appropriate wrapper for the DA or A&E server.
   3. **CLSID**: Class ID. A unique identifier created automatically for every OPC server. Click the **New** button to generate a new Class ID.
   4. **Prog ID**: Unique ID for this OPC server. Type the desired value.
   5. **Description**: Meaningful description for the server
   6. **Specifications**: Type of OPC server
   7. **Port Number**: NetWall RED port number
3. Enter the **Port Number** for the NetWall RED server.
4. Click to enable **Tracing** if desired. Refer to “Tracing” for more information.

   1. If you enable tracing, enter or browse to locate the **Trace Path**, and enter the name of the **Trace Point**.
5. Click the **OK** button to save the server configuration and return to the *OPC Server Configurator.*
6. Repeat this process for each instance that you want to create.
7. Click the **Exit** button to close the tool.

### <Tracing>

Tracing can be used to monitor the OPC server for a single point.

In the following example, **Enable Trace** was selected, an output folder was specified, and a **Trace Point** was entered (Bucket Brigade Array of Real 8). You can change the Trace Point only when your OPC client is disconnected from the RED flanking server.

The output file has a .*txt* extension, but the values are comma separated so you can import them into a spreadsheet.

Trace output in the trace file appears as follows:

`comparison list for Dynamic/Analog Types/dbt0007`

`Event Source Value Time Event Time Value`

`ValUpd 11:27:14.698 11:27:08.187 74.4310620748477`

`Subscr,11:27:14.698,11:27:08.193,74.4310620748477`

`ValUpd,11:27:14.798,11:27:08.296,76.1249282357974`

`Subscr,11:27:14.798,11:27:08.301,76.1249282357974`

`ValUpd,11:27:14.899,11:27:08.387,77.7785116509801`

`Subscr,11:27:14.899,11:27:08.398,77.7785116509801`

`ValUpd,11:27:15.001,11:27:08.492,79.3892626146237`

`Subscr,11:27:15.001,11:27:08.494,79.3892626146237`

### [Edit or Delete Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#edit-or-delete-server)

To edit or delete a server, right-click the server and select **Edit** or **Delete** from the menu.

### [Export Server](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#export-server)

To export the server contents as a .*xml* file, select **Export Registered Servers** from the **Tasks** menu and browse to the desired location.

### [View Server Events](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#view-server-events)

To view events on the OPC server, click **Events** on the OPC Configurator. The event log displays.

Click the appropriate button to **Refresh**, **Clear**, or **Save** the event log.

## [Using the Customer OPC Client](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#using-the-customer-opc-client)

After installing the OPC Connector and configuring data collection, you can use a standard OPC client to connect to the OPC server and view the statistics for the OPC Connector as a series of OPC Points.

The following images show example output with an OPC client simulator.

## [DCOM Configuration on RED side](/docs/netwalldiode/v1.13.2/opcda-connector/opc-da-connector#dcom-configuration-on-red-side)

For best operability with existing software, *BshoreOPCServerWrap.msi* has been consciously made 32-bit as most existing DA clients are 32-bit software. However, it is likely that a user runs the *BshoreOPCServerWrap.msi* on a 64-bit machine. This leads to a bit of confusion, since some 32-bit DCOM servers cannot be found easily.

Check the steps to launch the 32-bit DCOM config console:

1. Use OPSWAT’s RED OPC configuration utility to create the DA server of your choice, in this example – we will be configuring the “OPSWAT_Schneider_ 27000” server.

2. Press the “Windows” button or in the Search box, type:**mmc -32** (that is: mmc [space] -32). This command launches MMC in 32-bit mode. Once launched, it will bring application such as:

3. From the Menu – select “File -> Add or Remove Snap-Ins” (or press CTRL+M). Select “Component Services” and click “Add >” button.

4. Walk through the items and find the service of interest (in this example, OPSWAT_Schneider_27000).

5. Right click the service and proceed with the desired configuration.

This process would allow you to configure any of the OPSWAT OPC DA DCOM services on the RED Flanker.

MetaDefender
