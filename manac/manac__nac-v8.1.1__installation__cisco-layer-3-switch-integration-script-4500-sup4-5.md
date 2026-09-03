<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/cisco-layer-3-switch-integration-script-4500-sup4-5 -->

# Cisco Layer 3 Switch Integration Script (4500 SUP4-5)

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

PowershellCopyconf t
!
ip flow ingress
ip flow-export version 5
ip flow-export source vlan x (replace x with switch management VLAN number and remove this comment)
ip flow-export destination x.x.x.x 50001 (replace x.x.x.x with IP of NAC server and remove this comment)
!
ip access-list extended impulse_block permit ip any host 198.31.193.211
!
ip access-list extended intranet remark allow DNS
permit udp any any eq domain remark allow DHCP
permit udp any any eq bootps remark allow access to AD server
permit ip any host x.x.x.x (Replace with IP of AD server and remove this comment)
remark allow access to AV server
permit ip any host x.x.x.x (Replace with IP of AV server and remove this comment)
remark allow RDP access to blocked hosts permit tcp any eq 3389 any
!
route-map impulse deny 10 match ip address intranet
!
route-map impulse permit 20 match ip address impulse_block
set ip next-hop x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
!
interface vlan X (user test VLAN) ip policy route-map impulse
ip helper-address x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
!
end

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
