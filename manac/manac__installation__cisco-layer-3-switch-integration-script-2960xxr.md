<!-- source: https://www.opswat.com/docs/manac/installation/cisco-layer-3-switch-integration-script-2960xxr -->

# Cisco Layer 3 Switch Integration Script (2960X/XR)

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

PowershellCopyconf t
!
flow record sc-record match ipv4 protocol
match ipv4 source address match ipv4 destination address match transport source-port
match transport destination-port
!
flow exporter sc-exporter
destination x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
transport udp 50001
export-protocol netflow-v5
!
flow monitor sc-monitor exporter sc-exporter record sc-record
!
sampler sc-sampler
mode deterministic 1 out-of 32
!
ip access-list extended impulse_block permit ip any host 198.31.193.211
!
ip access-list extended intranet
remark allow DNS
deny udp any
remark allow any eq
DHCP domain
deny udp any any eq bootps
remark allow access to AD server
deny ip any host x.x.x.x (Replace with IP of AD server and remove this comment)
remark allow access to AV server
deny ip any host x.x.x.x (Replace with IP of AV server and remove this comment)
remark allow RDP access to blocked hosts deny tcp any eq 3389 any
!
route-map impulse permit 10
match ip address intranet
!
route-map impulse permit 20
match ip address impulse_block
set ip next-hop x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
!
interface X (Layer 3 interface(s) which is/are default gateway for subnet(s) to be placed under policy – recommend a test subnet first, remove this comment)
ip policy route-map impulse
ip flow-monitor sc-monitor sampler sc-sampler input
ip helper-address x.x.x.x (replace with IP of NAC appliance and remove this comment)
!
end

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
