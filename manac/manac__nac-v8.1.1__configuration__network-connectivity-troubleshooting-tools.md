<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/network-connectivity-troubleshooting-tools -->

# Network Connectivity Troubleshooting Tools

As of release 6.5.16 and later, tools to help troubleshoot the connectivity of your appliance within your network are available in the console configuration utility. To access these tools, an admin user with a hardware version of NAC will have to connect a keyboard and a monitor to their NAC appliance and log in with the username of "admin". The console configuration utility should come up. Admin users with virtual environments should access the configuration utility through their VM provider's interface. The image below reflects the list of troubleshooting tools available.

Shell

## [Helpful Tips](/docs/manac/nac-v8.1.1/configuration/network-connectivity-troubleshooting-tools#helpful-tips)

- The Shell allows for the following troubleshooting tools: arp, ifconfig, netstat, nslookup, ping, route, tcpdump, and traceroute.
- Files these tools generate are limited to an overall total of 2 gigabytes in size.
- Individual files are kept for 30 days after they are last accessed.
- Packet captures are made available at <https://portal.myweblogon.com:8443/downloads/troubleshooting/somePacketCaptureCustomerTook.pcap>. “portal.myweblogon.com” can be replaced with the IP address of the NAC appliance or the custom hostname of the appliance if applicable.
- Port Check lets admins troubleshoot whether a TCP connection can be established between an IP address and a port.
