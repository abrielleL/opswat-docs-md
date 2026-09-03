<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/alcatel-omniswitch-2-switch-integration-script -->

# Alcatel OmniSwitch 2 Switch Integration Script

Note: This integration was certified on an OS6465-P28 running 8.6.289.R01 and an OS6865-P16X running 8.6.289.R01. Replace x.x.x.x with the NAC appliance IP and replace “your-shared-secret-here” with the shared secret you would like to use, this will also need to be added in the NAC RADIUS UI.

BashCopyunp profile "SC_Guest_Profile" qos-policy-list "SC_Guest_List"
unp profile "SC_Initial_Profile"
unp profile "SC_Compliant_Profile"
unp profile "SC_Quarantine_Profile" qos-policy-list "SC_Quarantine_List"
unp profile "SC_Guest_Profile" map vlan 18
unp profile "SC_Initial_Profile" map vlan 18
unp profile "SC_Compliant_Profile" map vlan 18
unp profile "SC_Quarantine_Profile" map vlan 18
unp redirect pause-timer 60
unp redirect server 10.101.150.10
unp port 1/1/1 port-type bridge
unp port 1/1/1 redirect-port-bounce direction both default-profile "SC_Initial_Profile"
classification trust-tag ap-mode dynamic-service none
unp port 1/1/1 admin-state enable
unp port 1/1/1 802.1x-authentication
unp port 1/1/1 mac-authentication
!
aaa radius-server "NAC" host x.x.x.x hash-key your-shared-secret-here retransmit 3
timeout 2 auth-port 1812 acct-port 1813 vrf-name default
!
aaa device-authentication mac "NAC"
aaa device-authentication 802.1x "NAC"
aaa accounting mac "NAC"
aaa accounting 802.1x "NAC"
!
policy service svc-dhcp destination udp-port 67
policy service svc-dns destination udp-port 53
policy service group protocolallow svc-dns svc-dhcp
policy network group NAC x.x.x.x 198.31.193.211
policy network group internal 10.0.0.0 mask 255.0.0.0 172.16.0.0 mask 255.240.0.0
192.168.0.0 mask 255.255.0.0
policy condition to-protocolallow service group protocolallow
policy condition to-internal destination network group internal
policy condition to-NAC destination network group NAC
policy action ACCEPT
policy action DENY disposition deny
policy rule Allow-NAC precedence 1002 condition to-NAC action ACCEPT no
default-list
policy rule Allow-Services precedence 1002 condition to-protocolallow action ACCEPT no
default-list
policy rule Deny-Internal precedence 1000 condition to-internal action DENY no default-list
policy list SC_Quarantine_List type unp
policy list SC_Quarantine_List rules Deny-Internal Allow-NAC Allow-Services
policy list SC_Guest_List type unp
policy list SC_Guest_List rules Deny-Internal Allow-Services
qos apply
!
!
mvrp enable
!
wr mem flash-synchro
