<!-- source: https://www.opswat.com/docs/manac/installation/aruba-cx-os-switch-wired-layer-2-integration -->

# Aruba CX OS-Switch Wired Layer 2 Integration

Note – In this example, an HP Aruba CX 6300M configuration is provided as tested on 10.09.1000 firmware, however any Aruba CX OS-Switch supporting the following features are eligible for integration. This integration is not intended for HPE switches running non-ArubaOS-Switch or ArubaOS software (K or Y software versions).

NAC VM is <NAC-IP>

JavascriptCopyconfigure
!
aaa authentication port-access dot1x authenticator radius server-group NAC
aaa authentication port-access mac-auth radius server-group NAC
aaa authentication port-access dot1x authenticator enable
aaa authentication port-access mac-auth enable
aaa authentication port-access captive-portal-profile captive-portal
url https://portal.myweblogon.com
exit
!
radius-server host <NAC-IP> key plaintext "your-secret-here"
aaa group server radius NAC
server <NAC-IP>
exit
!
aaa accouting port-access start-stop interim
radius dyn-authorization enable
radius dyn-authorization client <NAC-IP> secret-key plaintext "HelloEnforcer"
class ip DNS
10 match udp any any eq 53
exit
!
class ip DHCP
10 match udp any any eq 67
20 match udp any any eq 68
exit
!
class ip INTERNAL
10 match ip any <AD-SERVER-IP>
20 match ip any <OTHER-INTERNAL-RESOURCE> (Add as many of these as you need)
exit
!
class ip IP-ANY-ANY
10 match ip any any
exit
!
class ip WEB-TRAFFIC
10 match tcp any any eq 80
20 match tcp any any eq 443
exit
!
class ip SC-APPLIANCE
10 match tcp any 198.31.193.211 eq 80
20 match tcp any 198.31.193.211 eq 443
30 match tcp any 198.31.193.211 eq 8443
40 match tcp any <NAC-IP> eq 80
50 match tcp any <NAC-IP> eq 443
60 match tcp any <NAC-IP> eq 8443
exit
!
port-access policy SC_COMPLIANT_POLICY
class ip IP-ANY-ANY
exit
!
port-access policy SC_GUEST_POLICY
class ip DNS
class ip DHCP
class ip INTERNAL action drop
class ip IP-ANY-ANY
exit
!
port-access policy SC_INITIAL_POLICY
class ip IP-ANY-ANY
exit
!
port-access policy SC_QUARANTINE_POLICY
class ip DNS
class ip DHCP
class ip INTERNAL
class ip SC-APPLIANCE
class ip WEB-TRAFFIC action redirect captive-portal
exit
!
port-access role SC_Guest_Role
vlan access xxx (VLAN # guest clients should be placed in)
associate policy SC_GUEST_POLICY
exit
!
port-access role SC_Initial_Role
vlan access xxx (VLAN # clients have when initially connecting)
associate policy SC_INITIAL_POLICY
exit
!
port-access role SC_Compliant_Role
vlan access xxx (VLAN # compliant clients should be placed in)
associate policy SC_COMPLIANT_POLICY
exit
!
port-access role SC_Quarantine_Role
vlan access xxx (VLAN # blocked clients should be placed in)
associate policy SC_QUARANTINE_POLICY
exit
!
dhcpv4-snooping
dhcpv4-snooping authorized-server 10.40.176.50 (replace with ip address of dhcp server)
---
no dhcpv4-snooping option 82
---
dhcpv4-snooping allow-overwrite-binding
---
---
interface x (uplink interface)
dhcpv4-snooping trust
exit
!
**********************************************************
interface 1/1/2 (can be a single port or range port)
aaa authentication port-access auth-precedence mac-auth dot1x
aaa authentication port-access client-limit 2
aaa authentication port-access dot1x authenticator enable
aaa authentication port-access mac-auth enable
************************************************************

Troubleshooting command

JavascriptCopyshow port-access client interface 1/1/2 detail
(Show detail overview of role port assignment)
show aaa authentication port-access interface 1/1/2 client-status
(Command on the switch will display the details of a session.)
show port-access role radius
(to see what VLAN is applied to what profile)
show radius dyn-authorization
(Command can be used to see if the COA was being acknowledge by the switch.)
