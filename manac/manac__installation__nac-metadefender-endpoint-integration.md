<!-- source: https://www.opswat.com/docs/manac/installation/nac-metadefender-endpoint-integration -->

# NAC and MetaDefender Endpoint Integration

NAC now supports integration with MetaDefender IT Access through the installation of an MetaDefender Endpoint that bundles the NAC Policy Key. The Dual Agent Integration enables network access control based on the installation of the MetaDefender Endpoint and compliance with MetaDefender IT Access. Devices attempting to access the network will be required to install, run, and become compliant with MetaDefender IT Access before receiving access.

## [Deployment](/docs/manac/installation/nac-metadefender-endpoint-integration#deployment)

NAC relies on the MetaDefender Endpoint to report the MetaDefender IT Access compliance of a device. The MetaDefender IT Access administrator is free to create arbitrary complex policies for devices and NAC will ensure the device is compliant with said policies before allowing a device access to a network.

*Note: Because the* *MetaDefender Endpoint* *receives its configuration from, and reports compliance data to* *MetaDefender IT Access, it is necessary to allow outbound HTTPS traffic to* [*gears.opwat.com*](gears.opwat.com) *for quarantined devices. The best way to accomplish this will vary based on your network and integration method. If you are unsure how to allow this traffic on your network, feel free to reach out to your OPSWAT Support representative for guidance.*

To enable the MetaDefender Endpoint and MetaDefender IT Access Compliance policies in NAC, the administrator must retrieve the MetaDefender IT Access license key from the “Settings > Global > Account” subsection under the MetaDefender IT Access Settings and enter the key into the “MetaDefender IT Access Integration” subsection in the NAC configuration.

*Note: If you have any pending changes in the Policy Manager portion of the NAC UI, you need to click "Apply and Use" .*

## [NAC and MetaDefender IT Access Integration](/docs/manac/installation/nac-metadefender-endpoint-integration#nac-and-metadefender-it-access-integration)

After saving the MetaDefender IT Access license Key in the NAC configuration, the MetaDefender Endpoint policy will be available in the NAC Policy Manager as both a Quarantine and Audit policy.

The MetaDefender Endpoint policy is configured to display remediation pages that allow users to:

1. Download the MetaDefender Endpoint + Policy Key bundle
2. Give instruction on checking MetaDefender IT Access Compliance
