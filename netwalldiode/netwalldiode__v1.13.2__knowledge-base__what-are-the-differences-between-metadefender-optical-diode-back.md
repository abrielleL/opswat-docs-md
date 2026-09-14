<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/knowledge-base/what-are-the-differences-between-metadefender-optical-diode-back -->

# What are the differences between MetaDefender Optical Diode Back-to-Back and the Bilateral Security Gateway functionality?

This article applies to MetaDefender Optical Diode version 1.11.0 or higher.

This document provides a summary of the main differences between BSG and Optical Diode back-to-back functionality.

|  | **Optical Diode**  **Back-to-back** | **Bilateral Security Gateway** |
| --- | --- | --- |
| Connections | Allows connections to be initiated from either side of the network(e.g. low-to-high or high-to-low) | Connections can only be initiated from one side of the network. Typically from high-to-low. BSG is designed for going high to low. It is not recommended for low to high. |
| Ports | Ports cannot be dynamic | Allows for dynamic ports |
| Applications | Good for:   - RDP - SSH - HTTP - API Calls. No Redirects. - WSUS (local connection) | Depending on how WSUS system is setup (pulling files from low into high, it is a preferred, more secure, solution. Ideal solution for MS SQL & historian replication. |
| [Of appliances](/docs/netwalldiode/v1.13.2/knowledge-base/what-are-the-differences-between-metadefender-optical-diode-back#of-appliances) | 4   - 1 Pair set low-to-high - 1 Pair set high-to-low | 2   - 1 pair typically configured high-to-low. |

Support:

If **Further Assistance** is required or you have any other questions, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).

MetaDefender
