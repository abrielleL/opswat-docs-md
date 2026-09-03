<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/operating/network-map-visualization -->

# Network Map

First, users need to select a sensor from the list at the top-right corner.

The network map visualization feature will help users to visualize the network graph in the system, the relationships between entities, and easy to understand how and whether entities are connected.

This feature is visible entities below:

- Device nodes.
- Device connections.
- Protocol flows.

There are two types of network maps: Cluster and Purdue Model.

*(Image could not be embedded — see Confluence)*

*(Image could not be embedded — see Confluence)*

User can Filter by Asset or by Communication Protocol

*(Image could not be embedded — see Confluence)*

*(Image could not be embedded — see Confluence)*

The filtered devices/connections will display in the right window

*(Image could not be embedded — see Confluence)*

## [Device node](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#device-node)

A device node can represent either a single machine in the network, such as an HMI, PLC, SCADA, or switch, server…Users can see device information by clicking on the device node.

*(Image could not be embedded — see Confluence)*

On the left side, the user can see more about the onboarding time and agent information.

On the right side, there are 6 tabs containing related device information: connections, open ports/protocols, vulnerability, alert, update history, and login history.

#### [1. Connections](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#1-connections)

This tab will show all connection information related to the device the user is focusing on.

The network connection graph will indicate which device is having a connection to the current device, which protocol, and the direction of the protocol.

The donut chart indicates the percentage of protocols that the device is using. The chart color is also based on the protocol color.

Below is the connection list with more details about the connections:

- Counterpart IP: destination device.
- Counterpart Port: destination port.
- Direction: the direction of protocol between the source and destination devices.
- IP: source device (focused device).
- My port: port of the focused device.
- Protocol: all protocols that are used to communicate on this device.
- Started: the time of the connection is established.
- Duration: communication time of connection.
- Data length: packet length.
- Status: status of connection (up/down).

#### [2. Open Port/Protocols](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#2-open-portprotocols)

This tab indicates the current open ports and protocols on the device. *(Refer to Device Manipulation for more details.)*

#### [3. Vulnerability](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#3-vulnerability)

This tab indicates the Unpatched CVE that the device is being violated. *(Refer to Device Manipulation for more details.)*

#### [4. Alert](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#4-alert)

This tab is used to check whether the device has previously triggered any alerts. The alert information shown here is the same as on the Alert List page. (Refer to Device Manipulation for more details.)

#### [5. Update history](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#5-update-history)

This tab will track the device property changes. Users can follow from old to new values. *(Refer to Device Manipulation for more details.)*

#### [6. Login history](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#6-login-history)

This tab displays the login history for this device.

## [Device link](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#device-link)

A device link (straight line) represents the physical link between two devices. The device link is created based on the IP range of the network device that the device is connecting to. That means the user **must** define the subnet mask for the network device so that MetaDefender OT Security can create the physical link automatically.

If the device has become inactive, the physical link will be gray.

Users can show/hide physical links by checking/unchecking Show physical links on the tooltips button.

## [Device connections](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#device-connections)

*(Image could not be embedded — see Confluence)*

A device connection (dashed line) represents the connection between two devices. One device can have one or more connections to another device. Users can click/touch on the connection to see more details.

The header graph indicates the connection direction.

On the Current Connections tab, the user can see the active connection with the status “Up”. If all connections are down, they will be moved to the past connection. At this time, on the network map, the connection link is blurred, and it is unclickable. After **5** minutes, if there is no connection on the device anymore, the connection link will be removed from the graph.

On the Past Connections tab, the user can see the inactive connection with the status “Down”.

If the device has become inactive, the connection will also be gray.

Users can show/hide connections by checking/unchecking “Show connections” on the tooltips button.

## [Protocol](/docs/md-ot-security/v4.0.0/operating/network-map-visualization#protocol)

A protocol is a particle moving on the connection between 2 devices.

One device can have multiple connections to another device. In this case, on graph only shows one connection but many particles that represent multiple protocols/services.

Users can have a quick overview of what protocols are on the connection by hovering over that connection.

The particle direction indicates the direction in which the device is communicating.

The protocol color can be set in the protocol settings.

Users can show/hide protocol direction by checking/unchecking Show protocol flow on the tooltips button.
