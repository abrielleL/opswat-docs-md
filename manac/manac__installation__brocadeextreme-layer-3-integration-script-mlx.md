<!-- source: https://www.opswat.com/docs/manac/installation/brocadeextreme-layer-3-integration-script-mlx -->

# Brocade/Extreme Layer 3 Integration Script (MLX)

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

PowershellCopyconf t
!
cam-partition profile ipv4
!
filter-change-update-delay 0
!
acl policy
!
force-delete-bound-acl
!
ip access-list extended impulse_block permit ip any host 198.31.193.211
permit ip any host 198.31.193.211
remark allow DNS
deny udp any any eq domain
remark allow
deny udp any DHCP
any eq
bootps
remark allow access to AD server
deny ip any host x.x.x.x (Replace with IP of AD server and remove this comment)
remark allow access to AV server
deny ip any host x.x.x.x (Replace with IP of AV server and remove this comment)
remark allow RDP access to blocked hosts deny tcp any eq 3389 any
!
route-map impulse permit 10
match ip address impulse_block
set ip next-hop x.x.x.x (replace x.x.x.x with IP NAC server and remove this comment)
!
interface ve X (Layer 3 interface(s) which is/are gateway for subnet(s) to be placed under policy – test subnet first, recommend a test subnet first, remove this comment)
ip policy route-map impulse
ip helper-address x.x.x.x (replace with IP of NAC appliance and remove this comment)
!
interface ethernet x/x/x (Layer 2 interface(s) for any layer 3 interface with the route-map applied, remove this comment)
sflow-forwarding
!
sflow enable sflow sample 128
sflow polling-interval 15
sflow destination x.x.x.x 50001 (replace x.x.x.x with IP of NAC server and remove this comment)
!
end

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
