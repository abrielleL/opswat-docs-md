<!-- source: https://www.opswat.com/docs/netwall/v5.13.2/setup/netwall-setup -->

# MetaDefender Security Gateway Setup

## [Prerequisites](/docs/netwall/v5.13.2/setup/netwall-setup#prerequisites)

| Parameter | Limits |
| --- | --- |
| Temperature | -10-35ºC Operating -40-65ºC Non-Operating |
| Humidity | 5-95% non-condensing, Non-Operating 10-80% RH, Operating |

| Item | Limits |
| --- | --- |
| Type / Watts | 250 Watts |

### [Hardware requirements](/docs/netwall/v5.13.2/setup/netwall-setup#hardware-requirements)

If any items you are supposed to receive are missing or damaged, contact Support.

You will receive a package from OPSWAT containing the following:

- Two 1U servers.
- Mounting rail kits.
- Two power cables.
- One PCI cable.
- Two security dongles.

In addition, you must have:

- Flathead screwdriver.
- Ethernet cables.

The installation location must provide:

- Access to the USB port on the MetaDefender Security Gateway BLUE node. Ports are available on the front and back of the node.
- 2 x 1U rack space.
- 250 Watts power in the rack where the nodes will be installed.

Info

***The included power cables are intended for exclusive use with the NetWall appliance***

## [Installation procedure](/docs/netwall/v5.13.2/setup/netwall-setup#installation-procedure)

MetaDefender Security Gateway node installation includes the following steps:

1. Install the servers in the rack.
2. Connect the servers to your system.
3. Connect the servers to each other.
4. Power up each node.

### [Install servers in the rack](/docs/netwall/v5.13.2/setup/netwall-setup#install-servers-in-the-rack)

Install each server in the rack with the supplied mounting rails, following your local procedures.

The sides containing the USB ports should be toward the front of the rack. You will insert a dongle in the USB port of the MetaDefender Security Gateway BLUE node and the Windows Host computer.

### [Connect servers to you system](/docs/netwall/v5.13.2/setup/netwall-setup#connect-servers-to-you-system)

The following graphic shows the rear view of the server.

Use the following table to connect both servers to your system. You will not need all of the connections for the MetaDefender Security Gateway installation.

| Port Number | Description | MetaDefender Security Gateway connection |
| --- | --- | --- |
| 1 | Power supply Unit | Connect MetaDefender Security Gateway BLUE and MetaDefender Security Gateway RED to their power supplies with the power cables. |
| 2 | Redundant Power supply Unit | Connect MetaDefender Security Gateway BLUE and MetaDefender Security Gateway RED to their power supplies with the power cables. |
| 3 | RJ45 LAN Port (LAN3) | N/A. |
| 4 | COM Port (COM1) | N/A. |
| 5 | COM Port (COM2) | N/A. |
| 6 | RJ45 LAN Port (LAN2) | N/A. |
| 7 | RJ45 LAN Port (LAN1) | MetaDefender Security Gateway BLUE: Connect to the trusted network with an Ethernet cable.  MetaDefender Security Gateway RED: Connect to the untrusted network with an Ethernet cable. |
| 8 | Line In | N/A. |
| 9 | PCIe card slot |  |
| 10 | USB 3.2 Gen 2 Ports | N/A. |
| 11 | HDMI Port (HDMI1) | Connect to a HDMI monitor to access the CLI. |
| 12 | DisplayPort (DP1) | N/A. |
| 13 | D-Sub Port (VGA1) | Connect to a VGA monitor to access the CLI. |
| 14 | USB 3.2 Gen 2 Type-C Port | N/A. |
| 15 | USB 3.2 Gen 2 Port | N/A. |
| 16 | USB 3.2 Gen 2 Ports | N/A. |
| 17 | Line Out | N/A. |
| 18 | Microphone | N/A. |

### [Connect servers to each other](/docs/netwall/v5.13.2/setup/netwall-setup#connect-servers-to-each-other)

Use the PCI cable to connect the servers to each other. Install the cable connector on each end of the PCI cable into the connector, indicated by ‘9’ on the above table, on each server.

Warning

- Make sure both servers are powered off before connecting them.
- Stand on an electrostatic mat to connect the nodes.
- Computer cables should always use strain relief to protect the connected equipment from excessive force via the cable. This is especially important for cables between racks.
### [Power up Security Gateway appliances](/docs/netwall/v5.13.2/setup/netwall-setup#power-up-security-gateway-appliances)

Press the power button (indicated in the picture below) on each MetaDefender Security Gateway appliance to power it up. Press each power button a second time to shut down that appliance. You also can reset the appliance pressing the other button placed to the right.

### [Basic Configuration via Configuration File](/docs/netwall/v5.13.2/setup/netwall-setup#basic-configuration-via-configuration-file)

This feature enables basic configuration parameters to be uploaded via a JSON Configuration File. **It is useful in instances whereby a user is configuring a fleet of security Gateways.** Most users should utilize configuration instructions in the [Configuration](/docs/netwall/v5.13.2/configuration/configuration) section of the manual. The feature supports configuring TCP, UDP, HTTPs and Syslog. Other connectors must be configured manually.

#### [Config via Configuration File BLUE](/docs/netwall/v5.13.2/setup/netwall-setup#config-via-configuration-file-blue)

