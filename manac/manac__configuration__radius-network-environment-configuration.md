<!-- source: https://www.opswat.com/docs/manac/configuration/radius-network-environment-configuration -->

# RADIUS Network Environment Configuration

## [Configure NAC as a RADIUS device for the network environment](/docs/manac/configuration/radius-network-environment-configuration#configure-nac-as-a-radius-device-for-the-network-environment)

Within the wired or wireless network infrastructure, the NAC appliance will need to be configured as a RADIUS server for both RADIUS authentication and RADIUS accounting. Depending on the vendor, this may be in one location or in two different locations.

When configuring NAC as a RADIUS server, be sure to use the same shared secret (sometimes called a password or key) for both authentication and accounting. This shared secret is specific to the communication between the network environment and NAC and will be needed again later in this document.

If NAC will be configured to proxy RADIUS requests to an upstream RADIUS server, NAC will need to be configured as a RADIUS client in the upstream RADIUS server.

Please consult your chosen vendor’s documentation for specific instructions to complete this step.

## [Configure WLANs or wired ports to use NAC as a RADIUS server](/docs/manac/configuration/radius-network-environment-configuration#configure-wlans-or-wired-ports-to-use-nac-as-a-radius-server)

Within the network infrastructure, configure a new SSID with WPA2-Enterprise security or a new port with 802.1x and choose NAC as the RADIUS server for both authentication and accounting.

Please consult your chosen vendor’s documentation for specific instructions to complete this step.
