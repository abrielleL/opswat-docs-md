<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/setup/diode-setup -->

# MetaDefender Optical Diode Setup

## [Prerequisites](/docs/netwalldiode/v1.14.0/setup/diode-setup#prerequisites)

### [Hardware Requirements](/docs/netwalldiode/v1.14.0/setup/diode-setup#hardware-requirements)

If any items you are supposed to receive are missing or damaged, contact Support.

You will receive a package from OPSWAT containing one of four hardware form factors:

1. One NetWall 1U Server
2. 2 x 1U NetWall Servers
3. 2 X 1U DELL Enterprise Servers
4. 2 x Din Rail Industrial Computers

Accessories:

- Power Cables.

  - Two for 1U Server
  - Four for 2 x 1U Servers
  - Two for Din Rail
- Fiber Optic Cables.

  - Two for server models
  - One for Din Rail
- Two Security Dongles.
- Mounting Rail Kit (1U Servers only)

In addition, you will need:

- Flathead screwdriver.
- Ethernet cables.

The installation location must provide:

- Access to the USB port on the MetaDefender Optical Diode BLUE node. Ports are available on the front and back of the node.
- 1U or 2 x 1U rack space depending on model.
- 250 Watts power in the rack where the nodes will be installed.

Info

***The included power cables are intended for exclusive use with the NetWall appliance***

## [Installation Procedure](/docs/netwalldiode/v1.14.0/setup/diode-setup#installation-procedure)

Optical Diode installation includes the following steps:

1. Install the servers in the rack.
2. Connect the servers to your system.
3. Connect the servers to each other.
4. Power up each node.

### [Install Servers](/docs/netwalldiode/v1.14.0/setup/diode-setup#install-servers)

Install each server in the rack with the supplied mounting rails, following your local procedures.

The sides containing the USB ports should be toward the front of the rack. You will insert a dongle in the USB port of the Optical Diode BLUE node and the Windows Host computer.

### [Connect Servers](/docs/netwalldiode/v1.14.0/setup/diode-setup#connect-servers)

Warning

- Make sure both servers are powered off before connecting them.
- Stand on an electrostatic mat to connect the nodes.
- Computer cables should always use strain relief to protect the connected equipment from excessive force via the cable. This is especially important for cables between racks.
#### [1U Server for 100Mbps, 1Gbps and 10Gbps](/docs/netwalldiode/v1.14.0/setup/diode-setup#1u-server-for-100mbps-1gbps-and-10gbps)

The following graphic shows the front and rear view of the server.

Front View

Use the following table to connect server to your system. You will not need all available ports for the installation.

| Port Number | Description | Optical Diode Connection |
| --- | --- | --- |
| 1 | Power | BLUE on/off |
| 2 | Security Dongle USB | Must be inserted to perform configuration changes. |
| 3 | Display Port | Connect monitor to access BLUE UI. |
| 4 | RJ45 Port (LAN1) | Optical Diode BLUE: Connect to the trusted network with an Ethernet cable. |
| 5 | RJ45 LAN Port (LAN2) | BLUE Management Port. |
| 6 | Security Dongle USB | Must be inserted to perform configuration changes. |
| 7 | Display Port | Connect to monitor to access the RED UI. |
| 8 | RJ45 LAN Port (LAN3) | Optical Diode RED: Connect to the untrusted network with an Ethernet cable. |
| 9 | RJ45 LAN Port (LAN4) | RED Management Port |
| 10 | Power | RED on/off |
| 11 | Power Supply Unit (Red) | Connect Optical Diode RED to the power supply with power cable. |
| 12 | SFP1 Slot (RX) | Optical Diode RED: Connect the provided fiber to the SFP TX (14). |
| 13 | SFP2 Slot (RX) | Optical Diode RED: Connect the second provided fiber to the SFP TX (15). |
| 16 | Power Supply Unit (Blue) | Connect Optical Diode BLUE to the power supply with power cable. |
| 17 | 10G SFP+ [Blue] | Connect to source network with an ethernet cable. |
| 18 | 10G SFP+ [Blue] | Connect to source network with an ethernet cable. |
| 19 | 10G SFP+ [Red] | Connect to destination network with an ethernet cable. |
| 20 | 10G SFP+ [Red] | Connect to destination network with an ethernet cable. |

#### [2 X 1U Servers for 100Mbps and 1Gbps](/docs/netwalldiode/v1.14.0/setup/diode-setup#2-x-1u-servers-for-100mbps-and-1gbps)

The following graphic shows the front and rear view of the server.

Front View

Back Panel

