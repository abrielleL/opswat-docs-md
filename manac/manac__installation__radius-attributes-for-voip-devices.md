<!-- source: https://www.opswat.com/docs/manac/installation/radius-attributes-for-voip-devices -->

# RADIUS Attributes for VoIP Devices

## [Introduction](/docs/manac/installation/radius-attributes-for-voip-devices#introduction)

This article provides instructions and examples for configuring RADIUS attributes for VoIP devices. The most common use case for these attributes is to include the attributes in replies from the RADIUS server to a switch when a VoIP device connects to a switch port with authentication enabled. The switch, if properly configured, will then assign the VoIP device to the designated voice VLAN configured on the switch/port.

Info

NOTE - These instructions assume the NAC RADIUS server and switch have already been configured. See the [Network Integration](/docs/manac/installation/network-integration) page for instructions to configure the NAC RADIUS server, add the switch to the RADIUS server and configure the switch.

Info

NOTE - The general configuration of VoIP servers on a network is outside the scope of this article. These instructions assume VoIP services have already been configured and validated on a network prior to the NAC RADIUS server integration.

## [RADIUS Attribute Configuration](/docs/manac/installation/radius-attributes-for-voip-devices#radius-attribute-configuration)

Once the desired RADIUS Enforcement Role has been configured, below are two examples of VoIP RADIUS attributes and values that can be configured in the Enforcement Role. For general information on configuring Enforcement Roles, see the [Network Integration](/docs/manac/installation/network-integration) page. These instructions are specific to VoIP Enforcement Roles only.

Below is an example of a VoIP RADIUS attribute that can be sent back to a properly configured Cisco switch. Upon receiving an access-accept message from the NAC RADIUS server, the switch will place a VoIP device in the VoIP VLAN designated on the switch.

Below is an example of a VoIP RADIUS attribute that can be sent back to a properly configured Arris/Ruckus/Brocade (ICX) switch. Upon receiving an access-accept message from the NAC RADIUS server, the switch will place a VoIP device in the VoIP VLAN designated on the switch. The "T:" in the attribute value designates the Tagged voice VLAN configured on the switch. The "0" in the following attribute value instructs the switch not to perform 802.1X authentication on the switch port but to perform mac authentication instead. This allows phones that are not configured for 802.1X to connect to the network.

For additional information on RADIUS attributes required (above and beyond just a voice VLAN ID), please refer to the network equipment vendor's documentation.

Success

This concludes the configurations and examples for configuring RADIUS attributes for VoIP devices.
