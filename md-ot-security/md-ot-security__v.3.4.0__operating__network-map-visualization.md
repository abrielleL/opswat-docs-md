<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/network-map-visualization -->

# Network Map

First, users need to select a sensor from the list at the top-right corner.

The network map tab is accessible under **Investigate → Network map.**

The network map feature will help user to visualize the network graph in the system, the relationships between entities and easy to understand how and whether entities are connected.

This feature has visible entities below:

- Device nodes.
- Device links.
- Device connections.
- Protocol's flow.
- Cluster boundary.

There are two type of network map: Cluster and Purdue Model.

Cluster

Purdue Level

On the top left of the screen, there is a small menu: the user can click on it to expand its interface. The user can turn on/off display preferences and create asset.

## [Device node](/docs/md-ot-security/v.3.4.0/operating/network-map-visualization#device-node)

A device node can represent either a single machine in the network, such as a HMI, PLC, SCADA or switch, server…

User can see device information by click/touch on the device node. There are two kind of device information: basic and detail.

### [The basic information](/docs/md-ot-security/v.3.4.0/operating/network-map-visualization#the-basic-information)

The basic device information includes device name, exposure score, IP address, MAC address, purdue model, type, sub-type, mfr./brand, product/model, hardware cpu, hardware version, article/part number, country of origin of NIC, site, status, criticality, OS/firmware, OS description, OS version, OS revision, OS kernel.

### [The detail information](/docs/md-ot-security/v.3.4.0/operating/network-map-visualization#the-detail-information)

On the left side, user can see more onboarded time and discovery agent information.

On the right side there are 5 tabs contained related device information: connections, open port/protocols, vulnerability, alert and update history.

1. Connections

This tab will show all connection information that related to the device user is focusing.

The network connection graph will indicate what device is having connection with the current device, which protocol and the direction of protocol.

The pie chart indicates the percentage of protocol that the device is using. The chart color is also based on the protocol color.

Below is the connection list with more detail about the connections:

- Counterpart IP: destination device.
- Counterpart Port: destination port.
- Direction: the direction of protocol between source and destination device.
- IP: source device (focused device).
- My port: port of focused device.
- Protocol: all protocols that used to communicate on this device.
- Started: time of the connection is established.
- Duration: communication time of connection.
- Data length: packet length.
- Status: status of connection (up/down).

2. Open Port/Protocols

This tab indicates the current open port and protocols on the device. *(Refer to Device Manipulation for more detail.)*

3. Vulnerability

This tab indicates the Unpatched CVE that the device is being violated. *(Refer to Device Manipulation for more detail.)*

4. Alert

This tab is used to check if this device used to be alerted. The alert information is same with alert list page. *(Refer to Device Manipulation for more detail.)*

5. Update history.

This tab will track the device property changing. User can follow from old to new value. *(Refer to Device Manipulation for more detail.)*

## [Device link](/docs/md-ot-security/v.3.4.0/operating/network-map-visualization#device-link)

A device link (straight line) represents for the physical link between two devices. The device link is created based on the IP range of network device that the device is connecting to. That mean, user **must** define the subnet mask for network device so that MetaDefender OT Security can create the physical link automatically.

If the device is become inactive, the physical link will be gray.

User can show/hide physical link by check/uncheck Show physical links on tooltips button.

## [Device connections](/docs/md-ot-security/v.3.4.0/operating/network-map-visualization#device-connections)

A device connection (dash line) represents for the connection between two devices. One device can have one or more connection to one device. User can click/touch on the connection to see more detail.

The header graph indicates the connection direction.

On Current connections tab, user can see the active connection with status is “Up”. If all connections are down, it will be moved to the past connection. In this time on the network map, the connection link is blurred, and it is unclickable. After **5** mins, if there is no connection on the device anymore, the connection link will be removed on graph.

On Past connections tab, user can see the inactive connection with status is “Down”.

If the device is become inactive, the connection will also be gray.

User can show/hide connections by check/uncheck “Show connections” on tooltips button.

## [Protocol](/docs/md-ot-security/v.3.4.0/operating/network-map-visualization#protocol)

A protocol is a particle moving on the connection between 2 devices.

One device can have multiple connections to another device. In this case, on graph just only show one connection but many particles which represent multiple protocols/services.

User can have a quick overview what protocols are on the connection by hover on that connection.

The particle direction indicates the direction where the device is communicating to.

The protocol color can be set at protocol setting.

User can show/hide protocol direction by check/uncheck Show protocol flow on tooltips button.

## [Cluster](/docs/md-ot-security/v.3.4.0/operating/network-map-visualization#cluster)

A cluster is a group of devices. A cluster is defined based on the IP range of the network device.

User can show/hide cluster by check/uncheck “Show cluster’s boundary” on tooltips button.