Use the following table to connect both servers. You will not need all available ports for the installation.

| Port Number | Description | MetaDefender Optical Diode Connection |
| --- | --- | --- |
| 1 | Power supply unit | Connect Optical Diode BLUE and Optical Diode RED to their power supplies with the power cables. |
| 2 | Redundant power supply | Connect Optical Diode BLUE and Optical Diode RED to their power supplies with the power cables. |
| 3 | RJ45 LAN Port (LAN3) | N/A. |
| 4 | COM Port (COM1) | N/A. |
| 5 | COM Port (COM2) | N/A. |
| 6 | RJ45 LAN Port (LAN2) | N/A. |
| 7 | RJ45 LAN Port (LAN1) | Optical Diode BLUE: Connect to the source network with an Ethernet cable.  Optical Diode RED: Connect to the destination network with an Ethernet cable. |
| 8 | Line In | N/A |
| 9 | SFP1 Slot | Optical Diode BLUE: Connect the provided fiber to the SFP TX here.  Optical Diode RED: Connect the other end of the provided fiber to the SFP RX here. |
| 10 | SFP2 Slot | Optical Diode BLUE: Connect a second provided fiber to the redundant SFP TX here.  Optical Diode RED: Connect the other end of the second provided fiber to the redundant SFP RX here. |
| 11 | USB 3.2 Gen 2 Ports | N/A. |
| 12 | HDMI Port (HDMI1) | Connect to a HDMI monitor to access the CLI. |
| 13 | DisplayPort (DP1) | N/A. |
| 14 | D-Sub Port (VGA1) | Connect to a VGA monitor to access the CLI. |
| 15 | USB 3.2 Gen 2 Port | N/A. |
| 16 | USB 3.2 Gen 2 Type-C Port | N/A. |
| 17 | USB 3.2 Gen 2 Ports | N/A. |
| 18 | Line Out | N/A. |
| 19 | Microphone | N/A. |

#### [DIN Rail Servers for 10, 50 and 100Mbps](/docs/netwalldiode/v1.14.0/setup/diode-setup#din-rail-servers-for-10-50-and-100mbps)

OPSWAT provides the MetaDefender Optical Diode in a Din Rail form factor for industrial environments as mentioned before. Din Rail models support a single optical fiber connection.

C1D2 Installation Requirements

1. The devices are DIN Rail PC, and they are required to be mounted into a suitable enclosure that only can be disassembled or accessed by use of a tool.
2. The devices are suitable for use in Class I, Division 2, Groups A, B, C and D or non-hazardous location only.
3. Temperature Code (T code) – T4
4. Ambient Temperature: -40˚C to 75˚C
5. WARNING - EXPLOSION HAZARD – DO NOT DISCONNECT POWER INPUT TERMINAL WHILE THE CIRCUIT IS LIVE OR UNLESS THE AREA IS KNOWN TO BE FREE OF IGNITABLE CONENTRATIONS.
6. HDMI Display Port is not for use in hazardous locations.
7. The DC input power adapter is not for use in hazardous locations.

The following graphic shows the ports of the server.

Use the following table to connect both servers to your system.

| Port Number | Description | MetaDefender Optical Diode connection |
| --- | --- | --- |
| 1 | Fiber port | Optical Diode Din Rail BLUE: Connect the provided fiber here (SFP TX).  Optical Diode Din Rail RED: Connect the other end of the provided fiber here (SFP RX). |
| 2 | RJ45 LAN Port Bypass pair | Optical Diode Din Rail BLUE: Connect to the trusted network with an Ethernet cable.  Optical Diode Din Rail RED: Connect to the untrusted network with an Ethernet cable. |
| 3 | RJ45 LAN Port Bypass pair | N/A. |
| 4 | RJ45 LAN Port MGMT | Connect to a laptop or desktop with an Ethernet cable for Optical Diode Din Rail management accessing the webUI. |
| 5 | USB 3.0 2 Ports | Connect the provided security dongle here for configuring Optical Diode. |
| 6 | LEDs | HDD Activity Status/ System Status/ System Power/ Redundant Power |
| 7 | Buttons | Reset (Power Cycle) and Power Button |

#### [Dell Server for 1GBPS and 10Gbps](/docs/netwalldiode/v1.14.0/setup/diode-setup#dell-server-for-1gbps-and-10gbps)

The following graphic shows the rear view of the server.

Back Panel

Use the following table to connect both servers to your system. You will not need all of the connections for the Optical Diode installation.

