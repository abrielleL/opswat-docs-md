<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/cisco-catalyst-c9200-c9300-integration -->

# Cisco Catalyst C9200 IOS XE integration

NAC Cisco Layer 2 Switch Configuration Example:

Note – In this example, a Cisco Catalyst C9200 IOS XE configuration is provided. Cisco Catalyst 9200 running IOS XE 17.6.1 or later are supported for centrally switched traffic. However, any Cisco C9K switch supporting the following features are eligible for integration:

- RADIUS Authentication/Accounting
- 802.1X
- MAC Authentication Bypass (MAB)
- RADIUS Change of Authorization (CoA)
- Cisco-AVPair “url-redirect”
- Cisco-AVPair “url-redirect-acl”

Note – In this example the NAC RADIUS Server / Policy Server is 10.10.10.10 (replace this IP with the IP of your NAC system)

Note – Replace the VLAN number on the example port configuration with the desired default VLAN for the port.

VbnetCopyaaa new-model
aaa session-id common
aaa authentication dot1x default group NAC_grp
aaa authorization network default group NAC_grp
aaa accounting Identity default start-stop group NAC_grp
aaa accounting delay-start group NAC_grp
aaa accounting update newinfo periodic 2880
!
!
!
!
aaa server radius dynamic-author
client 10.10.10.10 server-key HelloEnforcer
port 3799
!
dot1x system-auth-control
radius-server vsa send authentication
radius-server vsa send accounting
!
radius server NAC
address ipv4 10.10.10.10 auth-port 1812 acct-port 1813
automate-tester username Test3 ignore-auth-port ignore-acct-port probe-on
key HelloEnforcer
!
!
aaa group server radius NAC_grp
server name NAC
ip radius source-interface Vlan1
!
!
ip radius source-interface Vlan1
ip http server
ip http secure-server
device-sensor filter-list dhcp list DHCP-LIST
option name host-name
option name requested-address
option name parameter-request-list
option name class-identifier
option name client-identifier
!
device-sensor filter-list lldp list LLDP-LIST
tlv name system-name
tlv name system-description
tlv name system-capabilities
!
device-sensor filter-list cdp list CDP-LIST
tlv name device-name
tlv name address-type
tlv name capabilities-type
tlv name version-type
tlv name platform-type
!
device-sensor filter-spec dhcp include list DHCP-LIST
device-sensor filter-spec lldp include list LLDP-LIST
device-sensor filter-spec cdp include list CDP-LIST
!
device-sensor notify all-changes
!
device-tracking policy IP-Tracking
no protocol udp
tracking enable
!
ip access-list extended sc_compliant_acl
10 permit ip any any
ip access-list extended sc_initial_acl
10 permit ip any any
ip access-list extended sc_quarantine_acl
10 deny ip any host 198.31.193.211
20 deny ip host 198.31.193.211 any
30 deny ip any host 10.10.10.10
40 deny ip host 10.10.10.10 any
50 deny udp any any eq domain
60 deny udp any eq domain any
70 deny udp any any eq bootps
80 deny udp any eq bootps any
90 permit tcp any any eq www
#### [IBNS 2.0 Policy and Interface Configuration](/docs/manac/nac-v8.1.1/installation/cisco-catalyst-c9200-c9300-integration#ibns-20-policy-and-interface-configuration)

Service Template:

VbnetCopyservice-template DEFAULT_LINKSEC_POLICY_MUST_SECURE
service-template DEFAULT_LINKSEC_POLICY_SHOULD_SECURE
service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
voice vlan
service-template CRITICAL_AUTH_VLAN
service-template CRITICAL-ACCESS
description *Fallback Policy on AAA Fail*
access-group ACL-CRITICAL-V4
!

Class map:

