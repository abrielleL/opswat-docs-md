<!-- source: https://www.opswat.com/docs/mdtransferguard/netwall-TG/1-metadefender-TG-introduction -->

# MetaDefender Diode X Introduction

Please note that the process to update from 1.9.X to 2.4.X is different than the normal process explained in the Updates section. Please, refer to support in order to update to version 2.0.0.

MetaDefender Diode X ensures uncompromising security for file transfers between networks of different security classifications, providing a secure file scanning and transfer solution that delivers unsurpassed performance, reliability, and security. MetaDefender Diode X integrates OPSWAT’s award-winning MetaDefender Core file sanitization engine. MetaDefender Core thoroughly scans and sanitizes files before they are securely transferred by MetaDefender Diode X over a one-way optical connection across a network security boundary to the desired destination.

MetaDefender Diode X provides hardware-enforced, one-way data transfer between the source and destination networks over a non-routable protocol break, ensuring complete security from network-borne threats. The source and destination servers are referred to as Source (BLUE) and Destination (RED) and are joined by an optical fiber. The fiber facilitates the transfer of non-routable data between the networks. No direct network connection exists between source and destination networks and no routable network information (IP address, MAC address) is exchanged.

The optical fiber performs optical isolation between the two servers. One end of the optical fiber is connected to an optical transmitter on the source domain, and the other end of the optical fiber is connected to an optical receiver on destination domain. The laws of physics, guarantee 100% isolation between the two servers.

## [MetaDefender Diode X Features](/docs/mdtransferguard/netwall-TG/1-metadefender-TG-introduction#metadefender-diode-x-features)

MetaDefender Diode X provides the following features:

- No network connection between source and destination network.
- Full Protocol Break: Only the Data Payload is transferred across the network boundary and data traffic is physically enforced in one way only.
- Integrates MetaDefender Core (MD Core) file sanitization engine.

## [MetaDefender Diode X Components](/docs/mdtransferguard/netwall-TG/1-metadefender-TG-introduction#metadefender-diode-x-components)

MetaDefender Diode X consists of the following components:

- MetaDefender Diode X BLUE and RED User Interface: UI used to configure data flows and transfer parameters.
- MetaDefender Diode X Appliances: Each appliance consists of a 1U server. One appliance services the source network (MetaDefender Diode X BLUE) and the other services the destination network (MetaDefender Diode X RED).
