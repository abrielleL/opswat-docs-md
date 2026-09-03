<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/dell-n-seriesos6-layer-3-integration-script -->

# Dell N-Series/OS6 Layer 3 Integration Script

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

PowershellCopyconfig
!
ip access-list impulse_block
permit ip any host 198.31.193.211
!
ip access-list intranet
remark allow DNS
permit udp any any eq domain
remark allow DHCP
permit udp any any eq bootps
remark allow access to AD server (recommended)
permit ip any host x.x.x.x
remark allow access to AV server (recommended if applicable)
permit ip any host x.x.x.x
remark allow access to WSUS server (recommended if applicable)
permit ip any host x.x.x.x
remark allow RDP access to blocked hosts (optional)
permit tcp any eq 3389 any
!
route-map impulse deny 10
match ip address intranet
!
route-map impulse permit 20
match ip address impulse_block
set ip next-hop x.x.x.x (ip address of NAC appliance)
!
sflow 1 destination owner 1 x.x.x.x 50001 (ip address of NAC appliance) sflow 1 polling gigabitethernet x/x/x 15 (L2 interfaces for test VLAN)
sflow 1 sampling gigabitethernet x/x/x 1024 (L2 interfaces for test VLAN)
!
interface fa/gi/vlanX (interface for test subnet) ip policy route-map impulse
ip helper-address x.x.x.x (ip address of NAC appliance)
!
exit
!
exit

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
