<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/brocade-ruckus-arris-wired-layer-2-integration -->

# Brocade-Ruckus-Arris Wired Layer 2 Integration

Note – In this example, a Brocade/Ruckus/Arris ICX 7450 configuration is provided. However, any ICX Layer 2 switch supporting the following features are eligible for integration. Impulse recommends version 8.0.30 or later.

- RADIUS Authentication/Accounting
- 802.1X / MAC Authentication
- RADIUS Change of Authorization (CoA)
- Dynamic VLAN Assignment

Note – In this example the NAC RADIUS Server / Policy Server is 10.10.10.10 (replace this IP with the IP of your NAC system). Also replace the auth-default-vlan and test port numbers with desired values.

BashCopyconf t
!
authentication
auth-default-vlan 20
disable-aging permitted-mac-only (for version 08.0.90 or later)
dot1x enable (disregard unless endpoint supplicants are used)
dot1x enable ethe 1/1/23 (disregard unless endpoint supplicants are used)
mac-authentication enable
mac-authentication enable ethe 1/1/47
auth-order mac-auth dot1x
!
aaa authentication dot1x default radius
aaa accounting dot1x default start-stop radius
aaa accounting mac-auth default start-stop radius (for version 08.0.70 or later)
aaa authorization coa enable
radius-client coa host 10.10.10.10 key xxxxx
radius-server host 10.10.10.10 auth-port 1812 acct-port 1813 default key xxxxx
radius-server host 10.10.10.10 auth-port 1812 acct-port 1813 default key xxxxx
dot1x mac-auth no-login (use this line instead of previous line if RADIUS is presently used for switch login access)
radius-server accounting interim-updates (for version 08.0.70 or later)
radius-server accounting interim-interval 5 (for version 08.0.70 or later)
ip radius source-interface ve X (Layer 3 management interface)
ip access-list extended 100 (for 7xxx series only)
sequence 10 permit ip any any (for 7xxx series only)
!
interface ethernet 1/1/47
dot1x port-control auto
mac-authentication enable-dynamic-vlan
authentication max-sessions 32
authentication auth-vlan-mode multiple-untagged (for hubs/unmanaged switches)
authentication reauth-timeout 60 (for printers)
port-name NAC Test Port
authentication auth-mode multiple untagged
dhcp snooping client-learning disable (for 7xxx series only)
dhcp snooping trust (for 7xxx series only)
!
end

Note – For VOIP environments ensure LLDP is enabled, LLDP pass-through is enabled under authentication and no voice VLAN is configured on the test port.

BashCopyconf t
!
no cdp run (disregard this if you have Cisco phones)
lldp med network-policy application voice tagged vlan 200 priority 4 dscp 46
ports ethe x/x/x
lldp run
!
authentication
pass-through lldp
!
interface ethernet x/x/x
authentication voice-vlan
!
end

Note – For VOIP environments, the NAC RADIUS server must be configured to return the following RADIUS attributes. This will ensure the voice vlan is returned and also ensure the phone does not attempt 802.1X authentication as mac authentication will have already occurred.

BashCopyTunnel-Type:0 += VLAN
Tunnel-Medium-Type:0 += IEEE-802
Tunnel-Private-Group-Id:0 += "T:x"(replace x with voice VLAN number)
Foundry-MAC-Authent-needs-802.1x = 0
Foundry-802_1x-enable = 0 (use this line instead of previous line if switch is
running 08.0.30 or later)