VbnetCopyclass-map type control subscriber match-any IN_CRITICAL_AUTH
match activated-service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
match activated-service-template CRITICAL_AUTH_VLAN
match activated-service-template CRITICAL-ACCESS
!
class-map type control subscriber match-none NOT_IN_CRITICAL_AUTH
match activated-service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
match activated-service-template CRITICAL_AUTH_VLAN
match activated-service-template CRITICAL-ACCESS
!
class-map type control subscriber match-all AAA_SVR_DOWN_UNAUTHD_HOST
match result-type aaa-timeout
match authorization-status unauthorized
!
class-map type control subscriber match-all AAA_SVR_DOWN_AUTHD_HOST
match result-type aaa-timeout
match authorization-status authorized
!
class-map type control subscriber match-all DOT1X_NO_RESP
match method dot1x
match result-type method dot1x agent-not-found
!
class-map type control subscriber match-all MAB_FAILED
match method mab
match result-type method mab authoritative
!
class-map type control subscriber match-all DOT1X_FAILED
match method dot1x
match result-type method dot1x authoritative

Policy map:

On the 3 following configurations if the RADIUS server is down then we will apply CRITICAL_AUTH_VLAN, DEFAULT_CRITICAL_VOICE_TEMPLATE and CRITICAL-ACCESS service template. If the RADIUS server goes up then it reinitializes the authentication if the port is in IN_CRITICAL_VLAN.

for 802.1X with MAC Authentication fallback:

VbnetCopypolicy-map type control subscriber DOT1X_MAB
event session-started match-all
10 class always do-until-failure
10 authenticate using dot1x priority 10
event authentication-failure match-first
5 class DOT1X_FAILED do-until-failure
10 terminate dot1x
20 authenticate using mab priority 20
10 class AAA_SVR_DOWN_UNAUTHD_HOST do-until-failure
10 activate service-template CRITICAL_AUTH_VLAN
20 activate service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
30 activate service-template CRITICAL-ACCESS
40 authorize
50 pause reauthentication
20 class AAA_SVR_DOWN_AUTHD_HOST do-until-failure
10 activate service-template CRITICAL_AUTH_VLAN
20 activate service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
30 activate service-template CRITICAL-ACCESS
40 pause reauthentication
50 authorize
30 class DOT1X_NO_RESP do-until-failure
10 terminate dot1x
20 authenticate using mab priority 20
40 class MAB_FAILED do-until-failure
10 terminate mab
20 authentication-restart 10800
60 class always do-until-failure
10 terminate dot1x
20 terminate mab
30 authentication-restart 10800
event agent-found match-all
10 class always do-until-failure
10 terminate mab
20 authenticate using dot1x priority 10
event aaa-available match-all
10 class IN_CRITICAL_AUTH do-until-failure
10 clear-session
20 class NOT_IN_CRITICAL_AUTH do-until-failure
10 resume reauthentication
event inactivity-timeout match-all
10 class always do-until-failure
10 clear-session
event authentication-success match-all
10 class always do-until-failure
10 activate service-template DEFAULT_LINKSEC_POLICY_SHOULD_SECURE
event violation match-all
10 class always do-all
10 replace

for MAC Authentication only:

VbnetCopypolicy-map type control subscriber MACAUTH
event session-started match-all
10 class always do-until-failure
10 authenticate using mab priority 10
event authentication-failure match-first
10 class AAA_SVR_DOWN_UNAUTHD_HOST do-until-failure
10 activate service-template CRITICAL_AUTH_VLAN
20 activate service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
30 activate service-template CRITICAL-ACCESS
40 authorize
50 pause reauthentication
20 class AAA_SVR_DOWN_AUTHD_HOST do-until-failure
10 activate service-template CRITICAL_AUTH_VLAN
20 activate service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
30 activate service-template CRITICAL-ACCESS
40 pause reauthentication
50 authorize
30 class always do-until-failure
10 terminate mab
20 authentication-restart 30
event aaa-available match-all
10 class IN_CRITICAL_AUTH do-until-failure
10 clear-session
20 class NOT_IN_CRITICAL_AUTH do-until-failure
10 resume reauthentication
event inactivity-timeout match-all
10 class always do-until-failure
10 clear-session
event authentication-success match-all
10 class always do-until-failure
10 activate service-template DEFAULT_LINKSEC_POLICY_SHOULD_SECURE

