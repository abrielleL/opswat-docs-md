<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/dell-wired--dynamic-vlan- -->

# Dell Wired (dynamic VLAN)

The following document provides steps for configuring a Dell switch for dynamic-VLAN-based enforcement with NAC.

In this use case above, the Dell N-Series switch is configured to authenticate against the NAC RADIUS Server. Since MAC authentication is also supported, no supplicant configuration is required on the end user wired device. However, 802.1X for managed devices is also supported.

For Managed devices connecting to the switch, 802.1X authentication will be performed. After authentication takes place, the NAC RADIUS server will dynamically assign the Managed device the appropriate level of access. This is achieved by leveraging VLAN/Filter-Id RADIUS attributes and Dynamic VLAN/ACL Assignment on the NSeries switch.

For unmanaged devices connecting to the switch port, MAC authentication is performed. The MAC authentication will initially place the user in the Quarantine VLAN for Captive Portal user authentication to capture identity. Policy Based Routing (PBR) configuration on the Dell Layer 3 switch (N-Series or S-Series) or Dell SonicWall will redirect traffic received in the Quarantine VLAN to NAC . After authentication a RADIUS Change of Authorization (CoA) will be sent from the NAC RADIUS server to the N-Series Layer 2 switch and the user will be placed in the Guest VLAN/ACL.

### [Configuration:](/docs/manac/nac-v8.1.1/installation/dell-wired--dynamic-vlan-#configuration)

The following configuration commands are not intended to comprise the entire configuration needed for a fully functional access switch but contain the key configurations needed to enable the features described in this document. The commands below assume that the switch is fully functional and all production VLANs and the quarantine VLAN haves already been configured. It is recommended that the integration is verified on a test VLAN/port before applying configurations to a production VLAN/port(s).

Configuring a Dell S-Series (OS9) Layer 2 switch

Example - NAC VM is <NAC-IP>, VLAN ID is <VLAN-ID>

configure t
!
interface GiX/X/X (uplink ports and all other ports except for test port)
dot1x port-control force-authorized
!
dot1x authentication
!
radius dynamic-auth
dynamic-auth-enable
client <NAC-IP> key “radius-key”
!
radius-server host <NAC-IP> key “radius-key”
!
interface GiX/X/X (client test port)
switchport
dot1x authentication
dot1x mac-auth-bypass
dot1x auth-type mab-only (if no supplicants will be used on clients)
!
copy running-config startup-config

Configuring the Dell S-Series (OS9) Layer 3 Switch Quarantine VLAN Redirect

NOTE – This script includes CAM configuration for PBR which requires a switch reload. In order for PBR to function properly, a switch reload must be performed. NOTE - The be sure to delete the CAM configuration not required for your model.

configure t
!
cam-acl l2acl 1 ipv4acl 1 ipv6acl 0 ipv4qos 1 l2qos 1 l2pt 0 ipmacacl 0 vman-qos 0 ecfmacl 0
ipv4pbr 9 (use these settings for S4000)
cam-acl l2acl 1 ipv4acl 2 ipv6acl 0 ipv4qos 1 l2qos 1 l2pt 0 ipmacacl 0 vman-qos 0 ecfmacl 0
ipv4pbr 8 (use these settings for S6000)
!
ip redirect-list sc-quarantine
seq 1 permit udp any any eq 53
seq 2 permit udp any any eq 68
seq 3 permit ip any host x.x.x.x (IP of customer landing page web server)
seq 4 redirect <NAC-IP> ip any any
!
Interface vlan <VLAN-ID>
description NAC Quarantine VLAN
ip address 10.10.30.1/24
ip redirect-group sc-quarantine
!
Interface vlan <VLAN-ID>
description NAC Appliance/VM VLAN
ip address 10.10.10.1/24
!
end
!
copy running-config startup-config
