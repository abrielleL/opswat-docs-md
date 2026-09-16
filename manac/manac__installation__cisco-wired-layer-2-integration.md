<!-- source: https://www.opswat.com/docs/manac/installation/cisco-wired-layer-2-integration -->

# Cisco Wired Layer 2 Integration

Cisco Layer 2 switch configuration example.

In this example, a configuration validated on modern Cisco IOS-XE switches (Catalyst 9200 and 3850, IOS-XE 16.12+) is provided. Any Cisco Layer 2 switch supporting the following features is eligible for integration:

- RADIUS Authentication/Accounting
- 802.1X
- MAC Authentication Bypass (MAB)
- RADIUS Change of Authorization (CoA)
- Cisco-AVPair "url-redirect"
- Cisco-AVPair "url-redirect-acl"

> **Note:** In this example the NAC RADIUS Server / Policy Server is `10.10.10.10` — replace this IP with the IP of your NAC system.
>
> Replace the VLAN number in the example port configuration with the desired default VLAN for the port.
>
> The `radius server <name>` block form shown below is used on IOS-XE 16.x and later. On older switches (IOS 15.2 and earlier) you may instead use the legacy single-line form: `radius-server host 10.10.10.10 auth-port 1812 acct-port 1813 key XXXXX`.

## [Layer 3 DHCP prerequisites](/docs/manac/installation/cisco-wired-layer-2-integration#layer-3-dhcp-prerequisites)

BashCopyinterface vlanX (Layer 3 interface for enforced network)
ip helper-address X.X.X.X (DHCP server)
ip helper-address X.X.X.X (IP address of NAC Enforcer)
!
end
## [Layer 2 switch configuration](/docs/manac/installation/cisco-wired-layer-2-integration#layer-2-switch-configuration)

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
authentication host-mode multi-auth
authentication order dot1x mab
authentication priority dot1x mab
authentication port-control auto
mab
dot1x pae authenticator (only required if endpoints are configured for 802.1X)
dot1x timeout tx-period 15
dot1x max-reauth-req 1
spanning-tree portfast
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
remark do not redirect web traffic destined for the redirect URL www.customerwebsite.com (replace x.x.x.x below with the website address)
deny tcp any host x.x.x.x eq www
deny tcp any host x.x.x.x eq 443
deny tcp any host x.x.x.x eq 8443
permit ip any any (redirect all other traffic)
!
radius server NAC
address ipv4 10.10.10.10 auth-port 1812 acct-port 1813
key XXXXX
!
radius-server vsa send authentication
!
end
> **Note:** The port configuration above attempts 802.1X first and falls back to MAB. On a port that serves only non-802.1X devices (printers, IP phones, IoT endpoints, etc.), the switch will wait for 802.1X to time out — `dot1x timeout tx-period` × (`dot1x max-reauth-req` + 1) seconds — before MAB authenticates the device. To avoid that delay on such ports, either:
>
> - remove the `dot1x pae authenticator` and `dot1x ...` lines so the port uses MAB only, or
> - reverse the order so MAB is attempted first: `authentication order mab dot1x` / `authentication priority mab dot1x`.

## [Additional ACL exceptions (if required)](/docs/manac/installation/cisco-wired-layer-2-integration#additional-acl-exceptions-if-required)

Examples of other types of ACL exceptions that can be added to `sc_quarantine_acl`:

BashCopyremark allow PXE boot
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