for 802.1X only:

VbnetCopypolicy-map type control subscriber DOT1X
event session-started match-all
10 class always do-until-failure
10 authenticate using dot1x priority 10
event authentication-failure match-first
10 class AAA_SVR_DOWN_UNAUTHD_HOST do-until-failure
10 activate service-template CRITICAL_AUTH_VLAN
20 activate service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
30 activate service-template CRITICAL-ACCESS
40 authorize
50 pause reauthentication
20 class AAA_SVR_DOWN_AUTHD_HOST do-until-failure
10 activate service-template CRITICAL_AUTH_VLAN
20 activate service-template DEFAULT_CRITICAL_VOICE_TEMPLATE
30 activate service-template CRITICAL-ACCESS
40 pause reauthentication
50 authorize
30 class DOT1X_FAILED do-until-failure
10 terminate dot1x
40 class DOT1X_NO_RESP do-until-failure
10 terminate dot1x
60 class always do-until-failure
10 terminate dot1x
20 authentication-restart 10800
event agent-found match-all
10 class always do-until-failure
10 authenticate using dot1x priority 10
event aaa-available match-all
10 class IN_CRITICAL_AUTH do-until-failure
10 clear-session
20 class NOT_IN_CRITICAL_AUTH do-until-failure
10 resume reauthentication
event inactivity-timeout match-all
10 class always do-until-failure
10 clear-session
event authentication-success match-all
10 class always do-until-failure
10 activate service-template DEFAULT_LINKSEC_POLICY_SHOULD_SECURE

Interface Template (802.1X MAC Authentication):

VbnetCopytemplate identity-template-mab
dot1x pae authenticator
spanning-tree portfast
switchport access vlan 1
switchport mode access
switchport voice vlan 100
mab
access-session host-mode multi-domain
access-session control-direction in
access-session closed
access-session port-control auto
authentication periodic
authentication timer reauthenticate server
service-policy type control subscriber DOT1X_MAB

Interface Template (MAC Authentication):

VbnetCopytemplate identity-template-macauth
dot1x pae authenticator
spanning-tree portfast
switchport access vlan 1
switchport mode access
switchport voice vlan 100
mab
access-session host-mode multi-auth
access-session control-direction in
access-session closed
access-session port-control auto
authentication periodic
authentication timer reauthenticate server
service-policy type control subscriber MACAUTH

Interface Template (802.1X):

VbnetCopytemplate identity-template-dot1x
dot1x pae authenticator
spanning-tree portfast
switchport access vlan 1
switchport mode access
switchport voice vlan 100
mab
access-session host-mode multi-auth
access-session control-direction in
access-session closed
access-session port-control auto
authentication periodic
authentication timer reauthenticate server
service-policy type control subscriber DOT1X

Apply the new policy-map to the Test interface

VbnetCopyinterface gigabitEthernet 1/0/1
device-tracking attach-policy IP-Tracking
source template identity-template-mab
eapol announcement

Troubleshooting command:

When you use Port Templates, use the command **"show derived-config"** to see the actual (total) configuration on an interface after the Template has been applied to it.

VbnetCopyshow derived-config interface gigabitEthernet 1/0/1
switchport mode access
switchport voice vlan 100
device-tracking attach-policy NAC
authentication periodic
authentication timer reauthenticate server
access-session host-mode multi-domain
access-session control-direction in
access-session closed
access-session port-control auto
mab
eapol announcement
dot1x pae authenticator
dot1x timeout tx-period 5
spanning-tree portfast
service-policy type control subscriber DOT1X_MAB
endVbnetCopyshow authentication sessions interface gigabitEthernet 1/0/1 detail
show tech-support identity
