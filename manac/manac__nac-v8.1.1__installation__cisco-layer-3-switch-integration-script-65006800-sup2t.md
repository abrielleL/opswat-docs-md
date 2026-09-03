<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/cisco-layer-3-switch-integration-script-65006800-sup2t -->

# Cisco Layer 3 Switch Integration Script (6500/6800 SUP2T)

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC** **Router Integration Script**

PowershellCopyconf t
!
flow record sc-record match ipv4 protocol
match ipv4 source address
match ipv4 destination address
match transport source-port
match transport destination-port
!
flow exporter sc-exporter
destination x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
transport udp 50001
export-protocol netflow-v5
!
flow monitor sc-monitor
exporter sc-exporter
record sc-record
!
ip access-list extended impulse_block
permit ip any host 198.31.193.211
!
ip access-list extended intranet
remark allow DNS
permit udp any any eq domain
remark allow DHCP
permit udp any any eq bootps
remark allow access to AD server
permit ip any host x.x.x.x (Replace with IP of AD server and remove this comment)
remark allow access to AV server
permit ip any host x.x.x.x (Replace with IP of AV server and remove this comment)
remark allow RDP access to blocked hosts
permit tcp any eq 3389 any
!
route-map impulse deny 10
match ip address intranet
!
route-map impulse permit 20
match ip address impulse_block
set ip next-hop x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
!
interface X (Layer 3 interface(s) which is/are default gateway for subnet(s) to be placed under policy – recommend a test subnet first, remove this comment)
ip policy route-map impulse
ip flow monitor sc-monitor input
ip helper-address x.x.x.x (replace x.x.x.x with IP of NAC server and remove this comment)
!
end

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
