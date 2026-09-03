<!-- source: https://www.opswat.com/docs/manac/nac-cloud/release-notes -->

# Release Notes

## [10.1.17 MetaDefender NAC On-prem - 26 Dec, 2025](/docs/manac/nac-cloud/release-notes#10117-metadefender-nac-on-prem---26-dec-2025)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- RADIUS capabilities

  - Support for EAP-TLS (certificate-based) authentication.
  - EAP-TTLS Authentication
  - EAP-PEAP Authentication

## [1.14 MetaDefender NAC Cloud - 17 Sep, 2025](/docs/manac/nac-cloud/release-notes#114-metadefender-nac-cloud---17-sep-2025)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- **Add Threat Severity condition for Rule**

  - OT Security integration by enforcing security policy according to the threat severity.

#### [Enhancements](/docs/manac/nac-cloud/release-notes#enhancements)

- Security enhancements

## [1.13 MetaDefender NAC Cloud - 20 Aug, 2025](/docs/manac/nac-cloud/release-notes#113-metadefender-nac-cloud---20-aug-2025)

#### [Enhancements](/docs/manac/nac-cloud/release-notes#enhancements)

- Added NetBIOS Name to the configuration of EAP-PEAP
- Minor bug fixes.

## [1.12 MetaDefender NAC Cloud - 16 Jul, 2025](/docs/manac/nac-cloud/release-notes#112-metadefender-nac-cloud---16-jul-2025)

#### [Enhancements](/docs/manac/nac-cloud/release-notes#enhancements)

- **Device Classification Enhancement**

  - Expand the existing Device Classification Override functionality to support bulk operations, allowing administrators to select multiple Unknown Devices and apply the same classification (Device type, OS) simultaneously.

## [1.11 MetaDefender NAC Cloud - 18 Jun, 2025](/docs/manac/nac-cloud/release-notes#111-metadefender-nac-cloud---18-jun-2025)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- **Device Classification Override**

  - Administrators can manually update Device Classification information (such as: Device type, OS) of an **Unknown Device.** Later, if another Unknown Device accesses the Network with the same DHCP request list, it will automatically inherit the same classification.

#### [Enhancements](/docs/manac/nac-cloud/release-notes#enhancements)

- **Restructure RADIUS Rule**

  - RADIUS Rule has been restructured, allowing administrators to aggregate attributes from multiple sources (Certificate, Endpoint, RADIUS, LDAP, SAML, etc.) within flexible policy structures. The new Rule supports both individual conditions and grouped condition sets, connected by AND/OR operators, enabling complex hierarchical logic.
- **Add LDAP-based conditions for Rule**

  - MetaDefender NAC now supports LDAP-based attributes from EAP-TTLS and LDAP authentication via Captive Portal, alongside existing endpoint and certificate attributes, giving you more granular control over network access policies.

## [1.10 MetaDefender NAC Cloud - 21 May, 2025](/docs/manac/nac-cloud/release-notes#110-metadefender-nac-cloud---21-may-2025)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- **Guest Sponsorship**

  - Added a new validation method for sponsor approval when Guest register to access Network, which will required sponsor approval before granting network access to guests. This enhances security while streamlining the approval process with customizable notification settings for sponsors.

#### [Enhancements](/docs/manac/nac-cloud/release-notes#enhancements)

- **Add Cert-based conditions for Rule**

  - MetaDefender NAC now supports certificate-based attributes from EAP-TLS authentication alongside existing endpoint attributes, giving you more granular control over network access policies.

## [1.9 MetaDefender NAC Cloud - 16 April, 2025](/docs/manac/nac-cloud/release-notes#19-metadefender-nac-cloud---16-april-2025)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- **Integration with My OPSWAT Central Management**: MetaDefender NAC is now embedded directly into My OPSWAT Central Management, providing a unified interface for all your security management needs.

## [1.8 MetaDefender NAC Cloud - 19 February, 2025](/docs/manac/nac-cloud/release-notes#18-metadefender-nac-cloud---19-february-2025)

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- Minor bug fixes & Enhancement.

## [1.7 MetaDefender NAC Cloud - 22 January, 2025](/docs/manac/nac-cloud/release-notes#17-metadefender-nac-cloud---22-january-2025)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- Administrators now have the ability to create custom Network Vendors with specific RADIUS vendor attributes. These custom Vendors can be utilized when setting up a RADIUS Client or assigning them to an Access Profile.

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- Minor bug fixes & Enhancement.

