<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---juniper-srx -->

# Contextual Intelligence Publishing - Juniper SRX

## [Overview](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---juniper-srx#overview)

Using Contextual Intelligence Publisher (CIP), Single Sign-On can be enabled for Juniper SRX and non-managed devices. Once configured, end users will no longer need to authenticate to Juniper SRX since the user credentials will be passed transparently from CIP. Integrating the two allows seamless identity-aware firewalling and greater ease of use for matching firewall traffic to individual users. The CIP integration currently provides the following values to Juniper SRX:

- Machine IP Address
- Username
- Group Memberships
- Device Type

The purpose of this guide is to walk through the configuration requirements for sending identity information from CIP to Juniper SRX.

Prior to working through this document, Juniper SRX and NAC must be installed and functional on the network. The Juniper SRX must be on firmware version 12.3X48 or newer. CIP must also be installed in the NAC system.

## [Configure Juniper SRX](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---juniper-srx#configure-juniper-srx)

In the firewall, the following commands should be run from the cli to enable the webapi.

**Enable the webapi:**

configure
set system services webapi user srx
set system services webapi user password "password"
set system services webapi client 10.100.210.200
set system services webapi http port 8080
set system services webapi https port 8443
set system services webapi https default-certificate
commit

Note: The user and password values should be modified to be specific to your installation. These items will need to be used later. The client should be the IP address of the NAC manager appliance.

**Allow webapi access from a specific zone:**

configure
set security zones security-zone [zonename] host-inbound-traffic system-services webapi-clear-text
set security zones security-zone [zonename] host-inbound-traffic system-services webapi-ssl
commit

Note: Replace [zonename] with the actual zone name of the NAC manager appliance.

**Verify the configurations are in place:**

show configuration system services webapi
## [Configure Contextual Intelligence Publisher](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---juniper-srx#configure-contextual-intelligence-publisher)

Once Juniper SRX is configured, open the NAC Configuration at [https://portal.myweblogon.com:8443/ConnectUI](https://auth.impulse.com:8443/ConnectUI) ([portal.myweblogon.com](http://auth.impulse.com) can be replaced by the manager IP or a branded URL) and choose “Contextual Intelligence Publisher.” Click on “Add” and enter the following information:

- **Publisher:** Juniper SRX
- **Name:** A name to describe where CIP is publishing Data.
- **Username:** API username configured in the Juniper SRX
- **Password:** API password configured in the Juniper SRX
- **IP:** The IP of the Juniper SRX appliance
- **Port:** https port configured for the Juniper SRX API

Once everything is entered, click “Submit”. Once save, data will start being published to Juniper SRX.

Once finished, click “Submit” and continue to the next section to verify the integration.

## [Verify Integration](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---juniper-srx#verify-integration)

In the Juniper SRX cli, the following can be run to verify that it is receiving data from NAC:

show services user-identification authentication-table authentication-source aruba-clearpass extensive
