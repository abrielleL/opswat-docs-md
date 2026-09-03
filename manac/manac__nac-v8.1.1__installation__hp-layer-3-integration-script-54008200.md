<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/hp-layer-3-integration-script-54008200 -->

# HP Layer 3 Integration Script (5400/8200)

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

NOTE – This script includes CAM configuration for PBR which requires a switch reload. The reload command is part of the script so the switch will reload when the script is run.

PowershellCopyconfig
!
class ipv4 impulse_block
remark allow-dns
ignore udp any any eq 53
remark allow-dhcp
ignore udp any any eq 68
remark allow access to AD server
ignore ip any x.x.x.x (Replace with IP of AD server and remove this comment)
remark allow access to AV server
ignore ip any x.x.x.x (Replace with IP of AV server and remove this comment)
remark allow-rdp
ignore tcp any eq 3389 any
match ip any 198.31.193.211/32
exit
!
policy pbr impulse
class ipv4 impulse_block
action ip next-hop x.x.x.x (replace x.x.x.x with IP of NAC appliance and remove this comment)
exit
!
vlan x (Layer 3 interface(s) which is/are default gateway for subnet(s) to be placed under policy – recommend a test subnet first, remove this comment)
service-policy impulse in
!
wr me
!
exit

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
