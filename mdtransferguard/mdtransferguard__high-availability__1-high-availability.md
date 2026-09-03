<!-- source: https://www.opswat.com/docs/mdtransferguard/high-availability/1-high-availability -->

# High Availability

## [Introduction](/docs/mdtransferguard/high-availability/1-high-availability#introduction)

The MetaDefender Diode X High Availability (HA) solution uses two sets of appliances and an appropriate appliance configuration. This ensures a high level of operational performance (uptime and dataflow).

High Availability feature supports the following:

- TCP Streams
- UDP Streams
- MFT (HTTP) Streams
- File Transfer
- Connectors

The strategy for high availability will utilize Active/Standby components, where one appliance will be in Active state at a given time. The other appliance will be in Standby, ready to take over should hardware in the active appliance fail.

## [Hardware Requirements](/docs/mdtransferguard/high-availability/1-high-availability#hardware-requirements)

A pair of MetaDefender Diode X appliances are combined in a logical unit to formulate High Availability. It is required that the NetWall appliances be of same model type and software version are used in the HA pair. Additionally, the switches to which the Diode X appliances are connected to must support multicast switching:

- Two BLUE Diode X.
- Two RED Diode X.
- Two switches supporting multicast switching one for BLUE side and one for the RED side.
- Fiber cables need to be connected as it is displayed in the Figure. Diode X BLUE 1 Fiber 1 should be connected to the corresponding SFP in Diode X RED 1 and Diode X BLUE 1 Fiber 2 should be connected to Diode X RED 2. User should repeat this schema for Diode X BLUE 2 Fiber 1 and Fiber 2, connecting them respectively to Diode X RED 2 and Diode X RED 1.

Important

The switches supporting multicast switching are not provided by OPSWAT.

## [Networking Requirements](/docs/mdtransferguard/high-availability/1-high-availability#networking-requirements)

In order to function properly, ucarp requires a logical/real IP address on each domain of the HA-pair, and a single shared VIP on each domain for the HA-pair. So the IPs needed would be:

- Management IP for each Diode X BLUE.
- Additional IP for each Diode X BLUE.
- Management IP for each Diode X RED.
- Additional IP for each Diode X RED.
- Two Virtual IP (VIP) for Common Address Redundancy Protocol (CARP), one for BLUE side and one for RED side.

A VIP (Virtual IP address) is a shared IP that is used between either two BLUE or two RED Diode X servers. This VIP is only active on one of the Diode X appliances at any given time. The other appliance in the HA-pair, has the VIP interface down which places that VIP interface in standby mode. If a failover event occur, the system will force an election event (the event occurring when hardware failure is detected), and that election event will determine the state of each node’s VIP.

## [High Availability Setup](/docs/mdtransferguard/high-availability/1-high-availability#high-availability-setup)

There are several steps a user should follow to properly configure High Availability.

- Connect the fiber cables as indicated before.
- Configure additional IPs in the 2 BLUE appliances and in the 2 RED appliances.
- Configure Virtual IPs in the 2 BLUE appliances and in the 2 RED appliances.
- Define Primary and Secondary servers.
- Configure Connectors for proper failover management.

### [Configure additional IPs](/docs/mdtransferguard/high-availability/1-high-availability#configure-additional-ips)

As mentioned before, Diode will need an extra IP address per appliance for enabling logical separation between management IP network and the data IP network. This segregation ensures that management Web UI is always accessible on the management IP network. To configure the additional IP go to Advanced -> Networking -> IP Addresses, deploy the Action button and click on Add IP Address, fill in the IP Address and Mask and click on Submit button.

### [Configure Virtual IPs](/docs/mdtransferguard/high-availability/1-high-availability#configure-virtual-ips)

A VIP (Virtual IP address) is required as mentioned before. To configure the VIP go to Advanced -> Networking -> IP Addresses, deploy the Action button and click on Add VIP Address, fill in the mandatory fields click on Submit button.

You need to remember the Security text you define as this should be the same in both Transfer Guard (it should be the same between the two Diode X BLUE and again, the same between the two Diode X RED), so both appliances know they are part of the same HA system. In the image bellow, there is a configuration example.

### [Define Primary Server](/docs/mdtransferguard/high-availability/1-high-availability#define-primary-server)

Once configured both appliances of the HA pair, user can check which one is the Primary appliance and which one is in Standby status in the Dashboard.

User can change this using the Demote button in the Primary appliance Dashboard. Once the user clicks on the Demote button, that appliance would become the secondary and would go to Stand by mode while the other appliance of the HA pair would become the Primary.

### [Configure Connectors](/docs/mdtransferguard/high-availability/1-high-availability#configure-connectors)

Connectors within Diode X are typically designed to be outbound clients (Blue domain and some Red domain) or servers (Red domain). Thus, when the connector is outbound client, no additional configuration is needed to ensure successful failover or election events. In the case where the connector is designed as server (Red domain) the VIP address is the one that should be used for clients that need to connect to it.
