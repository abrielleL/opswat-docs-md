<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility -->

# Optional - Configure Device Profiling and Visibility

- [Configure Profiling and Visibility](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#configure-profiling-and-visibility)

  - [Configure DHCP Syslog](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#configure-dhcp-syslog)
  - [Configure DHCP Device Identification](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#configure-dhcp-device-identification)
  - [Add desired subnets to NAC for Profiling/Visibility](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#add-desired-subnets-to-safeconnect-for-profilingvisibility)
  - [Test with endpoint to validate Profiling/Visibility](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#test-with-endpoint-to-validate-profilingvisibility)

## [Configure Profiling and Visibility](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#configure-profiling-and-visibility)

This section describes how to configure NAC Essentials to profile devices attached to the network for desired network subnets.

This section assumes that administrators have completed all the required steps on the [NetworkIntegrationSteps](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#src-4085153_safe-id-T3B0aW9uYWwtQ29uZmlndXJlRGV2aWNlUHJvZmlsaW5nL1Zpc2liaWxpdHktTmV0d29ya0ludGVncmF0aW9uU3RlcHM) page or the [NAC Layer 3 Integration](/docs/manac/nac-v8.1.1/installation/layer-3-integration-guide) page (for Layer 3 integrations only).

Info

The steps below are not required for 802.1X/WPA2E Authentication, mac authentication or Initial VLAN Assignment. They are only required for Device Profiling/Visibility.

## [Configure DHCP Syslog](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#configure-dhcp-syslog)

NAC will process DHCP syslog exported from DHCP servers to correlate IP and MAC addresses in real-time. The DHCP Syslog configuration is in the Configuration Manager under Network Inputs.

Select the appropriate DHCP vendor from the drop down list.

DHCP Syslog

Once vendor and IP are configured, click the Add button to add the server to NAC . Instructions for configuring the server to export syslog to NAC are located below the Add button.

## [Configure DHCP Device Identification](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#configure-dhcp-device-identification)

NAC will examine DHCP requests forwarded by DHCP relay agents to help with device fingerprinting. NAC will not respond to DHCP requests and does not act as a DHCP server, the requests are used for identification purposes only. The DHCP Device Identification configuration is in the Configuration Manager under Network Inputs.

Choose the appropriate vendor and expand the section for instructions on how to forward DHCP requests as seen in the example below.

## [Add desired subnets to NAC for Profiling/Visibility](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#add-desired-subnets-to-nac-for-profilingvisibility)

With the network integration tasks all completed, the next step is to define the desired subnet(s) in NAC . Adding a Subnet Definition in NAC is required for any subnet to be examined for Profiling/Visibility. Subnet Definitions can be added in the Configuration under Enforcement Setup.

To add a new subnet, click on Enable Configuration Mode and then click Add New Subnet.

Define Network Subnets

Define Network Subnets

Select the appropriate device from the Enforcement Device drop down menu and fill out the remaining fields, then click the Add button followed by the Commit Changes button. The Enforcement device will be RADIUS for Layer 2 integrations or a Layer 3 switch/router for Layer 3 integrations.

New Subnet Mappings

Next, click the Disable Configuration mode and the newly added subnet should show up in the list.

With the Subnet Definition added, the next step is to create a policy in NAC . The purpose the policy is to add the previously configured subnets to the system for Profiling/Visibility. Policies are configured in the Policy Manager portion of the NAC UI.

Once in the Policy Manager, select Qualifiers from the Qualifiers Menu drop down list.

Qualifiers Menu, Qualifiers

Create a subnet qualifier by clicking on the Subnet tab and filling in the network address under the IP address field, adding an optional description and clicking the Save button.

Qualifiers Menu, Subnets

To add the newly created Qualifier to a Qualifier Set, select Qualifier Set from the Qualifiers menu.

Qualifiers Menu, Qualifier Set

Give the Qualifier Set a name and highlight the new subnet qualifier in the left (Available) window.

Click the right arrow to move the new subnet qualifier to the right (Selected) window and click Save.

To add the Qualifier Set to a Qualifier Container, select Qualifier Container from the Qualifiers Menu.

Qualifier Menu, Qualifier Container

Give the Qualifier Container a name. With the Machine Types and Networking checkboxes checked, highlight and move “All host types” and the newly created Qualifier Set and move them to the Selected window.

Sandbox-Qualifier-Container

With all of the qualifying configuration complete, the next step is to create a Policy Group. Select Policy Group from the Policies Menu.

Give the Policy Group a name, select the Qualifier Container created in the previous step from the drop down list, click Save and then click Apply and Use.

To review the configurations, select Overview, expand the Policy Group and verify the data is correct.

Overview

## [Test with endpoint to validate Profiling/Visibility](/docs/manac/nac-v8.1.1/installation/optional---configure-device-profiling-and-visibility#test-with-endpoint-to-validate-profilingvisibility)

With all configuration tasks completed, a test endpoint device can be connected to the test subnet. The NAC Device Manager section of the UI is used to verify the status of online devices.

After connecting an endpoint to the test subnet and the device obtains an IP address, it should show up in the Device Manager in NAC. Click on the IP address or MAC address to view device details.

NAC Devices

The endpoint will also now show up as compliant with policy in Device Manager.

Device Details

Success

This concludes the steps required to configure and test Profiling and Visibility and completes the features available in NAC Essentials. NAC Essentials is the base product in the NAC family of products. For information on the additional features available in NAC Core and NAC Enterprise, please visit the links below.

NAC Standard Configuration Guide

NAC Enterprise Configuration Guide