## [1.6 MetaDefender NAC Cloud - 18 December, 2024](/docs/manac/nac-cloud/release-notes#16-metadefender-nac-cloud---18-december-2024)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- Support new vendors for CloudNAC integration:

  - Ruckus
  - Meraki
  - AeroHive(Extreme)
  - Dell Switch N2024P

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- Minor bug fixes & Enhancement.
- Security improvements.

## [1.5 MetaDefender NAC Cloud - 20 November, 2024](/docs/manac/nac-cloud/release-notes#15-metadefender-nac-cloud---20-november-2024)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- Captive Portal - LDAP-based Authentication

  - MetaDefender NAC Cloud now supports LDAP-based authentication for captive portal login. Users can sign in to the network using their LDAP credentials, streamlining the authentication process for domain users. Administrators can easily configure an Active Directory (AD) server source to facilitate this authentication method.
- Radius Session View

  - Admins can now manage all current RADIUS sessions of devices connected to the network. This includes the ability to Re-Authenticate users by triggering a CoA (Change of Authorization) or Disconnect packet, which forces users to reconnect to the network.

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- Enhanced RADIUS Logs for Improved Troubleshooting

  - Logs now provide detailed insights, making it easier to trace network data.
- Enhanced Dashboard with Visual Auditing Charts.

## [1.4 MetaDefender NAC Cloud - 16 October, 2024](/docs/manac/nac-cloud/release-notes#14-metadefender-nac-cloud---16-october-2024)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- Multi-site deployment for NAC Edges

  - Administrators can now create multiple NAC Edge instances, providing the ability to manage multiple sites independently. Each site can be configured with different authentication methods, enabling greater flexibility and control across the network.
- CloudNAC OVA Release

  - CloudNAC is now available as an OVA (Open Virtualization Appliance), simplifying deployment by allowing quick installation in virtual environments with minimal configuration.

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- Various performance improvements and optimizations.
- Bug fixes to enhance stability and overall functionality.

## [1.3 MetaDefender NAC Cloud - 18 September, 2024](/docs/manac/nac-cloud/release-notes#13-metadefender-nac-cloud---18-september-2024)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- Guest Access Self Provisioning

  - Allow End user to register a guest account via Captive Portal (released as a feature flag).

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- Restructure RADIUS configuration UI.

## [1.2 MetaDefender NAC Cloud - 21 August, 2024](/docs/manac/nac-cloud/release-notes#12-metadefender-nac-cloud---21-august-2024)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- Device Enrollment

  - Introducing Device Enrollment feature targeting IoT and non-802.1X devices, ensuring they match specified conditions from RADIUS rules.
- EAP-PEAP Authentication

  - MetaDefender NAC Cloud now supports EAP-PEAP Authentication which enhances the security for authentication processes within Enterprise network environment.
- End-user SAML Single Sign-on (for Agent-less)

  - Enables captive-portal-based single sign-on against Okta or other SAML IdPs for devices with or without MD Endpoint.

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- RADIUS Rules: Add some extra conditions to check the device's compliant status.
- Fix an issue that NAC fails to detect devices with changes in Network adapters, resulting in incorrect VLAN assignment.
- Users can now switch between various authentication methods (EAP-PEAP, EAP-TLS, EAP-TTLS) or disable all to use MAB.

## [1.1 MetaDefender NAC Cloud - 17 July, 2024](/docs/manac/nac-cloud/release-notes#11-metadefender-nac-cloud---17-july-2024)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- RADIUS (802.1X) Username is now visible in MDITA console "Inventory" view and "Device Details" view.
- EAP-TTLS Authentication

  - CloudNAC integrations now support AD/LDAP based authentication, providing enhanced convenience and security (released as a feature flag).

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- Admin may now input CIDR ranges when creating "RADIUS Clients" and "Proxied RADIUS Clients".

## [1.0 MetaDefender NAC Cloud - 30 May, 2024](/docs/manac/nac-cloud/release-notes#10-metadefender-nac-cloud---30-may-2024)

#### [New features](/docs/manac/nac-cloud/release-notes#new-features)

- RADIUS capabilities

  - Support for MAB (MAC Address Bypass) authentication.
  - Support for EAP-TLS (certificate-based) authentication.
- Captive Portal capabilities

  - Support for MetaDefender Endpoint on-boarding for newly connected devices.
  - Support for remediation page redirection for non-compliant devices.

#### [Improvements and Enhancements](/docs/manac/nac-cloud/release-notes#improvements-and-enhancements)

- Security improvements.
