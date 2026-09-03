<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/-arubaos-8--aruba-wireless-controller-without-gre-tunnels -->

# (ArubaOS 8) Aruba Wireless Controller without GRE tunnels

#### [Summary](/docs/manac/nac-v8.1.1/installation/-arubaos-8--aruba-wireless-controller-without-gre-tunnels#summary)

**This document provides scripts to complete the integration of NAC with one more ArubaOS8 Mobility Controllers for Radius Based Enforcement.**

**Note** – A PEF (Policy Enforcement Firewall) license is required on each controller for this integration.

#### [NAC ArubaOS 8 Integration Script – Mobility Master or Mobility Controller](/docs/manac/nac-v8.1.1/installation/-arubaos-8--aruba-wireless-controller-without-gre-tunnels#nac-arubaos-8-integration-script--mobility-master-or-mobility-controller)

XmlCopyconf t
netservice svc-sc_https tcp 8443
netservice svc-sc_https2 tcp 9443
!
netdestination apple-cna
name captive.apple.com
!
ip access-list session sc_compliant_acl
any any any permit
!
ip access-list session sc_guest_acl
any network x.x.x.x any deny (Add any network denied to guest users and remove this comment)
any any any permit
!
ip access-list session sc_redirect_acl
any host 198.31.193.211 any dst-nat ip <NAC-IP>
!
ip access-list session sc_intranet_acl
any host x.x.x.x any permit (Add any internal resource allowed to all users while blocked and remove this comment)
!
ip access-list session sc_quarantine_acl
user alias apple-cna svc-http permit position 1 (Note – This command will disable captive portal detection for the Captive Network Assistant [CNA] utility in Apple devices. This can be useful if you prefer users to interact with NAC pages in a full-featured browser, or if CNA is causing other problems for your users. If you desire to keep Apple's native CNA functionality intact, omit this line.)
any any svc-http dst-nat ip <NAC-IP>
any any svc-https dst-nat ip <NAC-IP>
any any svc-sc_https dst-nat ip <NAC-IP>
any any svc-sc_https2 dst-nat ip <NAC-IP>
any any svc-dns permit
any any svc-dhcp permit
any any svc-kerberos dst-nat ip <NAC-IP>
any any any deny
!
user-role SC_Compliant_Role
access-list session sc_redirect_acl
access-list session sc_compliant_acl
!
user-role SC_Guest_Role
access-list session sc_redirect_acl
access-list session sc_guest_acl
!
user-role SC_Quarantine_Role
access-list session sc_redirect_acl
access-list session sc_intranet_acl
access-list session sc_quarantine_acl
!
user-role SC_Initial_Role
access-list session sc_redirect_acl
access-list session sc_compliant_acl
!
aaa rfc-3576-server <NAC-IP>
key ArUb@-SC-RB3
!
aaa authentication-server radius "NAC_RBE"
host <NAC-IP>
key ArUb@-SC-RB3
!
aaa authentication-server radius "NAC_Acct"
host <NAC-IP>
key ArUb@-SC-RB3
!
aaa authentication dot1x "NAC-dot1x_prof"
!
end
!
write memory
#### [NAC / ArubaOS 8 - Open Wireless Example](/docs/manac/nac-v8.1.1/installation/-arubaos-8--aruba-wireless-controller-without-gre-tunnels#nac--arubaos-8---open-wireless-example)

XmlCopyconf t
aaa server-group "NAC_RBE_svrgrp"
auth-server "NAC_RBE" position 1
!
aaa server-group "NAC_Acct_svrgrp"
auth-server "NAC_Acct" position 1
!
aaa authentication mac "SC_Open_RBE_Mac_Auth"
delimiter none
case upper
!
aaa profile "NAC-Open_SSID"
initial-role "SC_Initial_Role"
authentication-mac "SC_Open_RBE_Mac_Auth"
mac-default-role "SC_Initial_Role"
mac-server-group "NAC_RBE_svrgrp"
dot1x-default-role "SC_Initial_Role"
radius-accounting "NAC_Acct_svrgrp"
radius-interim-accounting
rfc-3576-server <NAC-IP>
!
wlan ht-ssid-profile "NAC-Open-htssid_prof"
!
wlan ssid-profile "NAC-Open-ssid_prof"
essid "NAC-Open"
ht-ssid-profile "NAC-Open-htssid_prof"
!
wlan virtual-ap "NAC-Open-vap_prof"
aaa-profile "NAC-Open_SSID"
ssid-profile "NAC-Open-ssid_prof"
vlan <VLAN-ID>
!
ap-group "NAC"
virtual-ap "NAC-Open-vap_prof"
!
end
!
write memory
#### [NAC / ArubaOS 8 - Secure Wireless Example (802.1x)](/docs/manac/nac-v8.1.1/installation/-arubaos-8--aruba-wireless-controller-without-gre-tunnels#nac--arubaos-8---secure-wireless-example-8021x)

XmlCopyconf t
aaa server-group "NAC_RBE_svrgrp"
auth-server "NAC_RBE" position 1
!
aaa server-group "NAC_Acct_svrgrp"
auth-server "NAC_Acct" position 1
!
aaa profile "NAC_Secure_SSID"
initial-role "SC_Initial_Role"
dot1x-default-role "SC_Initial_Role"
authentication-dot1x "NAC-dot1x_prof"
dot1x-server-group "NAC_RBE_svrgrp"
radius-accounting "NAC_Acct_svrgrp"
radius-interim-accounting
rfc-3576-server <NAC-IP>
!
wlan ht-ssid-profile "NAC_Secure-htssid_prof"
!
wlan ssid-profile "NAC_Secure-ssid_prof"
essid "NAC_Secure"
ht-ssid-profile "NAC_Secure-htssid_prof"
opmode wpa2-aes
!
wlan virtual-ap "NAC_Secure-vap_prof"
aaa-profile "NAC_Secure_SSID"
ssid-profile "NAC_Secure-ssid_prof"
vlan <VLAN-ID>
!
ap-group "NAC"
virtual-ap "NAC_Secure-vap_prof"
!
end
!
write memory

**Note:** These steps may be needed if iOS users constantly get disconnected from Aruba SSIDs: Adjust the Global User idle timeout from 30 seconds to 300 seconds

XmlCopyconf t
aaa timers idle-timeout 300 seconds
!
end
!
write memory
