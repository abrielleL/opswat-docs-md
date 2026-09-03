<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/network-integration -->

# Network Integration

## [Introduction and Example Use Cases](/docs/manac/nac-v8.1.1/installation/network-integration#introduction-and-example-use-cases)

This article designed to provide network administrators the steps to enable NAC Essentials on the network. The configuration steps below will apply the necessary configurations for the following use cases.

## [Authenticate Users and Devices](/docs/manac/nac-v8.1.1/installation/network-integration#authenticate-users-and-devices)

### [802.1X Authentication](/docs/manac/nac-v8.1.1/installation/network-integration#8021x-authentication)

With the NAC RADIUS server joined to Active Directory and the network device (switch, AP, controller) properly configured, users will be able to authenticate to the wired or wireless network via 802.1x / EAP. Devices that are not able to successfully complete 802.1x / EAP authentication will not be able to connect the the local network at all. (I.e. They will not even be able to pull an IP.)

Supported EAP methods:

- EAP-PEAP (inner method MS-CHAPv2)
- EAP-TTLS (inner method PAP)
- EAP-TLS (cert-based auth)

### [Authentication for non-802.1X Capable Devices (including IoT)](/docs/manac/nac-v8.1.1/installation/network-integration#authentication-for-non-8021x-capable-devices-including-iot)

Using the NAC Authorized Devices feature, devices that are unable to be or are not configured for 802.1X/WPA2E can still be authenticated to the network via MAC address.

## [Assign Network Access](/docs/manac/nac-v8.1.1/installation/network-integration#assign-network-access)

### [Identity Based Network Access Assignment](/docs/manac/nac-v8.1.1/installation/network-integration#identity-based-network-access-assignment)

Devices successfully authenticated via 802.1X/WPA2E can optionally be assigned specific network access, such as VLAN ID. NAC will validate the group/OU a user belongs to and return the appropriate VLAN ID or desired RADIUS attributes.

### [MAC Address Based Network Access Assignment](/docs/manac/nac-v8.1.1/installation/network-integration#mac-address-based-network-access-assignment)

In addition to authenticating devices via MAC address, the NAC Authorized Devices feature also allows for RADIUS attributes such as VLAN ID to be returned when a device successfully authenticates. This ensures that no matter where on the network the device connects, it will also have the appropriate network access assigned. Common examples of this use case are phones and printers.

### [Guest VLAN](/docs/manac/nac-v8.1.1/installation/network-integration#guest-vlan)

Network integrated devices (switch, AP, controller) can be configured for Guest VLAN. User devices not configured for 802.1X/WPA2E, such as Guest or BYOD devices, can be placed in a Guest VLAN with restricted access, such as Internet only.

## [Network Integration Steps](/docs/manac/nac-v8.1.1/installation/network-integration#network-integration-steps)

Learn the steps required to integrate NAC into a customer Layer 2 network environment and validate the integration with a test policy. Note that this page only provides the minimum requirements needed to achieve network integration.

## [Enable the NAC RADIUS Server](/docs/manac/nac-v8.1.1/installation/network-integration#enable-the-nac-radius-server)

To access the NAC UI, navigate to the link below and login with NAC Admin credentials (admin/admin is the default username and password). <https://x.x.x.x:8443/manage>

NAC Login

Once logged into the NAC UI, the network integration options are located under Configuration Manager.

Once logged into Configuration Manager, click on Configuration under RADIUS in the left pane.

Once Configuration Mode is enabled, click on RADIUS Server and then click on the Enable button.

Click OK when prompted.

The Enforcement Status light should change from red to green indicating enforcement is enabled.

## [Select the RADIUS Authentication Type](/docs/manac/nac-v8.1.1/installation/network-integration#select-the-radius-authentication-type)

From the Authentication Type drop down list, select the appropriate authentication type.

If the desire is to not require endpoints to have 802.1X supplicants configured, the default Authentication Type of MAC Authentication Only is sufficient.

Info

If MAC Authentication Only is selected, skip to the NAS configuration steps (bypass EAP steps).

