<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/troubleshooting-tools -->

# Troubleshooting Tools

MetaDefender IT-OT Access SDP gateways provide users with basic networking troubleshooting tools to evaluate the health of their gateways. To access these tools, users will require access to the private gateway via SSH (AWS/Azure) or via direct access to the OVA.

Upon accessing the gateway, users will sign into the SDP Gateway Configuration Tool prompt, and navigate to **Tools** using either the mouse or pressing [F10].

| **Troubleshooting Tools** | **Description** |
| --- | --- |
| tcpdump | Monitor network traffic. |
| ping | Detect if destination is reachable via ICMP. |
| stun | Detect public IP address and what kind of NAT is in use, if any. |
| nslookup | Resolve IP address of destination. |
| telnet | Attempt to establish a TCP connection to the destination. |
| traceroute | Attempt to determine the route packets take to the destination. |

Most results that the tools generate will appear on the screen in a pop-up window. **Tcpdump**, being the exception, the dump file is accessible by accessing the provided web address.

***Note: For AWS and Azure gateways, do not attempt to access the web address given within the gateway. Use the public IP address listed in the instance details on AWS/Azure.***
