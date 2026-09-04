<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/settings/network-topology -->

# Sensor - Network Topology

## [Network Topology](/docs/md-ot-security/v.3.4.0/settings/network-topology#network-topology)

**Network Topology** is accessible under **Settings > Network Topology.**

## [**1. View network devices in the system**](/docs/md-ot-security/v.3.4.0/settings/network-topology#1-view-network-devices-in-the-system)

Network devices, including 4 types: *Network device, switch, getaway* and *router* will be displayed as different rectangle boxes in the left column with basic information including *IP range*, *Name,* *IP address* and *MAC address*. These network devices can be automatically discovered by MetaDefender OT Security or manually added by user.

For more details, you can tap on a specific device, device detail pop-up will appear.

*Note*: You can see more detail information by click on the detail button. You can also drag & drop the pop-up by click on the arrow icon nearby.

## [**2. Create network device**](/docs/md-ot-security/v.3.4.0/settings/network-topology#2-create-network-device)

In case the network device has not appeared in the left column (not yet detected by MetaDefender OT Security), you can add that device manually. Just click "Create network device" button on the right corner of the screen. Pop-up Add network device manually will appear.

You can drag & drop the pop-up by click on the arrow icon on the top right corner.

There are 3 required fields when adding a device manually including: Name, Type and IP range. The remaining fields are optional.

After manually adding network device successfully, the device will appear on the left column with other network devices.

*Note:* On adding device successfully, a success message will be displayed. On any errors occur (missing required field, wrong data format, server error…), an error message with the specific error described will be displayed.

## [**3. Edit IP range of network device**](/docs/md-ot-security/v.3.4.0/settings/network-topology#3-edit-ip-range-of-network-device)

You can change the IP of the network device to adjust the links between the network device and other devices in the reality and help MetaDefender OT Security to detect and accurately simulate the devices on network Topology.

Click on a network device that you want to edit its IP range. On device detail pop-up appear, tap on Edit button. After finishing editing the IP range, tap on Save button.

Valid format of IP range field:

- IP address with subnet mask (e.g. 192.168.1.128/24)
- IP range (e.g. 192.168.1.10-192.168.1.100)

*Note:* After pressing the save button, if the IP range field is not in the correct format, an error message will be displayed.

## [**4. Physical link between network devices**](/docs/md-ot-security/v.3.4.0/settings/network-topology#4-physical-link-between-network-devices)

In practice, a system usually consists of a core switch and other assets connected to it. The exact specification of the network topology makes the simulation of the system on Network Topology Visualization clear and easy to follow and monitor, especially when applying the Cluster mode feature.

First, you drag and drop the network device into the main workspace in the middle of the screen. After being dragged into the main workspace, a connect button (square) will appear on each device. Click the connect button at a source device and then click on connect button at the target device, a link will be created between the 2 devices.

To remove the existing link between 2 devices, just hover on that link. An X button will appear, click on it to remove the link. To send the device back to the list network device column, click on X button on the top of the corner.

*Note:*

For the changes to be applied, you need to tap on the Save button. In case you are leaving without saving, MetaDefender OT Security will show a reminder pop-up.

The network devices that in the same network will be connected automatically.
