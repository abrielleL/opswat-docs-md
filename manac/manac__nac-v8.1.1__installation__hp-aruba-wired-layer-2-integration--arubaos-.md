<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/hp-aruba-wired-layer-2-integration--arubaos- -->

# HP-Aruba Wired Layer 2 Integration (ArubaOS)

Note – In this example, an Aruba S2500 configuration is provided as tested on ArubaOS 7.4.1.7, however any ArubaOS Layer 2 switch supporting the following features are eligible for integration. This integration is not intended for HPE switches running non-ArubaOS software (K or Y software versions).

Note – If your ArubaOS switch is running in Tunneled Node mode, all traffic from the switch ports is tunneled directly to the controller. NAC would integrate directly with the controller in that scenario instead of the switch.

Note – In this example the NAC RADIUS Server / Policy Server is 10.10.10.10 (replace this IP with the IP of your NAC system)

Note – Be sure to remove comments in (BOLD) before cutting and pasting script into the switch

BashCopyconf t
!
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
any network x.x.x.x x.x.x.x any deny (any network denied to guest users - optional)
!
ip access-list session sc_intranet_acl
any host x.x.x.x any permit (any internal resource allowed to quarantined users - optional)
!
ip access-list session sc_redirect_acl
any host 198.31.193.211 any redirect tunnel 1
!
ip access-list session sc_quarantine_acl
user alias apple-cna svc-http permit position 1 (will prevent apple CNA browser from launching – if Apple CNA is desired, remove this line)
any any svc-http redirect tunnel 1
any any svc-https redirect tunnel 1
any any svc-sc_https redirect tunnel 1
any any svc-sc_https2 redirect tunnel 1
any any svc-sc_http redirect tunnel 1
any any svc-dns permit
any any svc-dhcp permit
any any svc-kerberos redirect tunnel 1
any any any deny
!
user-role SC_Initial_Role
session-acl sc_redirect_acl
session-acl sc_compliant_acl
!
user-role SC_Compliant_Role
session-acl sc_redirect_acl
session-acl sc_compliant_acl
!
user-role SC_Guest_Role
session-acl sc_redirect_acl
session-acl sc_guest_acl
!
user-role SC_Quarantine_Role
session-acl sc_redirect_acl
session-acl sc_intranet_acl
session-acl sc_quarantine_acl
!
interface tunnel ip "1"
description "NAC Interface tunnel01"
ip address 192.168.100.1 255.255.255.252
source-ip x.x.x.x (replace with the IP of the switch)
destination-ip 10.10.10.10
!
aaa rfc-3576-server "10.10.10.10"
key ArUb@-SC-RB3
!
aaa authentication-server radius "NAC_RBE"
host "10.10.10.10"
key ArUb@-SC-RB3
!
aaa authentication-server radius "NAC_Acct"
host "10.10.10.10"
key ArUb@-SC-RB3
!
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
aaa profile "NAC-Wired"
initial-role "SC_Initial_Role"
authentication-mac "SC_Open_RBE_Mac_Auth"
mac-default-role "SC_Initial_Role"
mac-server-group "NAC_RBE_svrgrp"
authentication-dot1x "NAC-dot1x_prof" (only required if end users devices will have supplicants configured – if not remove line)
dot1x-default-role "SC_Initial_Role" (only required if end users devices will have supplicants configured – if not remove line)
dot1x-server-group "NAC_RBE_svrgrp" (only required if end users devices will have supplicants configured – if not remove line)
radius-accounting "NAC_Acct_svrgrp"
radius-interim-accounting
rfc-3576-server "10.10.10.10"
!
interface gigabitethernet “x/x/x" (replace with test port)
aaa-profile "NAC-Wired"
no trusted port
!
write memory
!
end

This completes the ArubaOS switch configuration for NAC integration.

Note – The switch must now be added to the NAC RADIUS server. Refer to the NAC RADIUS Server Configuration guide for details on how to add the switch as a NAS.

Note – Unless 802.1X is required, be sure to select the MAC Authentication Only mode when configuring the NAC RADIUS server.