Info

This functionality only works for an initial setup when no Management IP/device has been previously configured.

1. Log in and accept the EULA. You will see the following screen blow.
2. Select the **Config File** button.
3. After selecting the Config File button you will see the next screen.
4. Choose the JSON file and select **Upload** to import the JSON Configuration File.

Press Submit and the device will reboot.

#### [Config via Configuration File RED](/docs/netwall/v5.13.2/setup/netwall-setup#config-via-configuration-file-red)

1. Repeat file upload on Security Gateway RED
2. Proceed with configuring Connectors in the Configuration section.

### [JSON Configuration File Format](/docs/netwall/v5.13.2/setup/netwall-setup#json-configuration-file-format)

#### [Basic Configuration](/docs/netwall/v5.13.2/setup/netwall-setup#basic-configuration)

JsonCopy{
"version": 1,
"settings": {
"management_ip": "192.0.2.10",
"gateway": "192.0.2.1",
"net_mask": "255.255.255.0",
"hostname": "optical-diode-1",
"dns_server_1": "1.1.1.1",
"dns_server_2": "8.8.8.8",
"ntp_server_1": "time.google.com",
"ntp_server_2": "203.0.113.5",
"time": "2025-12-04 14:33:21",
"time_zone": "US/Eastern",
"dns_suffix_search": "example.com",
"ssh_enabled": true,
"forward_syslog_red": false
},
"streams": []
}
#### [TCP Configuration - BLUE](/docs/netwall/v5.13.2/setup/netwall-setup#tcp-configuration---blue)

JsonCopy{
"channelnumber": 1,
"name": "tcp-example",
"protocol": "TCP",
"enabled": true,
"bilateral": false,
"description": "TCP example (blue)",
"port": 80,
"ipaddress": "10.0.0.0/24;web.blue.local",
"max_sessions": 5,
"bitrate": 10000000
}
#### [TCP Configuration -RED](/docs/netwall/v5.13.2/setup/netwall-setup#tcp-configuration--red)

JsonCopy{
"channelnumber": 10,
"name": "egress-tcp",
"protocol": "TCP",
"enabled": true,
"bilateral": false,
"description": "TCP example (red)",
"port": 443,
"ipaddress": "example.com",
"max_sessions": 10,
"terminate_on_fail": true,
"max_buffer_items": 200
}
#### [UDP Configuration - BLUE](/docs/netwall/v5.13.2/setup/netwall-setup#udp-configuration---blue)

JsonCopy{
"channelnumber": 2,
"name": "udp-example",
"protocol": "UDP",
"enabled": true,
"bilateral": false,
"description": "DNS over UDP (blue)",
"port": 53,
"ipaddress": "10.0.0.10",
"bitrate": 10000000
}
#### [UDP Configuration - RED](/docs/netwall/v5.13.2/setup/netwall-setup#udp-configuration---red)

JsonCopy{
"channelnumber": 11,
"name": "egress-udp",
"protocol": "UDP",
"enabled": true,
"bilateral": false,
"description": "DNS over UDP (red)",
"port": 53,
"ipaddress": "192.168.20.20",
"terminate_on_fail": true,
"max_buffer_items": 200
}
#### [HTTP Configuration - BLUE](/docs/netwall/v5.13.2/setup/netwall-setup#http-configuration---blue)

JsonCopy{
"channelnumber": 3,
"name": "http-app",
"protocol": "HTTP",
"enabled": true,
"bilateral": false,
"description": "HTTP service (blue)",
"port": 8080,
"ipaddress": "10.0.1.0/24;192.168.10.20",
"response_delay": 50,
"server_crypto": "",
"max_sessions": 20,
"bitrate": 10000000
}
#### [HTTP Configuration - RED](/docs/netwall/v5.13.2/setup/netwall-setup#http-configuration---red)

JsonCopy{
"channelnumber": 12,
"name": "http-service",
"protocol": "HTTP",
"enabled": true,
"bilateral": false,
"description": "HTTP service (red)",
"port": 8080,
"ipaddress": "service.red.local",
"response_delay": 120,
"client_crypto": false,
"max_sessions": 20,
"terminate_on_fail": true,
"max_buffer_items": 200
}
#### [Syslog Configuration - BLUE](/docs/netwall/v5.13.2/setup/netwall-setup#syslog-configuration---blue)

JsonCopy{
"channelnumber": 4,
"name": "syslog-blue",
"protocol": "SYSLOG (UDP)",
"enabled": true,
"bilateral": false,
"description": "Syslog source on blue",
"port": 514,
"ipaddress": "log.blue.local",
"bitrate": 10000000
}
#### [Syslog Configuration - RED](/docs/netwall/v5.13.2/setup/netwall-setup#syslog-configuration---red)

JsonCopy{
"channelnumber": 13,
"name": "syslog-red",
"protocol": "SYSLOG (UDP)",
"enabled": true,
"bilateral": false,
"description": "Syslog forwarding (red)",
"destination": [
{ "ipaddress": "198.51.100.10", "port": 514, "protocol": "UDP" },
{ "ipaddress": "198.51.100.11", "port": 514, "protocol": "TCP" }
],
"terminate_on_fail": true,
"max_buffer_items": 200
}
##
