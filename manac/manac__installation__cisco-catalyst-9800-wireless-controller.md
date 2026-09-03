<!-- source: https://www.opswat.com/docs/manac/installation/cisco-catalyst-9800-wireless-controller -->

# Cisco Catalyst 9800 Wireless Controller integration

**Overview**

The following guide covers Cisco Catalyst 9800 WLAN Controller configurations required to integrate the controller with NAC to be leveraged as an enforcement device. Cisco Catalyst 9800 WLAN controllers running 17.3 or later are supported for centrally switched traffic. Radius Based Enforcement (RBE) is supported for Open networks and for Secure networks using WPA2E/802.1x. By configuring your NAC Enforcer as an Authentication and Accounting Server, creating Access-Lists and leveraging features available in the WLAN controller, NAC will be enabled to block, redirect or limit access based on NAC Policy Group definitions.

**Network Preparation and Testing**

Prior to integration with NAC, please confirm that the WLANs you will be integrating are fully functional. A simple test of successfully associating with the SSID and browsing to a non-cached website should suffice. Ensure the static route below is added to the Layer 3 routing device upstream of your wireless controller(s). Please contact your Network Specialist if you require assistance with this task.

Static Route (apply if NAC is not integrated with wired network)

XmlCopyconf t
!
ip route 198.31.193.211 255.255.255.255 <NAC-IP>
!
end

**Add NAC Enforcer as a RADIUS Authentication server globally**

XmlCopyconfig t
!
aaa new-model
!
radius server <NAC-IP>
address ipv4 <NAC-IP> auth-port 1812 acct-port 1813
timeout 5
retransmit 2
key 7 <XXXXX>
!
!
!
aaa group server radius NAC_RBE
server name <NAC-IP>
deadtime 5
!
aaa group server radius NAC_Acct
server name <NAC-IP>
deadtime 5
aaa server radius dynamic-author
client <NAC-IP> server-key <Shared-Secret>
!
aaa authentication dot1x NAC_RBE_List group NAC_RBE group radius
aaa accounting update periodic 5
aaa accounting identity NAC_Acct_List start-stop group NAC_Acct
aaa authorization exec NAC_Authz_List group NAC_RBE
aaa authorization network NAC_MAC_Auth group NAC_RBE

**ACL Configuration**

XmlCopyip access-list extended sc_compliant_acl
permit ip any any
ip access-list extended sc_initial_acl
permit ip any any
ip access-list extended sc_quarantine_acl
deny ip any host 198.31.193.211
deny ip host 198.31.193.211 any
deny ip any host <NAC-IP>
deny ip host <NAC-IP> any
deny udp any any eq domain
deny udp any eq domain any
deny udp any any eq bootps
deny udp any eq bootps any
permit tcp any any eq www
#### [Enable Redirection for HTTP or HTTPs](/docs/manac/installation/cisco-catalyst-9800-wireless-controller#enable-redirection-for-http-or-https)

The web admin portal configuration is tied with the web authentication portal configuration and it needs to listen on port 80 in order to redirect. Ensure that you have the command "***ip http server***" for redirection on HTTP.

If you want to be redirected when you try to access an HTTPs URL, then add the command "*intercept-https-enable*" under the parameter map:

XmlCopyip http server
ip http secure-server
parameter-map type webauth global
type webauth
intercept-https-enable
trustpoint xxxxx
#### [Secure WPA2E/802.1X Wireless RBE Configuration](/docs/manac/installation/cisco-catalyst-9800-wireless-controller#secure-wpa2e8021x-wireless-rbe-configuration)

XmlCopyconfig t
wlan <Secure-SSID-Name> 1 <Secure-SSID-Name>
security dot1x authentication-list NAC_RBE_List
security web-auth parameter-map global
no shutdown
# Policy Profile Configuration
wireless profile policy NAC_policy
aaa-override
accounting-list NAC_Acct_List
nac
vlan <VLAN-ID>
no shutdown
# Link your WLAN profile to desired Policy Profile.
wireless tag policy "NAC Policy"
wlan <Secure-SSID-Name> policy NAC_policy
# To assign the same Policy Tag to APs
ap <ethernet-mac-addr>
policy-tag "NAC Policy"
#### [Open Wireless RBE Configuration](/docs/manac/installation/cisco-catalyst-9800-wireless-controller#open-wireless-rbe-configuration)

XmlCopywlan <Open-SSID-Name> 2 <Open-SSID-Name>
mac-filtering NAC_MAC_Auth
ip access-group web sc_quarantine_acl
security dot1x authentication-list NAC_RBE_List
security web-auth parameter-map global
no shutdown
# Policy Profile Configuration
wireless profile policy NAC_Guest_policy
aaa-override
accounting-list NAC_Acct_List
nac
vlan <VLAN-ID>
no shutdown
# Link your WLAN profile to desired Policy Profile.
wireless tag policy "NAC Policy"
wlan <Open-SSID-Name> policy NAC_Guest_policy
# To assign the same Policy Tag to APs
ap <ethernet-mac-addr>
policy-tag "NAC Policy"

This completes the WLAN controller configuration. Please run the commands below, and send the results to your NAC Network Engineer for next steps to complete integration validation testing

XmlCopy# show run wlan // WLAN configuration
# show run aaa // AAA configuration (server, server group, methods)
# show aaa servers // Configured AAA servers
# show ap config general // AP's configurations
# show ap name <ap-name> config general // Detailed configuration of specific AP
# show ap tag summary // Tag information for AP'S
# show wlan { summary | id | name | all } // WLAN details
# show wireless tag policy detailed <policy-tag-name> // Detailed information on given policy tag
# show wireless profile policy detailed <policy-profile-name>// Detailed information on given policy profile