If the desire is to require endpoints to have 802.1X supplicants configured, Select EAP as the Authentication Type.

If EAP was selected as the Authentication Type, check the enabled check box and fill out the required fields and click the Join button.

Info

The Workgroup and NetBIOS Name fields are typically left blank and will be auto-populated.

If the desire is to require endpoints to have 802.1X supplicants configured and authenticate via client certificates (EAP-TLS), click on the TLS tab, click the Enable check box and upload the CA certificate to be used for EAP-TLS authentication.

Info

The CA certificate should be in the following format when uploaded:

`-----BEGIN CERTIFICATE-----`

`Base64 encoded Root Cert Info here`

`-----END CERTIFICATE-----`

Info

If using a certification chain, it should be in the following format when uploaded:

`-----BEGIN CERTIFICATE-----`

`Base64 encoded Intermediate Cert Info here`

`-----END CERTIFICATE-----`

`-----BEGIN CERTIFICATE-----`

`Base64 encoded Root Cert Info here`

`-----END CERTIFICATE-----`

Add a network device (switch, AP, controller) to NAC. Click on NAS then click on the New NAS button.

NAS

Fill in the requested fields. For this example, we will be adding a Cisco Layer 2 switch.

## [Configure RADIUS Enforcement Roles and Attributes](/docs/manac/nac-v8.1.1/installation/network-integration#configure-radius-enforcement-roles-and-attributes)

Click on Enforcement Roles.

The default quarantine role applies a pre-configured quarantine ACL that resides on the switch and the default compliant role will allow all access. These can be modified as desired or left as default.

## [Apply/Save RADIUS Configuration Changes](/docs/manac/nac-v8.1.1/installation/network-integration#applysave-radius-configuration-changes)

Navigate to "Apply". Click Apply and Use and OK.

Make sure no errors appear in the log.

## [Configure Device Authorization (for IoT or non-802.1X capable devices)](/docs/manac/nac-v8.1.1/installation/network-integration#configure-device-authorization-for-iot-or-non-8021x-capable-devices)

For endpoints that are not capable of or configured for 802.1X, the Device Authorization provides a quick and easy method for accessing specific network access privileges based on mac address. This maps a mac address to a specific Enforcement Role which will be applied to the endpoint any time it connects to the network. An common example of this feature would be to place VoIP devices in one VLAN and printers in another VLAN. Bulk upload of a list of mac addresses is supported.

In the Configuration Manager UI, click on Authorized Devices under Enforcement setup.

Click on the Bulk Upload button in the upper right-hand corner, then click Download Template.

Open the template spreadsheet that was downloaded and add a device MAC address(es) and the associated enforcement role(s). Save changes.

Click on Select File, locate and select the template spreadsheet and click Upload.

The MAC addresses should now show up in the UI under Authorized Devices in the UI.

Follow the steps in the [261816336](/docs/manac/nac-v8.1.1/installation/network-integration#src-4085198) section to configure the desired VLANs for the "phones" and "printers" enforcement roles and apply the changes.

## [Apply configurations to network devices](/docs/manac/nac-v8.1.1/installation/network-integration#apply-configurations-to-network-devices)

Once a network device has been added to NAC and the NAC RADIUS server has been configured, a script or other configurations will need to be applied to the device. Example scripts and configuration steps are provided on the [NAC Layer 2 Network Integration Scripts](/docs/manac/nac-v8.1.1/installation/layer-2-switch-controller-ap-integration-scripts) page.

Success

This concludes the integration steps to secure your network. Repeat the steps above for all network devices you would like to integrate with NAC until fully deployed.

Endpoints with properly configured supplicants will be able to authenticate to 802.1X/WPA2E enabled networks with optional network access assignment. Other devices can be assigned network access based on mac address. For assigning devices that do not match either of these categories to a Guest VLAN, refer to your switch, controller or AP manufacturer's instructions to enable the Guest VLAN feature.

Although not required to secure the network, Device Profiling/Visibility is also available for NAC Essentials. See the link below for information on that option.

[Optional - Configure Device Profiling/Visibility](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility)
