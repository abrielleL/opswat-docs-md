<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/cisco-layer-3-switch-integration-script-3750x -->

# Cisco Layer 3 Switch Integration Script (3750X)

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

In order for policy-based routing to work on the 3750Xs, you will need to ensure that it is configured to use the “desktop dual IPV4 and IPV6 routing template”. Information can be found at:

https://www.cisco.com/c/en/us/td/docs/switches/lan/catalyst3750/software/release/12-2_55_ se/configuration/guide/scg3750/swsdm.html

BashCopyTo check which template is currently configured on the 3750Xs, please issue the following command:
show sdm prefer
If the current template is not the “desktop dual-ipv4-and-ipv6 routing” template, you will need
to change the template and reload the switches.
Please run the script below if the routing template needs to be changed:
conf t
!
sdm prefer dual-ipv4-and-ipv6 routing desktop
!
reload
Once the switch has booted, please issue the following command:
show sdm prefer
The switches should now show the “desktop dual-ipv4-and-ipv6 routing” template in use.

Please proceed with the script on the following page once the routing template has been verified on the switches.

PowershellCopyconf t
!
flow record sc-record match ipv4 version match ipv4 tos
match ipv4 ttl match ipv4 protocol
match ipv4 source address match ipv4 destination address match transport source-port
match transport destination-port
collect counter bytes
collect counter packets
collect timestamp sys-uptime first
collect timestamp sys-uptime last
!
flow exporter sc-exporter
destination x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
transport udp 50001
!
flow monitor sc-monitor exporter sc-exporter record sc-record
cache timeout active 60
!
ip access-list extended impulse_block permit ip any host 198.31.193.211
!
ip access-list extended intranet remark allow DNS
permit udp any any eq domain remark allow DHCP
permit udp any any eq bootps
remark allow access to AD server
permit ip any host x.x.x.x (Replace with IP of AD server and remove this comment)
remark allow access to AV server
permit ip any host x.x.x.x (Replace with IP of AV server and remove this comment)
remark allow RDP access to blocked hosts permit tcp any eq 3389 any
!
route-map impulse permit 10
match ip address intranet
!
route-map match ip impulse address permit 20 impulse_block
set ip next-hop x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
!
int X (Layer 2 interface(s) for any layer 3 interface with the redirect-group applied, remove this comment)
ip flow monitor sc-monitor input
interface X (Layer 3 interface(s) which is/are default gateway for subnet(s) to be placed under policy – recommend a test subnet first, remove this comment)
ip policy route-map impulse
ip helper-address x.x.x.x (replace with IP of NAC appliance and remove this comment)
!
end

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