| Port Number | Description | MetaDefender Optical Diode connection |
| --- | --- | --- |
| 1 | Power supply Unit | Connect Optical Diode BLUE and RED to their power supplies with the power cables. |
| 2 | Redundant Power supply Unit. | Connect Optical Diode BLUE and RED to their power supplies with the power cables. |
| 3 | SFP1 | Connect the fiber cable in the available slot. Used for transferring data from BLUE to RED. |
| 4 | SFP2 | Connect the other fiber cable in the available slot. Used for transferring data from BLUE to RED. Redundant path |
| 5 | SFP3 | 10Gb Ethernet |
| 6 | SFP4 slot | 10Gb Ethernet |
| 7 | RJ45 LAN Port (LAN2) | N/A. 1Gb |
| 8 | RJ45 LAN Port (LAN1) | Optical Diode BLUE: Connect to the source network with an ethernet cable. Optical Diode RED: Connect to the destination network with an ethernet cable. |
| 9 | COM Port (COM1) | N/A. |
| 10 | D-Sub Port (VGA1) | Connect to a VGA monitor to access the CLI. |
| 11 | iDRAC Port | N/A. |
| 12 | USB Port (USB1) | Plug in the security dongle in one of the USB ports to configure the appliance. |
| 13 | USB Port (USB2) | Plug in the security dongle in one of the USB ports to configure the appliance. |

### [Connect Servers](/docs/netwalldiode/v1.14.0/setup/diode-setup#connect-servers)

Use the fiber optic cable to connect the servers to each other. Install each end of the simplex fiber jumper into the connector indicated by Port Number 9 in the above table as appropriate based upon server color. If redundant fiber connections are being used, connect the second simplex fiber jumper likewise into the connector indicated by Port Number 10.

### [Power on Optical Diode Appliances](/docs/netwalldiode/v1.14.0/setup/diode-setup#power-on-optical-diode-appliances)

Press the power button on each MetaDefender Optical Diode appliance to power it up. Press each power button a second time to shut down that appliance. You also can reset the appliance pressing the other button placed next to the power button.

### [Basic Configuration via Configuration File](/docs/netwalldiode/v1.14.0/setup/diode-setup#basic-configuration-via-configuration-file)

This feature enables basic configuration parameters to be uploaded via a JSON Configuration File. **It is useful in instances whereby a user is configuring a fleet of Optical Diodes.** Most users should utilize configuration instructions in the [Configuration](/docs/netwalldiode/v1.14.0/configuration/diode-configuration) section of the manual. The feature supports configuring TCP, UDP, HTTPs and Syslog. Other connectors must be configured manually.

#### [Config via Configuration File - BLUE](/docs/netwalldiode/v1.14.0/setup/diode-setup#config-via-configuration-file---blue)

Important

This functionality only works for an initial setup when no Management IP/device has been previously configured.

1. Log in and accept the EULA. You will see the following screen blow.
2. Select the **Config File** button.
3. After selecting the **Config File** button you will see the next screen.
4. Choose the JSON file and select **Upload** to import the JSON Configuration File.

Press Submit and the device will reboot.

#### [Config via Configuration File - RED](/docs/netwalldiode/v1.14.0/setup/diode-setup#config-via-configuration-file---red)

1. Repeat file upload process on Optical Diode RED.
2. Proceed with configuring Connectors in the **Configuration** section.

### [JSON Configuration File Format](/docs/netwalldiode/v1.14.0/setup/diode-setup#json-configuration-file-format)

#### [Basic Configuration](/docs/netwalldiode/v1.14.0/setup/diode-setup#basic-configuration)

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
#### [TCP Configuration - BLUE](/docs/netwalldiode/v1.14.0/setup/diode-setup#tcp-configuration---blue)

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
#### [TCP Configuration - RED](/docs/netwalldiode/v1.14.0/setup/diode-setup#tcp-configuration---red)

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
#### [UDP Configuration - BLUE](/docs/netwalldiode/v1.14.0/setup/diode-setup#udp-configuration---blue)

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
#### [UDP Configuration - RED](/docs/netwalldiode/v1.14.0/setup/diode-setup#udp-configuration---red)

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
#### [HTTP Configuration - BLUE](/docs/netwalldiode/v1.14.0/setup/diode-setup#http-configuration---blue)

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
#### [HTTP Configuration - RED](/docs/netwalldiode/v1.14.0/setup/diode-setup#http-configuration---red)

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
#### [Syslog Configuration - BLUE](/docs/netwalldiode/v1.14.0/setup/diode-setup#syslog-configuration---blue)

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
#### [Syslog Configuration - RED](/docs/netwalldiode/v1.14.0/setup/diode-setup#syslog-configuration---red)

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

MetaDefender
