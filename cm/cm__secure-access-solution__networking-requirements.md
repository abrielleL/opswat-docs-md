<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/networking-requirements -->

# Networking Requirements

For My OPSWAT Central Management to successfully provide secure access to protected applications, each of the Gateways and Clients require network access to various Cloud components, as well as to each other. Cloud-based services used by SDP include: STUN (Session Traversal Utilities for NAT), HTTPS APIs, WebSocket APIs, and NTP (Network Time Protocol).

![](https://uploads.developerhub.io/prod/97qW/1nfxwd0vj2ziv5w95qcjvr1ar6zlbhjmb5jor77mjpyi08p2fxkuws4d3wcdsa9i.png)

## Client

### HTTPS APIs

The MetaDefender Endpoint uses HTTPS APIs hosted in the cloud to coordinate connections with My OPSWAT Central Management Gateways. Outgoing traffic should be allowed on port 443/TCP to the following hosts:

- [https://api-us.sdp.opswat.com](https://api-us.sdp.opswat.com) | US environment
- [https://cognito-idp.us-east-2.amazonaws.com](https://cognito-idp.us-east-2.amazonaws.com) | US environment
- [https://cognito-idp.eu-central-1.amazonaws.com](https://cognito-idp.eu-central-1.amazonaws.com) | EU environment
- [https://api-eu.sdp.opswat.com](https://api-eu.sdp.opswat.com) | EU environment

### STUN Servers

STUN services detect public IP addresses and ports for clients. This is critical for SDP to detect where a user’s device is located and to coordinate it's connection to Gateways. Outgoing traffic should be allowed on port 30000/UDP to the following hosts:

| **Production Version** | Address |
| ---- | ---- |
| US Production | 3.128.173.107 18.116.34.83 3.134.96.213 |
| EU Production | 13.48.78.200 13.48.84.113 13.51.158.149 |

### Client-to-Gateway Communication

Client-to-Gateway communication is a crucial part of SDP functioning properly. After initial configurations are obtained from the SDP controller, subsequent communications are between the Client device and the Gateway.

The client will communicate with the Gateway over UDP. The public ports are configurable, but must be forwarded to 30000/UDP and 30001/UDP for each deployed gateway. More information about Gateway port forwards is available in the next section.

| Gateway Port | Description |
| ---- | ---- |
| Port 30000/UDP | Gateways expect to receive most traffic from the Client on port 30000/UDP. |
| Port 30001/UDP | When a connection is initializing, the client may need to send a single packet to open the firewall, on port 30001/UDP. |

## Gateway

### HTTPS APIs

The Secure IT Access Gateway uses HTTPS APIs hosted in the cloud to coordinate connections and access for SDP Clients. Outgoing traffic from the Gateway should be allowed on port 443/TCP to the following hosts:

- [https://api-us.sdp.opswat.com](https://api-us.sdp.opswat.com) | US environment
- [https://api-eu.sdp.opswat.com](https://api-eu.sdp.opswat.com) | EU environment

### Gateway WebSocket APIs

Secure IT Access Gateways also make use of websockets for bi-directional communication with the SDP Controller. Outgoing traffic from the Gateway should be allowed on port 443/TCP to the following hosts for websocket traffic:

- wss://gateway-websockets-api-us.sdp.opswat.com | US Environment
- wss://gateway-websockets-api-eu.sdp.opswat.com | EU Environment

### STUN Servers

Secure IT Access Gateways also utilize STUN services to automatically discover public IP addresses for Clients to connect to. To allow this outgoing traffic from the Gateway should be allowed on port 30000/UDP to the following hosts:

| **Production Version** | Address |
| ---- | ---- |
| US Production | 3.128.173.107 18.116.34.83 3.134.96.213 |
| EU Production | 13.48.78.200 13.48.84.113 13.51.158.149 |

### Gateway-to-Client Communication

Using STUN services, Gateways and Clients are able to connect through many networks automatically without the need for further configuration. In some cases, however, port-forwards configured in the public firewall may be required to allow Client traffic to successfully reach Gateways. To ensure connectivity, two UDP ports should be forwarded from the public firewall to each Gateway on ports 30000 and 30001. The public ports configured should match the configuration made for each Gateway in the My OPSWAT Central Management console.

| Gateway Port | Description |
| ---- | ---- |
| Port 30000/UDP | Gateways expect to receive most traffic from the Client on port 30000/UDP. |
| Port 30001/UDP | When a connection is initializing, the client may need to send a single packet to open the firewall, on port 30001/UDP. |

### NTP

NTP ensures the system clock of Gateways remains highly accurate. An accurate system clock is required for cryptographic security. Client connections may fail if the Gateway clock and Client clock disagree by more than a few seconds. Traffic should be allowed from Gateways on port 123/UDP to the following pools of public NTP servers (administrators requiring specific addresses for their region can find more information at [ntppool.org](https://www.ntppool.org/zone/@)):

| NTP | Address |
| ---- | ---- |
| OVA | pool.ntp.org |
| AWS | 0.amazon.pool.ntp.org 1.amazon.pool.ntp.org 2.amazon.pool.ntp.org |
| Azure | 2.debian.pool.ntp.org |

## Controller

Network traffic allowed by the administrator for SDP components (Gateway and Client) will prepare the Controller to receive and send information related to new SDP connections and established sessions.

- **HTTPS APIs** - The client and gateway will make API calls over HTTPS.
- **Gateway WebSocket APIs** - The Controller sends real-time updates to the gateway.
- **STUN Servers** - OPSWAT supplies a STUN server to help locate clients and gateways.
- **NTP** - OPSWAT relies on public NTP servers to synchronize gateways.

![](https://uploads.developerhub.io/prod/97qW/ejvjabrjp0kpd9ae60ku0wxww1zf8mbxflb9ntiedm3gl5mtjexpm4o17gkewe03.png)
