<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/tcp-streaming-with-netwall-diode/tcp-streaming-with-netwall-diode -->

# TCP Streaming with MetaDefender Optical Diode

## [Introduction](/docs/netwalldiode/v1.14.0/tcp-streaming-with-netwall-diode/tcp-streaming-with-netwall-diode#introduction)

Under normal (non-Diode) circumstances, TCP protocol guarantees delivery and avoids data loss. But TCP Protocol handshaking and control requires bi-directional communications between the initiating TCP Data Sender and the responding TCP Data Receiver. This bi-directional communication is not possible in MetaDefender Optical Diode because a Data Diode, by definition, implements a physically enforced one-way communication.

In this document, we will explain How MetaDefender Optical Diode handles these situations and what strategies OPSWAT have implemented to minimize data loss.

## [TCP in a one-way environment](/docs/netwalldiode/v1.14.0/tcp-streaming-with-netwall-diode/tcp-streaming-with-netwall-diode#tcp-in-a-one-way-environment)

The Trusted (BLUE) side of MetaDefender Optical Diode establishes a Read TCP connection with the specified data source on the Trusted network and reads data from the data source. That data is transmitted across the fiber optic link in a proprietary non-routable packet format to the UnTrusted (RED) side of the Data Diode. The RED side of the Data Diode establishes a Write TCP connection with the specified data destination on the UnTrusted network and then streams the data from BLUE via TCP to the specified destination.

If the RED side is not able to transmit data to its specified destination as quickly as the BLUE side is transmitting, then RED must buffer that data. If this situation persists, then RED will be overrun with data as it runs out of buffer space. Buffer overrun results in data loss.

Several mechanisms can be implemented to reduce data loss due to buffer overrun:

- Control of the bit rate for a TCP Stream on BLUE.
- Control of the buffer size for a TCP Stream on RED.

These mechanisms are available via the OPSWAT MetaDefender Optical Diode Web Interfaces on both the BLUE and the RED MetaDefender Optical Diode appliances.

### [Bit Rate Control](/docs/netwalldiode/v1.14.0/tcp-streaming-with-netwall-diode/tcp-streaming-with-netwall-diode#bit-rate-control)

A TCP Stream or a collection of TCP Streams configured for a given TCP Port connection on BLUE can be constrained to a specific bit rate. This slows down the transmission rate of data across the Diode and alleviates potential data loss due to overrun on RED.

Bit Rate Control is configured using the OPSWAT MetaDefender Optical Diode Web Interface on the BLUE side. Having smaller bitrates would alleviate data overruns but notice that data transfer would be slower as well.

### [Buffer Size Control](/docs/netwalldiode/v1.14.0/tcp-streaming-with-netwall-diode/tcp-streaming-with-netwall-diode#buffer-size-control)

All TCP data transmitted from BLUE to RED is accumulated in a buffer on RED. Each TCP Stream or a collection of TCP Streams configured for a given TCP Port connection on RED has its own buffer. Each buffer entry is a block of data, where the block ranges from one to several thousand bytes.

Buffer size is configured using the OPSWAT MetaDefender Optical Diode Web Interface on the RED side. The default size of the buffer is 5000 entries and the size of an entry would be from 1 to 9000 Bytes. Having bigger buffers would alleviate data overrrun in RED side, but notice that this would consume sytem memoy as well.

## [File Transfers](/docs/netwalldiode/v1.14.0/tcp-streaming-with-netwall-diode/tcp-streaming-with-netwall-diode#file-transfers)

OPSWAT MetaDefender Optical Diode can be configured for transferrng files from BLUE to RED. If OPSWAT MetaDefender Optical Diode system is doing a lot of File transfers, the file transfers can consume bandwidth and other Data Diode resources to the point that it encroaches on TCP Stream performance.

OPSWAT MetaDefender Optical Diode provides a priority mechanism (High, Medium, Low) designed to limit the resources consumed by File Transfer. This throttling mechanism can lower the impact of large volume file transfers as well as compensate for a RED destination File Server that operates slower than the BLUE source File Server.

MetaDefender
