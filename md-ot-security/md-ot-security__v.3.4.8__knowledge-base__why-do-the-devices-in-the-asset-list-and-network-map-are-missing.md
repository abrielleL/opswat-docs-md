<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/knowledge-base/why-do-the-devices-in-the-asset-list-and-network-map-are-missing -->

# Why do the devices in the Asset List and Network Map are missing in MetaDefender OT Security?

In OT Security Management, the **Asset List** and **Network Map** serve distinct purposes, which can lead to differences in the number of displayed devices.

### [**Network Map**](/docs/md-ot-security/v.3.4.8/knowledge-base/why-do-the-devices-in-the-asset-list-and-network-map-are-missing#network-map)

The Network Map visualizes all devices that OT Security has detected across the network. This includes routers, switches, and other network infrastructure components. However, if a device is behind a router, OT Security may only detect the router’s **MAC address** rather than the individual devices connected to it. This behavior is expected because OT Security identifies devices based on MAC address data.

### [**Asset List**](/docs/md-ot-security/v.3.4.8/knowledge-base/why-do-the-devices-in-the-asset-list-and-network-map-are-missing#asset-list)

The Asset List provides detailed information on recognized devices that OT Security has fully identified, including their MAC addresses. Since devices behind a router may not have their MAC addresses directly visible, they **will not appear** in the Asset List. This is a key reason why the number of assets listed differs from the number of devices shown in the Network Map.

### [**Possible Reasons for Missing Devices in the Asset List**](/docs/md-ot-security/v.3.4.8/knowledge-base/why-do-the-devices-in-the-asset-list-and-network-map-are-missing#possible-reasons-for-missing-devices-in-the-asset-list)

1. **Devices Are Behind a Router** – OT Security detects the router’s MAC address instead of the individual devices behind it.
2. **No Active Communication and Active Scanning Is Not Enabled** – If devices are not actively communicating on the network, and **Active Scanning** is not enabled, OT Security relies on passive network monitoring, which may not capture all devices.

To verify if missing devices are behind a router, check their network positioning and consider enabling Active Scanning to enhance detection.
