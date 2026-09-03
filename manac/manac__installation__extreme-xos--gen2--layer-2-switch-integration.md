<!-- source: https://www.opswat.com/docs/manac/installation/extreme-xos--gen2--layer-2-switch-integration -->

# Extreme XOS (Gen2) Layer 2 Switch Integration

Note: Assigning different VLANs per policy is only supported for initial VLAN assignment.

BashCopycreate vlan "Auth"
configure policy captive-portal web-redirect 1 server 1 url https://x.x.x.x:8443/ enable (replace x.x.x.x with IP of NAC appliance and remove comment)
configure policy profile 2 name "sc_compliant_policy" pvidstatus "enable" pvid x untagged-vlans x (replace x with VLAN ID for compliant users and remove comment)
configure policy profile 3 name "sc_guest_policy" pvid-status "enable" pvid x untagged-vlans x (replace x with VLAN ID for guest users and remove comment)
configure policy profile 4 name "sc_quarantine_policy" pvidstatus "enable" pvid x web-redirect 1 (replace x with VLAN ID for quarantined users and remove comment)
configure policy profile 5 name "sc_initial_policy" pvid-status "enable" pvid x untagged-vlans 14 (replace x with VLAN ID users should be assigned when connecting for the first time and remove comment)
Note – Below is an example of networks guest clients cannot access. Modify as necessary and remove this comment.
configure policy rule 3 ipdestsocket 10.0.0.0 mask 8 drop
configure policy rule 3 ipdestsocket 172.16.0.0 mask 20 drop
configure policy rule 3 ipdestsocket 192.168.0.0 mask 16 drop
Note – Do not remove any entries below.
configure policy rule 4 udpdestportIP 67 mask 16 forward
configure policy rule 4 tcpdestportIP 53 mask 16 forward
configure policy rule 4 tcpdestportIP 80 mask 16 forward
configure policy rule 4 tcpdestportIP 443 mask 16 forward
configure policy rule 4 tcpdestportIP 8443 mask 16 forward
configure policy captive-portal listening 80
configure policy captive-portal listening 8443
configure policy captive-portal listening 443
enable policy
configure radius netlogin primary server x.x.x.x 1812 client-ip y.y.y.y vr VR-Default (replace x.x.x.x with IP of NAC appliance and y.y.y.y with non-management IP of switch and if not using VR-Default replace with vr used, remove comment when done)
configure radius netlogin primary shared-secret ***** (replace ***** with shared secret and remove comment)
configure radius-accounting netlogin primary server x.x.x.x 1813 client-ip y.y.y.y vr VR-Default (replace x.x.x.x with IP of NAC appliance and y.y.y.y with non-management IP of switch and if not using VR-Default replace with vr used, remove comment when done)
configure radius-accounting netlogin primary shared-secret ***** (replace ***** with shared secret and remove comment)
configure radius dynamic-authorization 1 server x.x.x.x clientip y.y.y.y vr VR-Default shared-secret ***** (replace x.x.x.x with IP of NAC appliance and y.y.y.y with non-management IP of switch and if not using VR-Default replace with vr used, remove comment when done)
enable radius netlogin
enable radius-accounting netlogin
enable radius dynamic-authorization
enable netlogin dot1x mac
configure netlogin mac authentication database-order radius
configure netlogin add mac-list ff:ff:ff:ff:ff:ff 48
enable netlogin ports x:x dot1x (replace x:x with test port and remove comment)
enable netlogin ports x:x mac (replace x:x with test port and remove comment)
configure sflow sample-rate 256
configure sflow poll-interval 15
enable sflow
configure sflow collector x.x.x.x port 50001 vr "VR-Default" (replace x.x.x.x with IP of NAC appliance and remove comment)
configure sflow agent ipaddress x.x.x.x (replace x.x.x.x with IP of NAC appliance and remove comment)
configure sflow ports x:x sample-rate 256 (replace x:x with test port and remove comment)
enable sflow ports x:x ingress (replace x:x with test port and remove comment)
