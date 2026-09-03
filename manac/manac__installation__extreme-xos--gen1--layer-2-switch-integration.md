<!-- source: https://www.opswat.com/docs/manac/installation/extreme-xos--gen1--layer-2-switch-integration -->

# Extreme XOS (Gen1) Layer 2 Switch Integration

Note: Gen 1 switches do not support RADIUS COA, so only initial VLAN assignment is possible.

BashCopycreate vlan "Auth"
configure radius netlogin primary server x.x.x.x 1812 client-ip y.y.y.y vr VR-Default (replace x.x.x.x with IP of NAC appliance and y.y.y.y with non-management IP of switch and if
not using VR-Default replace with vr used, remove comment when done)
configure radius netlogin primary shared-secret ***** (replace ***** with shared secret and remove comment)
enable radius netlogin
configure netlogin vlan Auth (no ports should be assigned to this VLAN as it is used for clients to authenticate via RADIUS, remove comment)
configure radius-accounting netlogin primary server x.x.x.x 1813 client-ip y.y.y.y vr VR-Default (replace x.x.x.x with IP of NAC appliance and y.y.y.y with non-management IP of
switch and if not using VR-Default replace with vr used, remove comment when done)
configure radius-accounting netlogin primary shared-secret ***** (replace ***** with shared secret and remove comment)
enable radius netlogin
enable radius-accounting netlogin
configure netlogin vlan Auth (no ports should be assigned to this VLAN as it is used for clients to authenticate via RADIUS, remove comment)
enable netlogin dot1x mac
configure netlogin dynamic-vlan enable
configure netlogin dynamic-vlan uplink-ports x:x (replace x:x with uplink port for switch and remove comment)
configure netlogin mac authentication database-order radius
configure netlogin add mac-list default
enable netlogin ports x:x dot1x (replace x:x with test port and remove comment)
enable netlogin ports x:x mac (replace x:x with test port and remove comment)
configure netlogin ports x:x mode port-based-vlans (replace x:x with test port and remove comment)
configure netlogin ports x:x no-restart (replace x:x with test port and remove comment)
configure sflow sample-rate 256
configure sflow poll-interval 15
enable sflow
configure sflow collector x.x.x.x port 50001 vr "VR-Default" (replace x.x.x.x with IP of NAC appliance and remove comment)
configure sflow agent ipaddress x.x.x.x (replace x.x.x.x with IP of NAC appliance and remove comment)
configure sflow ports x:x sample-rate 256 (replace x:x with test port and remove comment)
enable sflow ports x:x ingress (replace x:x with test port and remove comment)
