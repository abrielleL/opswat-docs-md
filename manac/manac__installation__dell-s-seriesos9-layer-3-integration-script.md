<!-- source: https://www.opswat.com/docs/manac/installation/dell-s-seriesos9-layer-3-integration-script -->

# Dell S-Series/OS9 Layer 3 Integration Script

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

NOTE – This script includes CAM configuration for PBR which requires a switch reload. The reload command is part of the script so the switch will reload when the script is run.

PowershellCopyconfigure t
!
cam-acl l2acl 1 ipv4acl 1 ipv6acl 0 ipv4qos 1 l2qos 1 l2pt 0 ipmacacl 0
vman-qos 0 ecfmacl 0 ipv4pbr 9
!
ip redirect-list impulse_block
seq 1 permit udp any any eq 53
seq 2 permit udp any any eq 67
seq 3 redirect x.x.x.x ip any host 198.31.193.211 (replace x.x.x.x with IP of NAC server and remove this comment)
!
interface vlan X (Layer 3 interface(s) which is/are default gateway for subnet(s) to be placed under policy – recommend a test subnet first, remove this comment)
ip redirect-group impulse_block
ip helper-address x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
!
sflow collector x.x.x.x agent-addr y.y.y.y 50001 (replace x.x.x.x with IP of NAC server and and y.y.y.y with switch management IP, remove this comment)
sflow enable
sflow polling-interval 15
sflow sample-rate 256
!
interface GigabitEthernet X (Layer 2 interface(s) for any layer 3 interface with the redirect-group applied, remove this comment)
sflow enable
sflow sample-rate 256
!
end
!
wr mem
!
reload

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
