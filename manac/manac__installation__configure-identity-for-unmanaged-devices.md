<!-- source: https://www.opswat.com/docs/manac/installation/configure-identity-for-unmanaged-devices -->

# Configure Identity for Unmanaged Devices

## [Configuring Identity for Unmanaged/BYOD Devices](/docs/manac/installation/configure-identity-for-unmanaged-devices#configuring-identity-for-unmanagedbyod-devices)

This section describes how to configure NAC Essentials to tie identity to unmanaged/BYOD devices.

This section assumes that administrators have completed all the required steps on the [741381518](/docs/manac/installation/configure-identity-for-unmanaged-devices#src-4085249) page or the [NAC Layer 3 Integration](/docs/manac/installation/layer-3-integration-guide) page (for Layer 3 integrations only).

Info

The steps below are not required for 802.1X/WPA2E Authentication, mac authentication or Initial VLAN Assignment. They are only required to tie identity to unmanaged devices.

## [Configure DHCP Syslog](/docs/manac/installation/configure-identity-for-unmanaged-devices#configure-dhcp-syslog)

NAC will process DHCP syslog exported from DHCP servers to correlate IP and MAC addresses in real-time. The DHCP Syslog configuration is in the Configuration Manager under Network Inputs.

Configuration Manager Menu

Select the appropriate DHCP vendor from the drop down list.

DHCP Syslog

Once vendor and IP are configured, click the Add button to add the server to NAC. Instructions for configuring the server to export syslog to NAC are located below the Add button.

## [Configure DHCP Device Identification](/docs/manac/installation/configure-identity-for-unmanaged-devices#configure-dhcp-device-identification)

NAC will examine DHCP requests forwarded by DHCP relay agents to help with device fingerprinting. NAC will not respond to DHCP requests and does not act as a DHCP server, the requests are used for identification purposes only. The DHCP Device Identification configuration is in the Configuration Manager under Network Inputs.

Choose the appropriate vendor and expand the section for instructions on how to forward DHCP requests as seen in example below.

## [Configure Authentication Sources](/docs/manac/installation/configure-identity-for-unmanaged-devices#configure-authentication-sources)

NAC can perform AD/LDAP look ups to correlate users to specific groups. The Authentication Sources configuration is in the Configuration Manager under Network Inputs.

Click on the Add button to add a new Authentication Source. Enter the required information and Save.

## [Add test subnet to NAC and configure test policy](/docs/manac/installation/configure-identity-for-unmanaged-devices#add-test-subnet-to-nac--and-configure-test-policy)

With all configuration tasks completed, a test endpoint device can be connected to the test subnet. The NAC Device Manager section of the UI is used to verify the status of online devices.

After connecting an endpoint to the test subnet and the device obtaining an IP address, it should show up in the Device Manager in NAC . Click on the IP address or MAC address to view device details.

The Device Manager has a feature which allows an Administrator or Help Desk technician to view the page displayed to the end user. Clicking on the user icon with the quarantine “ x ”, the same page which is being served by the NAC web server for the client is displayed.

Sign In

For testing purposes, use the NAC Admin account credentials to login. After entering credentials, checking the Acceptable Use Policy checkbox and clicking Sign In, a successful authentication will display a page letting the user know they are connected. At that point, the device is no longer quarantined on the network and should have whatever access that subnet permits.

The endpoint will also now show up as compliant with policy in Device Manager.

Device Details

Success

This concludes the steps required to configure and test Identity for Unmanaged/BYOD Devices. For additional Policy Configuration options, refer to the [Policy Manager Guide](/docs/manac/operating/policy-manager-guide) section. Additional documentation and user guides are located in the NAC [CK](/docs/manac/installation/configure-identity-for-unmanaged-devices#src-4085249).
