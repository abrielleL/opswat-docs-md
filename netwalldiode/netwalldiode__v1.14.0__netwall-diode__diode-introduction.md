<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/netwall-diode/diode-introduction -->

# MetaDefender Optical Diode Introduction

MetaDefender Optical Diode (hereinafter Optical Diode) provides unidirectional data transfer between networks of differing security classifications (zones). The zones are referred to as BLUE (source) and RED (destination) and are joined by an optic fiber. This fiber facilitates the transfer of non-routable data between the zones. No direct network connection exists and no pertinent network information (IP address, MAC address) is exchanged.

Note

1U Server-based models have redundant optical fiber connections. Din Rail models have a single optical fiber connection.

The optical fiber performs optical isolation between the BLUE and RED servers. One end of the optical fiber is connected to an optical transmitter on the BLUE Source side, and the other end of the optical fiber is connected to an optical receiver on the RED Destination side.

The laws of physics, guarantee 100% isolation between the two networks, and eliminate any possibility of data flow through the computers between domains.

The Source (BLUE) corresponds to the network initiating a communication. The Destination (RED) corresponds to the network receiving a communication.

For example, a water treatment plant has all of its critical systems in the OT (BLUE) high security zone. Areas such as Plant Management and Analytics, Accounting, and Predictive Maintenance are located in the IT (RED) low security zone. In this example, the Optical Diode passes data in a secure manner from the OT zone to the IT zone.

## [Optical Diode Features](/docs/netwalldiode/v1.14.0/netwall-diode/diode-introduction#optical-diode-features)

MetaDefender Optical Diode provides the following features:

- No network connection between inner network and outer network.
- Up to 10Gbit/sec transfer rate using optic fiber.
- Full Protocol Break: Data Payload Only and data traffic physically enforced in one way only (from BLUE to RED).

## [Optical Diode Components](/docs/netwalldiode/v1.14.0/netwall-diode/diode-introduction#optical-diode-components)

MetaDefender Optical Diode consists of the following components:

- MetaDefender Optical Diode BLUE and RED UI: UI used to configure MetaDefender Optical Diode nodes and transfer parameters.
- MetaDefender Optical Diode nodes: Collects and transfers customer data. Each node consists of a 1U server. One node services the BLUE zone (MetaDefender Optical Diode BLUE) and the other services the RED zone (MetaDefender Optical Diode RED).

MetaDefender
