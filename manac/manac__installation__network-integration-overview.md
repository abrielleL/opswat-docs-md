<!-- source: https://www.opswat.com/docs/manac/installation/network-integration-overview -->

# Network Integration Overview

## [Network Integration Options Comparison](/docs/manac/installation/network-integration-overview#network-integration-options-comparison)

NAC may be integrated into a customer network environment leveraging either a Layer 3 or a Layer 2 integration option. The integration type may depend on several factors including network equipment vendors (make/model), network topology and customer security policy requirements.

At a high level, Layer 3 integrations quarantine devices at either the user VLAN/subnet default gateway or point of ingress on a Layer 3 integration switch/router if the VLAN/subnet is not directly connected while Layer 2 integrations quarantine devices *and* assign network access on the Layer 2 integrated device (switch, controller or access point as applicable).

A short list of pros/cons for each type of integration is listed below:

## [Layer 3 Integration Pros:](/docs/manac/installation/network-integration-overview#layer-3-integration-pros)

- Less complex than Layer 2 integrations
- Typically quicker/easier to deploy
- Typically fewer network devices to integrate with
- Fails open last state (quarantined devices blocked, compliant or new devices not blocked)
- High Availability less of a concern

## [Layer 3 Integration Cons:](/docs/manac/installation/network-integration-overview#layer-3-integration-cons)

- May not scale to desired levels depending on equipment, number of VLANs and number of users
- May have negative performance impact depending on equipment, number of VLANs and number of users
- Does not block East/West traffic on same network segment during quarantine
- Does not provide ability to assign different levels of network access for compliant users/devices
- Generally less secure than Layer 2 integrations

## [Layer 2 Integration Pros:](/docs/manac/installation/network-integration-overview#layer-2-integration-pros)

- More secure than Layer 3 integrations
- Blocks East/West traffic on same network segment during quarantine (some vendor limitations may apply)
- Provides ability to assign different levels of network access for compliant users/devices
- Typically no issues with scaling

## [Layer 2 Integration Cons:](/docs/manac/installation/network-integration-overview#layer-2-integration-cons)

- More complex than Layer 3 integrations
- Typically takes longer to deploy
- Typically more network devices to integrate
- Can fail closed in certain scenarios
- High Availability more of a concern

## [Supported Vendors (at time of publishing):](/docs/manac/installation/network-integration-overview#supported-vendors-at-time-of-publishing)

## [Layer 3 Integration:](/docs/manac/installation/network-integration-overview#layer-3-integration)

Alcatel-Lucent

Brocade/Ruckus/Arris/Extreme (ICX and MLX Series)

Cisco

Dell

HP

## [Layer 2 Integration Wireless:](/docs/manac/installation/network-integration-overview#layer-2-integration-wireless)

Cisco

Meraki

HPE-Aruba

Aerohive

Ruckus

Xirrus

Juniper-Mist

Extreme (Identifi)

Extreme (WiNG)

Ubiquiti

## [Layer 2 Integration Wired:](/docs/manac/installation/network-integration-overview#layer-2-integration-wired)

Cisco

HPE

Ruckus/Arris (ICX)

Dell

Juniper

Meraki

Extreme (XOS)

For more detailed information on models and versions support, refer to the [NAC Technical Requirements](/docs/manac/installation/technical-requirements).

## [Layer 3 Integration Overview](/docs/manac/installation/network-integration-overview#layer-3-integration-overview)

Layer 3 integrations quarantine devices at either the user VLAN/subnet default gateway or point of ingress on a Layer 3 integration switch/router if the VLAN/subnet is not directly connected. Devices are detected through various network inputs (Netflow/sFlow, DHCP, RADIUS Accounting), assessed for policy and either quarantined or allowed on the network. If allowed on the network, a device will have whatever network access is provided by the VLAN/subnet the device resides in. Quarantined devices are redirected to NAC by dynamic ACL updates sent to the Layer 3 switch/router when a device falls out of compliance. For locally connected user VLANs/subnets, East/West traffic within a segment is permitted but traffic beyond a user device default gateway (Layer 3 interface) is not permitted unless an explicit exception is configured. Common exceptions include remediation resources, anti-virus servers, etc. Capacity for ACL updates may vary depending on make/model of Layer 3 switch/router. For high volume environments (such as wireless with open SSIDs, etc) a Layer 2 integration is recommended.

## [Layer 2 Integration Overview](/docs/manac/installation/network-integration-overview#layer-2-integration-overview)

Layer 2 integrations quarantine devices *and* assign network access on the Layer 2 integrated device (switch, controller or access point as applicable). Devices are detected through various network inputs (Netflow/sFlow, DHCP, RADIUS Accounting), assessed for policy and either quarantined or allowed on the network with the appropriate level of access (for example, assigned to a specific VLAN or specific ACL applied). Quarantined devices are redirected to NAC utilizing RADIUS Change of Authorization (CoA) updates sent to the Layer 2 integrated device (switch, controller or access point as applicable) when a device falls out of compliance. All routed traffic is blocked unless a specific exception is configured. Common exceptions include remediation resources, anti-virus servers, etc. If Layer 2ACLs are also supported by the vendor, East/West traffic within a segment may also be blocked. Capabilities for Layer 2 enforcement options may vary depending on make/model of Layer 2 device and what RADIUS attributes are supported.
