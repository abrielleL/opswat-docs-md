<!-- source: https://www.opswat.com/docs/manac/installation/ubiquiti-wireless-layer-2-integration -->

# Ubiquiti Wireless Layer 2 Integration

## [Summary](/docs/manac/installation/ubiquiti-wireless-layer-2-integration#summary)

This document provides scripts complete the installation of NAC RADIUS Based Enforcement.

NOTE – Ubiquiti CloudKey controller running 5.12.35 and a Unifi AP-AC-Pro running coa-debug.11173 code.

## [Controller Configuration](/docs/manac/installation/ubiquiti-wireless-layer-2-integration#controller-configuration)

NOTE – NAC must leverage VLAN assignment for the integration, therefore a quarantine VLAN will be needed.

Navigate to Settings > Configuration Profiles > RADIUS and click Create New RADIUS Profile.

Under GENERAL give the profile a name, select and Enable Wired and Enable Wireless. Under AUTHENTICATION SERVERS add the IP address of the NAC appliance for port 1812 and enter the shared secret (be sure to keep this handy as it will need to be entered on the NAC appliance side as well). Under ACCOUNTING select Enable Accounting, Enable Interim Update and set the Interim Update Interval to 300 (5 minutes). Finally, add the IP address of the NAC appliance under RADIUS Accounting Servers, set the port to 1813 and enter the same shared secret entered for the authentication server.

Click Apply.

Navigate to WI-FI > Wi-Fi Networks and select Create New Wi-Fi Network.

Click Create Advanced Wi-Fi.

## [Open (Guest) SSID Configuration](/docs/manac/installation/ubiquiti-wireless-layer-2-integration#open-guest-ssid-configuration)

Give the network (SSID) a name, ensure its enabled and expand Advanced Settings.

Under MISCELLANEOUS, select Combine Name/SSID and select Enable RADIUS DAS/DAC (CoA)

Under RADIUS MAC AUTHENTICATION select Enable RADIUS MAC Authentication, set the RADIUS profile to the one configured above for NAC , and ensure the MAC address format is set to lowercase with no delimiter as shown.

Click Done.

## [Secure SSID Configuration](/docs/manac/installation/ubiquiti-wireless-layer-2-integration#secure-ssid-configuration)

Give the network (SSID) a name, ensure its enabled, set Security Protocol to WPA Enterprise, WPA Mode to WPA2 only, enable CCMP encryption, set the Radius Profile to the one created for NAC and expand Advanced Settings.

Under MISCELLANEOUS, enable Refresh Shared Secret, select Combine Name/SSID and select Enable RADIUS DAS/DAC (CoA)

Click Done.

You should see the SSIDs broadcasting shortly thereafter. This concludes the Ubiquiti controller configuration.

L3 Upstream Redirect (PBR) Configuration

In order for traffic from the quarantine VLAN to be redirected to the NAC appliance, policy-based routing must be utilized on an upstream L3 switch or router. Below is an example for an Ubiquiti EdgeRouter.

PowershellCopyconfigure
!
set protocols static table x route 0.0.0.0/0 next-hop 10.100.18.84
(Replace x with the routing table used for the quarantine VLAN)
!
set firewall group network-group vlans network x.x.x.x/x
(Replace x.x.x.x/x with subnet used for the quarantine VLAN)
!
set firewall modify PBR rule 10 description SC_Quarantine_Vlan
!
set firewall modify PBR rule 10 source address x.x.x.x/x
(Replace x.x.x.x/x with subnet used for the quarantine VLAN)
!
set firewall modify PBR rule 10 modify table x
(Replace x with the routing table used for the quarantine VLAN)
!
set interfaces ethernet ethx vif x firewall in modify PBR
(Replace ethx with inbound interface for quarantine VLAN and x with
VLAN ID of quarantine VLAN)
!
commit ; save
## [NAC Configuration](/docs/manac/installation/ubiquiti-wireless-layer-2-integration#nac-configuration)

Ubiquiti leverages RADIUS assigned VLANs. The roles configured in the NAC RADIUS UI for the Ubiquiti NAS type should be configured as shown below.
