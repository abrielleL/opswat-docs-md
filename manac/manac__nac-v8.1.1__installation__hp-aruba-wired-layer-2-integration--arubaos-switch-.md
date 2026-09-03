<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/hp-aruba-wired-layer-2-integration--arubaos-switch- -->

# HP-Aruba Wired Layer 2 Integration (ArubaOS-Switch)

Note – In this example, an HP Aruba 2930F configuration is provided as tested on WC.16.10.0002, however any arubaOS-Switch Layer 2 switch supporting the following features are eligible for integration. This integration is not intended for HPE switches running non-ArubaOS-Switch or ArubaOS software (K or Y software versions).

Note – In this example the NAC RADIUS Server / Policy Server is x.x.x.x (replace this IP with the IP of your NAC system)

Note – Be sure to remove comments in (BOLD) before cutting and pasting script into the switch

BashCopyconfigure
!
class ipv4 "DNS"
10 match udp 0.0.0.0 255.255.255.255 0.0.0.0 255.255.255.255 eq 53
exit
!
class ipv4 "DHCP"
10 match udp 0.0.0.0 255.255.255.255 0.0.0.0 255.255.255.255 eq 67
exit
!
class ipv4 "INTERNAL"
10 match ip 0.0.0.0 255.255.255.255 192.168.0.0 0.0.255.255 (any
network denied to guest users - optional)
exit
!
class ipv4 "IP-ANY-ANY"
10 match ip 0.0.0.0 255.255.255.255 0.0.0.0 255.255.255.255
exit
!
class ipv4 "WEB-TRAFFIC"
10 match tcp 0.0.0.0 255.255.255.255 0.0.0.0 255.255.255.255 eq 80
20 match tcp 0.0.0.0 255.255.255.255 0.0.0.0 255.255.255.255 eq 443
exit
!
class ipv4 "SC-APPLIANCE"
10 match tcp 0.0.0.0 255.255.255.255 198.31.193.211 0.0.0.0 eq 80
20 match tcp 0.0.0.0 255.255.255.255 198.31.193.211 0.0.0.0 eq 443
30 match tcp 0.0.0.0 255.255.255.255 198.31.193.211 0.0.0.0 eq 8443
40 match tcp 0.0.0.0 255.255.255.255 x.x.x.x 0.0.0.0 eq 80
50 match tcp 0.0.0.0 255.255.255.255 x.x.x.x 0.0.0.0 eq 443
60 match tcp 0.0.0.0 255.255.255.255 x.x.x.x 0.0.0.0 eq 8443
exit
!
policy user "SC_COMPLIANT_POLICY"
10 class ipv4 "IP-ANY-ANY" action permit
exit
!
policy user "SC_GUEST_POLICY"
10 class ipv4 "DNS" action permit
20 class ipv4 "DHCP" action permit
30 class ipv4 "INTERNAL" action deny
40 class ipv4 "IP-ANY-ANY" action permit
exit
!
policy user "SC_INITIAL_POLICY"
10 class ipv4 "IP-ANY-ANY" action permit
exit
!
policy user "SC_QUARANTINE_POLICY"
10 class ipv4 "DNS" action permit
20 class ipv4 "DHCP" action permit
30 class ipv4 "SC-APPLIANCE" action permit
40 class ipv4 "WEB-TRAFFIC" action redirect captive-portal
exit
!
dhcp-snooping
dhcp-snooping authorized-server y.y.y.y (replace with ip address of dhcp server)
dhcp-snooping database delay 15
no dhcp-snooping option 82
dhcp-snooping vlan x (client VLAN(s))
dhcp-snooping allow-overwrite-binding
radius-server host x.x.x.x key "your-secret-here"
radius-server host x.x.x.x dyn-authorization
radius-server host x.x.x.x time-window 0
!
interface x (uplink interface)
dhcp-snooping trust
exit
!
aaa server-group radius "NAC" host x.x.x.x
aaa accounting update periodic 5
aaa accounting network start-stop radius
Note – VLANs for all roles can be the same (as was done when testing) or whichever VLAN you prefer for the role.
aaa authorization user-role name "SC_GUEST_ROLE"
policy "SC_GUEST_POLICY"
vlan-id x (VLAN # guest clients should be placed in)
exit
aaa authorization user-role name "SC_INITIAL_ROLE"
policy "SC_INITIAL_POLICY"
vlan-id x (VLAN # clients have when initially connecting)
exit
aaa authorization user-role name "SC_COMPLIANT_ROLE"
policy "SC_COMPLIANT_POLICY"
vlan-id x (VLAN # compliant clients should be placed in)
exit
aaa authorization user-role name "SC_QUARANTINE_ROLE"
captive-portal-profile "use-radius-vsa"
policy "SC_QUARANTINE_POLICY"
vlan-id x (VLAN # blocked clients should be placed in)
exit
aaa authorization user-role enable
aaa authentication port-access eap-radius
aaa authentication captive-portal enable
aaa port-access gvrp-vlans
aaa port-access authenticator x-x (can be a single port or range)
aaa port-access authenticator x-x tx-period 10
aaa port-access authenticator x-x supplicant-timeout 10
aaa port-access authenticator x-x client-limit 1
aaa port-access authenticator x-x cached-reauth-period 30
aaa port-access authenticator eap-id-compliance
aaa port-access authenticator active
aaa port-access supplicant x-x
aaa port-access mac-based x-x
aaa port-access mac-based x-x addr-limit 250
aaa port-access mac-based x-x cached-reauth-period 1
aaa port-access x-x auth-order authenticator mac-based

This completes the ArubaOS-Switch device configuration for NAC integration.

Note – The switch must now be added to the NAC RADIUS server. Refer to the NAC RADIUS Server Configuration guide for details on how to add the switch as a NAS.

Note – Unless 802.1X is required, be sure to select the MAC Authentication Only mode when configuring the NAC RADIUS server

PowershellCopyTroubleshooting Comnand:
Show port-access clients 3 detailed
debug destination session
debug event
