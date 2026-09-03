<!-- source: https://www.opswat.com/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts -->

# Layer 2 Switch/Controller/AP Integration Scripts

The following scripts are provided to integrate Layer 2 Switches/Controllers and APs with NAC. In order for this integration to function, the steps on the [Network Integration](/docs/manac/installation/network-integration) page must be completed.

## [Supported Vendors:](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#supported-vendors)

Info

**NOTE:** The list of supported vendors below is not exhaustive. MetaDefender NAC's L2 enforcement integration relies on standard RADIUS protocol. The specific minimum features required for networking equipment are:

- **RFC 4675:** VLAN assignment based on RADIUS attributes. (Allows NAC to assign a VLAN)
- **RFC 5176:** Dynamic authorization - CoA/Disconnect. (Allows NAC to update a device's access after it has already connected)

Most enterprise networking equipment supports these features. For wired integrations, only access switches need to support them.

If you suspect your equipment meets the criteria above but you do not see documentation for it here, please contact OPSWAT Support (<opswat-support@opswat.com>)

## [Layer 2 Integration Wireless:](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#layer-2-integration-wireless)

Aerohive

Alcatel (OmniSwitch)

Cisco

Extreme (Identifi)

Extreme (WiNG)

HPE-Aruba

Juniper-Mist

Meraki

Ruckus

Xirrus

## [Layer 2 Integration Wired:](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#layer-2-integration-wired)

Cisco

Dell

Extreme (XOS)

HPE

Juniper

Ruckus/Arris (ICX)

For more detailed information on models and versions support, refer to the [NAC Technical Requirements](/docs/manac/installation/technical-requirements). If your Layer 2 infrastructure is not supported, refer to the [NAC Network Integration Overview](/docs/manac/installation/network-integration-overview) page for additional information on the NAC Layer 3 integration options.

If any errors are encountered or there are questions regarding the script, email [opswat-support@opswat.com](mailto:opswat-support@opswat.com) with the make/model of the device along with a screenshot of the errors and a support ticket will be generated.

## [Aerohive Wireless Layer 2 Integration (HM-6)](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#aerohive-wireless-layer-2-integration-hm-6)

[NAC for Aerohive HiveManager6 - RBE Configuration Guide.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085325_1_MetaAccess_NAC_for_Aerohive_HiveManager6_-_RBE_Configuration_Guide.pdf)

## [Aerohive Wireless Layer 2 Integration (HM-NG)](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#aerohive-wireless-layer-2-integration-hm-ng)

[NAC for Aerohive HiveManagerNG Configuration Guide.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085326_1_MetaAccess_NAC_for_Aerohive_HiveManagerNG_Configuration_Guide.pdf)

## [Alcatel OmniSwitch 2 Switch Integration Script](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#alcatel-omniswitch-2-switch-integration-script)

<https://docs.opswat.com/manac/installation/alcatel-omniswitch-2-switch-integration-script>

## [Cisco Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#cisco-wireless-layer-2-integration)

<https://docs.opswat.com/manac/installation/cisco-wireless-layer-2-integration>

## [Cisco Wired Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#cisco-wired-layer-2-integration)

<https://docs.opswat.com/manac/installation/cisco-wired-layer-2-integration>

## [Cisco Wired Layer 2 Integration (2960X/XR)](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#cisco-wired-layer-2-integration-2960xxr)

<https://docs.opswat.com/manac/installation/cisco-wired-layer-2-integration0m3>

## [Cisco Wired Layer 2 Integration (IE2000)](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#cisco-wired-layer-2-integration-ie2000)

<https://docs.opswat.com/manac/installation/cisco-wired-layer-2-integrationfy5>

## [Dell Wired Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#dell-wired-layer-2-integration)

[NAC Dell-EMC N-Series and S-Series SafeConnect Layer 2 Integration Guide.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085327_1_MetaAccess_NAC_Dell-EMC_N-Series_and_S-Series_SafeConnect_Layer_2_Integration_Guide.pdf)

## [Extreme (Identifi) Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#extreme-identifi-wireless-layer-2-integration)

<https://docs.opswat.com/manac/installation/extreme--identifi--wireless-layer-2-integration>

## [Extreme (WiNG) Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#extreme-wing-wireless-layer-2-integration)

<https://docs.opswat.com/manac/installation/extreme--wing--wireless-layer-2-integration>

## [Extreme XOS (Gen1) Layer 2 Switch Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#extreme-xos-gen1-layer-2-switch-integration)

<https://docs.opswat.com/manac/installation/extreme-xos--gen1--layer-2-switch-integration>

## [Extreme XOS (Gen2) Layer 2 Switch Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#extreme-xos-gen2-layer-2-switch-integration)

<https://docs.opswat.com/manac/installation/extreme-xos--gen2--layer-2-switch-integration>

## [HP-Aruba Controller Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#hp-aruba-controller-wireless-layer-2-integration)

<https://docs.opswat.com/manac/installation/aruba-wireless-arubaos-8>

## [HP-Aruba Instant Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#hp-aruba-instant-wireless-layer-2-integration)

<https://docs.opswat.com/manac/installation/aruba-instant--arubaos-8--integration>

## [HP-Aruba Wired Layer 2 Integration (ArubaOS)](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#hp-aruba-wired-layer-2-integration-arubaos)

<https://docs.opswat.com/manac/installation/hp-aruba-wired-layer-2-integration--arubaos->

## [HP-Aruba Wired Layer 2 Integration (ArubaOS-Switch)](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#hp-aruba-wired-layer-2-integration-arubaos-switch)

<https://docs.opswat.com/manac/installation/hp-aruba-wired-layer-2-integration--arubaos-switch->

## [Juniper Wired Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#juniper-wired-layer-2-integration)

[NAC Juniper nce-EX-SafeConnect-Employee-and-Guest-Access.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085322_1_MetaAccess_NAC_Juniper_nce-EX-SafeConnect-Employee-and-Guest-Access.pdf)

## [Juniper-Mist Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#juniper-mist-wireless-layer-2-integration)

<https://docs.opswat.com/manac/installation/juniper-mist-wireless-layer-2-integration>

## [Meraki Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#meraki-wireless-layer-2-integration)

[NAC Meraki Integration Guide.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085329_1_SafeConnect_Meraki_Integration_Guide.pdf)

## [Meraki Wired Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#meraki-wired-layer-2-integration)

[NAC Meraki Wired Integration Guide.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085315_1_MetaAccess_NAC_Meraki_Wired_Integration_Guide.pdf)

## [Ruckus Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#ruckus-wireless-layer-2-integration)

[Ruckus Wireless NAC Integration Guide.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085332_1_Ruckus_Wireless_SafeConnect_Integration_Guide.pdf)

## [Brocade-Ruckus-Arris Wired Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#brocade-ruckus-arris-wired-layer-2-integration)

<https://docs.opswat.com/manac/installation/brocade-ruckus-arris-wired-layer-2-integration>

## [Ubiquiti Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#ubiquiti-wireless-layer-2-integration)

<https://docs.opswat.com/manac/installation/ubiquiti-wireless-layer-2-integration>

## [Xirrus Wireless Layer 2 Integration](/docs/manac/installation/layer-2-switch-controller-ap-integration-scripts#xirrus-wireless-layer-2-integration)

[NAC for Xirrus Integration Guide.pdf](https://onlinehelp.opswat.com/safeconnect-enforcer/attachments_4085323_1_MetaAccess_NAC_for_Xirrus_Integration_Guide.pdf)
