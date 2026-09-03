<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/alcatel-lucent-layer-3-integration-script--6850-6900- -->

# Alcatel-Lucent Layer 3 Integration Script (6850/6900)

**This document provides scripts required to complete the installation of the NAC Solution**

**NAC Router Integration Script**

PowershellCopysflow receiver 1 name NAC address x.x.x.x udp-port 50001 packet- size 1400 version 5 timeout 0 (replace x.x.x.x with IP of NAC appliance and remove this comment)
sflow sampler 1 x/x receiver 1 rate 1 sample-hdr-size 128 (Layer 2 interface(s) that user traffic will ingress on, remove this comment)
sflow poller 1 x/x receiver 1 interval 5 (Layer 2 interface(s) that user traffic will ingress on, remove this comment)
ip helper vlan x address x.x.x.x (replace x.x.x.x with IP of NAC appliance and remove this comment)
policy network group intranet x.x.x.x (Replace with IP of AD server and remove this comment)
policy network group intranet x.x.x.x (Replace with IP of AV server and remove this comment)
policy network group impulse_block 1.1.1.1 (placeholder, remove this comment)
policy service svc-dhcp destination udp port 67 policy service svc-dns destination udp port 53
policy service group protocolallow svc-dhcp svc-dns
policy condition to-protocolallow service group protocolallow policy condition to-intranet destination network group intranet policy condition to-enforcer destination ip 198.31.193.211 policy condition noncompliant source network group impulse_block
policy rule intranet-rule precedence 150 condition to-intranet action AllowTraffic
policy rule protocol-rule precedence 140 condition to-protocolallow action allowprotocol
policy rule enforcer-rule precedence 130 condition to-enforcer action next-hop-enforcer
policy rule block precedence 120 condition noncompliant action next-hop- enforcer
policy action AllowTraffic policy action allowprotocol
policy action next-hop-enforcer permanent gateway ip x.x.x.x (replace x.x.x.x with IP of NAC appliance and remove this comment)
qos apply

***Note – Be sure to also allow the** **NAC** **Enforcer access to the router if a VTY/SSH access-list is present on the router.**
