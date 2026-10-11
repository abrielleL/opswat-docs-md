<!-- source: https://www.opswat.com/docs/netwall/5.14.0/high-availability/untitled -->

# NetWall High Availability

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Introduction](/docs/netwall/5.14.0/high-availability/untitled#introduction)

The NetWall High Availability (HA) product family uses two sets of appliances of the same type (USG or BSG) and an appropriate appliance configuration. This ensures a high level of operational performance (uptime and dataflow).

High Availability feature supports the following:

- TCP Streams
- UDP Streams
- Vault(HTTP) Streams
- File Transfer
- Connectors

The strategy for high availability will utilize Active/Standby components, where one appliance will be in Active state at a given time. The other appliance will be in Standby, ready to take over should hardware in the active appliance fail.

## [Hardware Requirements](/docs/netwall/5.14.0/high-availability/untitled#hardware-requirements)

A pair of NetWall SG appliances will be combined in a logical unit to formulate Netwall HA. The prerequisite is that NetWall SG appliances of same type are used to form the HA pair. Additionally, the switches to which the NetWall SG appliances are connected must support multicast switching:

- Two BLUE NetWall Security Gateways (same kind, USG/BSG, both).
- Two RED NetWall Security Gateways (same kind, USG/BSG, both).
- Two switches supporting multicast switching one for BLUE side and one for the RED side.

## [Networking Requirements](/docs/netwall/5.14.0/high-availability/untitled#networking-requirements)

In order to function properly, ucarp requires a logical/real IP address on each domain of the HA-pair, and a single shared VIP on each domain for the HA-pair. So the IPs needed would be:

- Management IP for NetWall BLUE.
- Additional IP for NetWall BLUE.
- Management IP for NetWall RED.
- Additional IP for NetWall RED.
- Two Virtual IP (VIP) for Common Address Redundancy Protocol (CARP), one for BLUE side and one for RED side.

A VIP (Virtual IP address) is a shared IP that is used between either two BLUE or two RED NetWall computers. This VIP is only active on one of the NetWall appliances at any given time. The other appliance in the HA-pair, has the VIP interface down which places that VIP interface in standby mode. If a failover event occurs, the system will force an election event (the event occurring when hardware failure is detected), and that election event will determine the state of each node’s VIP.

## [High Availability Setup](/docs/netwall/5.14.0/high-availability/untitled#high-availability-setup)

There are several steps a user shoud follow to properly configure High Availability.

- Configure additional IPs in the 2 BLUE appliances and in the 2 RED appliances.
- Configure Virtual IPs in the 2 BLUE appliances and in the 2 RED appliances.
- Define Primary and Secondary servers.
- Configure Connectors for proper failover management.

### [Configure additional IPs](/docs/netwall/5.14.0/high-availability/untitled#configure-additional-ips)

As mentioned before, NetWall will need an extra IP address per appliance for enabling logical separation between management IP network and the data IP network. This segregation ensures that management WebUI is always accesible on the management IP network. To configure the additional IP go to Advanced -> Networking -> IP Addresses, deploy the Action button and click on Add IP Address, fill in the IP Address and Mask and click on Submit button.

### [Configure Virtual IPs](/docs/netwall/5.14.0/high-availability/untitled#configure-virtual-ips)

A VIP (Virtual IP address) is required as mentioned before. To configure the VIP go to Advaced -> Networking -> IP Addresses, deploy the Action button and click on Add VIP Address, fill in the mandatory fields click on Submit button.

You need to remember the Security text you define as this should be the same in both NetWalls (it should be the same between the two NetWalls BLUE and again, the same between the two NetWalls RED), so both appliances know they are part of the same HA system. In the image below, there is a configuration example.

### [Define Primary Server](/docs/netwall/5.14.0/high-availability/untitled#define-primary-server)

Once configured both appliances of the HA pair, user can check which one is the Primary appliance and which one is in Standby status in the Dashboard.

User can change this using the Demote button in the Primary appliance Dashboard. Once the user clicks on the Demote button, that appliance would become the secondary and would go to Stand by mode while the other appliance of the HA pair would become the Primary.

### [Configure Connectors](/docs/netwall/5.14.0/high-availability/untitled#configure-connectors)

Connectors within NetWall are typically designed to be outbound clients (Blue domain and some Red domain) or servers (Red domain). Thus, when the connector is outbound client, no additional configuration is needed to ensure successful failover or election events. In the case where the connector is designed as server (Red domain) the VIP address is the one that should be used for clients that need to connect to it.
