<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/brocaderuckusarris-layer-3-integration-script-icx -->

# Brocade/Ruckus/Arris Layer 3 Integration Script (ICX)

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

PowershellCopyconf t
!
sflow sample 128
sflow polling-interval 15
sflow destination x.x.x.x 50001 (replace x.x.x.x with IP of NAC server and remove this comment)
sflow enable
!
ip access-list extended impulse_block permit ip any host 198.31.193.211
!
ip access-list extended intranet remark allow DNS
deny udp any any eq domain c remark allow DHCP
deny udp any any eq bootps remark allow access to AD server
deny ip any host x.x.x.x (Replace with IP of AD server and remove this comment)
remark allow access to AV server
deny ip any host x.x.x.x (Replace with IP of AV server and remove this comment)
remark allow RDP access to blocked hosts deny tcp any eq 3389 any
!
route-map impulse permit 10
match ip address intranet impulse_block
Config t set ip next-hop x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
!
interface X (Layer 3 interface(s) which is/are default gateway for subnet(s) to be placed under policy – recommend a test subnet first, remove this comment)
ip policy route-map impulse
ip helper-address x.x.x.x (replace with IP of NAC
appliance and remove this comment)
!
Interface ethernet X/X/X (Layer 2 ingress interface(s) for subnet(s) to be placed under policy – recommend a test subnet first, remove this comment)
sflow forwarding
!
end

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
