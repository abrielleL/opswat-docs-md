<!-- source: https://www.opswat.com/docs/manac/installation/aruba-wireless-arubaos-8 -->

# Aruba Wireless Controller ArubaOS 8

#### [Summary](/docs/manac/installation/aruba-wireless-arubaos-8#summary)

**This document provides scripts to complete the integration of NAC with one more ArubaOS8 Mobility Controllers for Radius Based Enforcement.**

**Note** – A PEF (Policy Enforcement Firewall) license is required on each controller for this integration.

**Note** – Even when using a Mobility Master node to manage Mobility Controllers at many locations, the tunnel configuration must be applied directly on any Mobility Controller which you wish to integrate with the NAC (i.e. at the /mm/mynode level). The rest of the configuration can be applied at either the Mobility Controller level or the Mobility Master level. You can use `show configuration node-heirarchy` to see the configuration on the Mobility Master.

BashCopyshow configuration node-hierarchy
#### [NAC ArubaOS 8 Integration Script – Mobility Controller](/docs/manac/installation/aruba-wireless-arubaos-8#nac-arubaos-8-integration-script--mobility-controller)

BashCopyconf t
interface tunnel 58008
description "NAC Interface tunnel02"
ip address x.x.x.x 255.255.255.252 (Replace x.x.x.x with an available private IP, other host will be used by NAC server)
tunnel source x.x.x.x (Replace x.x.x.x with IP of controller and remove this comment)
tunnel destination <NAC-IP>
trusted
!
end
!
write memory

**Note** - Do not apply tunnel keep-alives as they are not compatible with third party vendors such as NAC.

**Note** - After completing the configuration above, please email a sanitized `show run` and `show switches` to your OPSWAT Network Specialist so they can complete the tunnel configuration on the NAC side.

#### [NAC ArubaOS 8 Integration Script – Mobility Master or Mobility Controller](/docs/manac/installation/aruba-wireless-arubaos-8#nac-arubaos-8-integration-script--mobility-master-or-mobility-controller)

BashCopyconf t
netservice svc-sc_https tcp 8443
netservice svc-sc_https2 tcp 9443
netservice svc-sc_http tcp 8008
!
netdestination apple-cna
name www.apple.com
name www.airport.us
name www.ibook.info
name www.thinkdifferent.us
name www.appleiphonecell.com
name www.itools.info
!
ip access-list session sc_compliant_acl
any any any permit
!
ip access-list session sc_guest_acl
any network x.x.x.x any deny (Add any network denied to guest users and remove this comment)
any any any permit
!
ip access-list session sc_redirect_acl
any host 198.31.193.211 any redirect tunnel 58008
any host <NAC-IP> any redirect tunnel 58008
!
ip access-list session sc_intranet_acl
any host x.x.x.x any permit (Add any internal resource allowed to all users while blocked and remove this comment)
!
ip access-list session sc_quarantine_acl
user alias apple-cna svc-http permit position 1 (Note – this command will disable captive portal detection. If the desire is to keep native captive portal detection enabled, skip this command)
any any svc-http redirect tunnel 58008
any any svc-https redirect tunnel 58008
any any svc-sc_https redirect tunnel 58008
any any svc-sc_https2 redirect tunnel 58008
any any svc-sc_http redirect tunnel 58008
any any svc-dns permit
any any svc-dhcp permit
any any svc-kerberos redirect tunnel 58008
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
####

#### [NAC / ArubaOS 8 - Open Wireless Example](/docs/manac/installation/aruba-wireless-arubaos-8#nac--arubaos-8---open-wireless-example)

BashCopyconf t
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
#### [NAC / ArubaOS 8 - Secure Wireless Example (802.1x)](/docs/manac/installation/aruba-wireless-arubaos-8#nac--arubaos-8---secure-wireless-example-8021x)

BashCopyconf t
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

**Note** - These steps may be needed if iOS users constantly get disconnected from Aruba SSIDs: Adjust the Global User idle timeout from 30 seconds to 300 seconds:

BashCopyconf t
aaa timers idle-timeout 300 seconds
!
end
!
write memory
