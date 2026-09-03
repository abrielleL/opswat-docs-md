<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/cisco-wired-layer-2-integrationfy5 -->

# Cisco Wired Layer 2 Integration(IE2000)

Note – In this example, a Cisco IE-2000-4TS-B configuration is provided. However, any Cisco IE Layer 2 switch supporting the following features are eligible for integration:

- RADIUS Authentication/Accounting
- 802.1X
- MAC Authentication Bypass (MAB)
- RADIUS Change of Authorization (CoA)
- Cisco-AVPair “url-redirect”
- Cisco-AVPair “url-redirect-acl”

Note – In this example the NAC RADIUS Server / Policy Server is 10.10.10.10 (replace this IP with the IP of your NAC system)

Note – Replace the VLAN number on the example port configuration with the desired default VLAN for the port.

Note – The “radius-server vsa send authentication” command is enabled by default and auto-generated on some IOS

versions. If the command does not show up in a sh run, “sh run all” can be used to verify that it is configured on the

switch.

Layer 3 DHCP prerequisites

BashCopyinterface vlanX (Layer 3 interface for enforced network)
ip helper-address X.X.X.X (DHCP server)
ip helper-address X.X.X.X (IP address of NAC Enforcer)
!
End

Layer 2 Switch Configuration

BashCopyaaa new-model
aaa authentication dot1x default group radius
aaa authorization network default local group radius
aaa accounting dot1x default start-stop group radius
aaa session-id common
aaa accounting update newinfo periodic 10
!
aaa server radius dynamic-author
client 10.10.10.10 server-key XXXXX
port 3799
auth-type any
!
dot1x system-auth-control
ip device tracking
!
interface GigabitEthernetX/X/X (replace with interface number)
description NAC User Test Port
switchport access vlan X (replace with desired default VLAN for port)
switchport mode access
ip access-group sc_initial_acl in
authentication port-control auto
mab
dot1x pae authenticator (only required if endpoints are configured for 802.1X)
dot1x timeout tx-period 15
dot1x max-reauth-req 1
authentication host-mode multi-auth
!
ip http server
ip http secure-server
ip radius source-interface X (Layer 3 management interface)
!
ip access-list extended sc_initial_acl
permit ip any any
!
ip access-list extended sc_quarantine_acl
remark allow dns and dhcp
deny udp any any eq domain
deny udp any any eq bootps
remark do not redirect web traffic destined for NAC appliance
deny tcp any host 10.10.10.10 eq www
deny tcp any host 10.10.10.10 eq 443
deny tcp any host 10.10.10.10 eq 8443
deny tcp any host 198.31.193.211 eq www
deny tcp any host 198.31.193.211 eq 443
deny tcp any host 198.31.193.211 eq 8443
remark do not redirect web traffic destined for the redirect URL
www.customerwebsite.com (replace x’s below with website address)
deny tcp any host x.x.x.x eq www
deny tcp any host x.x.x.x eq 443
deny tcp any host x.x.x.x eq 8443
permit ip any any (redirect all other traffic)
!
radius-server NAC
address 10.10.10.10 auth-port 1812 acct-port 1813
key XXXXX
radius-server vsa send authentication
!
End
Examples of other types of ACL exceptions (if required):
remark allow PXE boot
deny udp any host x.x.x.x eq tftp
deny udp any host x.x.x.x range 1025 5000
remark allow authentication to domain controller
deny tcp any host x.x.x.x eq 53
deny udp any host x.x.x.x eq 53
deny tcp any host x.x.x.x eq 88
deny udp any host x.x.x.x eq 88
deny udp any host x.x.x.x eq 123
deny tcp any host x.x.x.x eq 135
deny udp any host x.x.x.x eq 137
deny tcp any host x.x.x.x eq 139
deny tcp any host x.x.x.x eq 389
deny udp any host x.x.x.x eq 389
deny tcp any host x.x.x.x eq 445
deny udp any host x.x.x.x eq 445
deny tcp any host x.x.x.x eq 3268
