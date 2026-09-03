<!-- source: https://www.opswat.com/docs/manac/installation/juniper-ex-vqfx-integration -->

# Juniper EX/vQFX integration

Note – In this example, an Juniper vQFX configuration is provided as tested on 18.4R1.8 firmware and 20.3R1.8 firmware, however any Juniper-Switch EX/QFX supporting the following features are eligible for integration.

- **<NAC-IP>** is the NAC VM IP address (e.g. 10.40.177.2)
- **<NAC-Subnet>** is a subnet containing both the NAC IP and Juniper interface IP (e.g. 10.40.177.0/28)
- **<Client-Subnet>** is a subnet where clients will connect from (e.g. 10.40.180.243/28).***NOTE:*** *The network portion of this CIDR string must be the IP of the Juniper gateway interface for the subnet*

XmlCopyfirewall {
family inet {
filter fil {
term dns_dhcp {
from {
destination-port [ 53 67 ];
}
then accept;
}
term internal {
from {
destination-address {
<NAC-IP>;
198.31.193.211/32;
# IPs for other internal resources can be added here.
# Blocked devices will still be able to access these.
}
}
then accept;
}
term impulse_block {
from {
source-address {
1.1.1.1/32;
# Other IPs will be added here as they are blocked by the NAC.
}
}
then {
count to-enforcer-count;
routing-instance to-enforcer;
}
}
term default {
then accept;
}
}
}
}
forwarding-options {
storm-control-profiles default {
all;
}
dhcp-relay {
server-group {
DHCP_SERVER_1 {
<NAC-IP>;
}
}
group DHCP_GROUP {
active-server-group DHCP_SERVER_1;
}
group DHCP {
interface xe-0/0/0.0;
}
}
}
protocols {
igmp-snooping {
vlan default;
}
sflow {
polling-interval 60;
collector <NAC-IP> {
udp-port 5001;
}
interfaces xe-0/0/0.0;
}
}
policy-options {
policy-statement FBF-export {
term 1 {
from {
instance master;
route-filter <NAC-Subnet> exact;
}
then accept;
}
term 2 {
then reject;
}
}
}
routing-instances {
TEST-VR {
instance-type virtual-router;
}
to-enforcer {
instance-type virtual-router;
routing-options {
static {
route 0.0.0.0/0 next-hop <NAC-IP>;
}
instance-import FBF-export;
}
}
}
############# LAYER 3 interface VLAN #####################
interfaces {
xe-0/0/0 {
unit 0 {
family inet {
filter {
input fil;
}
address <Client-Subnet>;
}
}
}
}
