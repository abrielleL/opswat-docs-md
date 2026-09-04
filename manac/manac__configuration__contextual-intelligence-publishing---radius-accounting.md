<!-- source: https://www.opswat.com/docs/manac/configuration/contextual-intelligence-publishing---radius-accounting -->

# Contextual Intelligence Publishing - RADIUS Accounting

Overview

Using Contextual Intelligence Publisher (CIP), Single Sign-On can be enabled for Vendor that accepts RADIUS accounting. Once configured, end users will be authenticated to the 3rd party system since the user credentials will be passed transparently from CIP. Integrating the two allows seamless identity-aware rulesets to be applied to individual users. The CIP integration currently provides the following values using RADIUS Accounting:

- Machine IP Address
- MAC Address
- Username

The purpose of this guide is to walk through the configuration requirements for sending identity information from CIP to a 3rd party system using RADIUS Accounting.

Prior to working through this document, the 3rd party system and NAC must be installed and functional on the network. CIP must also be installed in the NAC system. The following 3rd party systems are reported to work with RADIUS accounting:

- SonicWALL Firewall
- [Fortinet Firewall](/docs/manac/configuration/contextual-intelligence-publishing---radius-accounting#src-4084900_ContextualIntelligencePublishing-RADIUSAccounting-Fortinet) (Using FortiAuthenticator)
- Lightspeed Web Filter
- WatchGuard Firebox Firewall

## [Configure 3rd Party System](/docs/manac/configuration/contextual-intelligence-publishing---radius-accounting#configure-3rd-party-system)

On the 3rd party system, there are usually two configuration items that are needed:

1. Create a RADIUS client
2. Configure Single Sign-On to utilize RADIUS accounting

*NOTE: As all systems are different, specific instructions are not available in this document. Please consult the documentation of the 3rd party system for instructions, or contact <https://www.opswat.com/support/> to inquire if there is a Vendor specific document available for this integration.

## [Configure Contextual Intelligence Publisher](/docs/manac/configuration/contextual-intelligence-publishing---radius-accounting#configure-contextual-intelligence-publisher)

Once the 3rd party system is configured, open the NAC Configuration at <https://portal.myweblogon.com:8443/manage> ([portal.myweblogon.com](http://portal.myweblogon.com) can be replaced by the manager IP or a branded URL) and choose “Contextual Intelligence Publisher.” Click on “Add” and enter the following information:

- **Publisher:** RADIUS Accounting
- **Name:** A name to describe where CIP is publishing Data.
- **IP:** The IP of the 3rd party appliance
- **Port:** RADIUS accounting port – the default of 1813 is recommended
- **Protocol:** UDP
- **Shared Secret:** The shared secret configured in 3rd party system.

Once everything is entered, click “Submit”. Once save, data will start being published to 3rd party system.

## [Fortinet (FortiAuthenticator)](/docs/manac/configuration/contextual-intelligence-publishing---radius-accounting#fortinet-fortiauthenticator)

1. For Fortinet, NAC uses a RADIUS accounting format to publish events.
2. The Fortinet Publisher is a clone of the Generic RADIUS CIP publisher with one significant difference: for Fortinet there is a Class attribute setting that is an additional drop-down setting in the Fortinet CIP publisher settings.
3. This Class attribute is added into the published RADIUS accounting and derives its value from one of many different RADIUS attributes NAC tracks, but the most significant for Fortinet is the SSID attribute, which is cleansed to provide the SSID the device is connected to in a form expected by Fortinet for its Group names.
4. Specifically, the SSID attribute is derived by modifying the format of the Called-Station-Id attribute by stripping the beginning of the SSID name and appending a "class = RSSO" to the front of the SSID value obtained by NAC through RADIUS Accounting.
5. Providing the CLASS value in this form permits the Fortinet to track where the device connected to for auditing and control purposes.

## [Troubleshooting](/docs/manac/configuration/contextual-intelligence-publishing---radius-accounting#troubleshooting)

## [Usernames are not being populated in 3rd Party System](/docs/manac/configuration/contextual-intelligence-publishing---radius-accounting#usernames-are-not-being-populated-in-3rd-party-system)

In both appliance, verify that the shared secret and IP Addresses match. If there is a mismatch, RADIUS accounting will either be dropped by the 3rd party system, or never received.

Ensure that NAC has an IP Address, MAC address, and username in the device record. If any of these three components is not present, NAC will not generate RADIUS Accounting for the device. The most likely reason for one of these three to not be populated is a user has not yet authenticated, or there is not currently an input source (ie. DHCP Syslog or RADIUS Accounting from a wireless controller) providing MAC Address information. Please contact <https://www.opswat.com/support/> if more help is needed configuring these items.

## [Users timing out too quick](/docs/manac/configuration/contextual-intelligence-publishing---radius-accounting#users-timing-out-too-quick)

NAC publishing does not currently send RADIUS accounting Interim updates. If users are timing out too quickly, the 3rd party system will need to be configured with a timeout relative to end-user behavior on the network. This usually means that a timeout of greater than 8 hours will be preferred. NAC will send RADIUS accounting starts when a user logs into a device on the network and when a device receives a new IP address. NAC will also send a RADIUS accounting stop when a device leaves the network, or when a device releases an IP address.
