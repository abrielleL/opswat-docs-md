<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/technical-requirements -->

# Technical Requirements

## [Infrastructure Requirements](/docs/manac/nac-v8.1.1/installation/technical-requirements#infrastructure-requirements)

## [Directory Server](/docs/manac/nac-v8.1.1/installation/technical-requirements#directory-server)

| **Requirements** | **Additional Information** |
| --- | --- |
| **LDAP** | LDAP compliant directory server |
| **MySQL** | v4.2 or higher User information stored in a single table:   - Username - Password - Group Membership - Expiration - Password encoding (if applicable) |
| **Secure LDAP** | - Public CA - Self-Signed Certificate - Copy of organizations Trusted Root Cert in PEM or Base64 format - Copies of other server certificates may also be needed |

## [DHCP Service](/docs/manac/nac-v8.1.1/installation/technical-requirements#dhcp-service)

| **Requirements** |  | **Additional Information** |
| --- | --- | --- |
| **Aruba** | Wireless Controllers |  |
| **Cisco**[**1**](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213385245/SafeConnect+Technical+Requirements#SafeConnectTechnicalRequirements-1) | Cisco, CiscoCatalyst, ASA |  |
| **Windows** | Server 2003 or higher | Windows Server 2003 or newer Requires installation of NAC DHCP Syslog Relay service Minimum 700 MB disk space |
| **Other** [**2**](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213385245/SafeConnect+Technical+Requirements#SafeConnectTechnicalRequirements-1) | Bluecat, Infoblox, Lucent, SonicWALL |  |

## [Domain Single Sign On (SSO)](/docs/manac/nac-v8.1.1/installation/technical-requirements#domain-single-sign-on-sso)

| **Requirements** |  |
| --- | --- |
| **Operating System** | Windows Vista or newer OSX 10.6 or newer[3](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213385245/SafeConnect+Technical+Requirements#SafeConnectTechnicalRequirements-1) |
| **Domain Managed** | Required |
| **Other** | Domain Controller IP’s and IP’s necessary for login scripts must be exempted from NAC policy enforcement |

## [RADIUS Single Sign On (SSO)](/docs/manac/nac-v8.1.1/installation/technical-requirements#radius-single-sign-on-sso)

| **Requirements** |  | **Additional Information** |
| --- | --- | --- |
| **RADIUS Accounting** | Required |  |
| **RADIUS Authentication** | User Account Based |  |
| **RADIUS Controller** | Required | NAC Appliance will need IP address(es) and shared secret are required to be configured |

## [SAML Single Sign On (SSO)](/docs/manac/nac-v8.1.1/installation/technical-requirements#saml-single-sign-on-sso)

| Requirements |  | Additional Information |
| --- | --- | --- |
| Google | Google Apps for Business/Education | More Information: <https://support.google.com/a/answer/6087519?hl=en&ref_topic=6304963> |
| Azure AD | Azure AD Premium | More Information: <https://azure.microsoft.com/en-us/documentation/articles/active-directory-saas-custom-apps/> |
| Duo Two-Factor | Duo Access Gateway | More Information: <https://duo.com/docs/dag#add-a-cloud-application-to-duo-access-gateway> |
| Okta |  | More Information: <http://developer.okta.com/standards/SAML/setting_up_a_saml_application_in_okta> |
| OneLogin |  | More Information: <https://support.onelogin.com/hc/en-us/articles/202673944-How-to-Use-the-OneLogin-SAML-Test-Connector> |
| Dell One Identity Cloud Access Manager |  | More Information: <http://documents.software.dell.com/dell-one-identity-cloud-access-manager/8.1.1/configuration-guide/adding-a-web-application/saml-federation> |
| Gluu |  | More Information: <https://www.gluu.org/docs/integrate/outbound-saml/> |
| Other |  | Must Support SAML 2.0 |

## [Virtual Enforcer System Requirements](/docs/manac/nac-v8.1.1/installation/technical-requirements#virtual-enforcer-system-requirements)

### [VMWare vSphere](/docs/manac/nac-v8.1.1/installation/technical-requirements#vmware-vsphere)

#### [Large Standalone Appliance or Manager for a cluster (Up to 25,000 concurrent devices)](/docs/manac/nac-v8.1.1/installation/technical-requirements#large-standalone-appliance-or-manager-for-a-cluster-up-to-25000-concurrent-devices)

| **Appliance Specifications** | **NAC VMWare Enforcer** |
| --- | --- |
| **VMWare Version** | ESXi 5.1 or newer |
| **Virtual Hardware Version** | Minimum version 8 |
| **CPU** | 16 vCPUs (2-3Ghz) |
| **Memory** | 32 GB Minimum |
| **Hard Drive Storage** | 500 GB Minimum |
| **Appliance Scalability** | Up to 25,000 Devices |
| **Network Interface** | Gigabit NIC |

#### [Small Standalone Appliance or Enforcer in a cluster (Up to 10,000 concurrent devices)](/docs/manac/nac-v8.1.1/installation/technical-requirements#small-standalone-appliance-or-enforcer-in-a-cluster-up-to-10000-concurrent-devices)

| **Appliance Specifications** | **NAC VMWare Enforcer** |
| --- | --- |
| **VMWare Version** | ESXi 5.1 or newer |
| **Virtual Hardware Version** | Minimum version 8 |
| **CPU** | 8 vCPUs (2-3Ghz) |
| **Memory** | 16 GB Minimum |
| **Hard Drive Storage** | 300 GB Minimum |
| **Appliance Scalability** | Up to 10,000 Devices |
| **Network Interface** | Gigabit NIC |

### [VMWare Cluster](/docs/manac/nac-v8.1.1/installation/technical-requirements#vmware-cluster)

| **Appliance Specifications** | **NAC VMWare Policy Enforcer** | **VMWare Policy Manager** |
| --- | --- | --- |
| **VMWare Version** | ESXi 5.1 or higher | ESXi 5.1 or higher |
| **Virtual Hardware Version** | Version 8 or higher | Version 8 or higher |
| **CPU** | 4 vCPUs (2-3Ghz)[4](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213385245/SafeConnect+Technical+Requirements#SafeConnectTechnicalRequirements-4) | 8 vCPUs (2-3Ghz) |
| **Memory** | 16 GB Minimum[5](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213385245/SafeConnect+Technical+Requirements#SafeConnectTechnicalRequirements-1) | 16 GB Minimum[5](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213385245/SafeConnect+Technical+Requirements#SafeConnectTechnicalRequirements-1) |
| **Hard Drive Storage** | 300 GB Minimum[6](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213385245/SafeConnect+Technical+Requirements#SafeConnectTechnicalRequirements-6) | 300 GB Minimum[6](https://impulsepoint.atlassian.net/wiki/spaces/CK/pages/213385245/SafeConnect+Technical+Requirements#SafeConnectTechnicalRequirements-1) |
| **Appliance Scalability** | 25,000 (per Enforcer/Manager) |  |
| **Network Interface** | Gigabit NIC |  |

## [Microsoft Hyper-V](/docs/manac/nac-v8.1.1/installation/technical-requirements#microsoft-hyper-v)

### [Standalone Appliance](/docs/manac/nac-v8.1.1/installation/technical-requirements#standalone-appliance)

| **Appliance Specifications** | **NAC Hyper-V Enforcer** |
| --- | --- |
| **Server** | Microsoft Server 2012 R2 |
| **Hyper-V Version** | Hypervisor Generation 2 |
| **CPU** | 4 vCPUs (2-3Ghz) |
| **Memory** | 16 GB Minimum |
| **Hard Drive Storage** | 300 GB Minimum |
| **Appliance Scalability** | Up to 10,000 Devices |
| **Network Interface** | Gigabit NIC |

## [End User Device Requirements](/docs/manac/nac-v8.1.1/installation/technical-requirements#end-user-device-requirements)

## [Policy Key System Requirements](/docs/manac/nac-v8.1.1/installation/technical-requirements#policy-key-system-requirements)

### [Microsoft Windows](/docs/manac/nac-v8.1.1/installation/technical-requirements#microsoft-windows)

| **Device Requirements** |  |
| --- | --- |
| **Operating System** | Windows Vista or newer |
| **Service Pack** | NA |
| **Memory** | 1 GB |
| **CPU** | Single Core 1.6Ghz |
| **Hard Drive Storage** | 100 MB |
| **Administrative Rights** | No |

### [Mac OS X](/docs/manac/nac-v8.1.1/installation/technical-requirements#mac-os-x)

| **Device Requirements** |  |
| --- | --- |
| **Operating System** | 10.6 or newer |
| **Memory** | 1 GB |
| **CPU** | Single Core 1.6Ghz |
| **Hard Drive Storage** | 100 MB |
| **Administrative Rights** | Yes (for installation only) |

## [Web Browser Support](/docs/manac/nac-v8.1.1/installation/technical-requirements#web-browser-support)

## [Microsoft Windows](/docs/manac/nac-v8.1.1/installation/technical-requirements#microsoft-windows)

| **Device Requirements** |  |
| --- | --- |
| **Internet Explorer** | v9+ |
| **Mozilla Firefox** | v35+ |
| **Google Chrome** | v40+ |

## [Mac OS X](/docs/manac/nac-v8.1.1/installation/technical-requirements#mac-os-x)

| **Device Requirements** |  |
| --- | --- |
| **Safari** | v6.1.6+ |
| **Mozilla Firefox** | v35+ |
| **Google Chrome** | v40+ |

## [Secure BYOD Onboarding System Requirements](/docs/manac/nac-v8.1.1/installation/technical-requirements#secure-byod-onboarding-system-requirements)

| **Requirements** | **Version** | **Additional Information** |
| --- | --- | --- |
| **Android** | 2.1 or newer |  |
| **Blackberry** | NA | Does not support Secure BYOD Onboarding but step by step instructions available |
| **ChromeOS** | Any |  |
| **iOS** | v4.0 or newer |  |
| **Linux** | Most major platforms | Requires Python |
| **Mac OS X** | OS X 10.5 or newer | OS X 10.4 does not support Secure BYOD Onboarding but step by step instructions available |
| **Nokia** | NA | Does not support Secure BYOD Onboarding but step by step instructions available |
| **Windows** | Windows XP or newer | Windows RT is also supported |
| **Windows Phone/ Windows Mobile** | NA | Does not support Secure BYOD Onboarding but step by step instructions available |

## [Network Integration Requirements](/docs/manac/nac-v8.1.1/installation/technical-requirements#network-integration-requirements)

## [Layer 2 Wired Integration Switch Support](/docs/manac/nac-v8.1.1/installation/technical-requirements#layer-2-wired-integration-switch-support)

| **Function/Feature** | **Switch Requirement** |
| --- | --- |
| **802.1X Authentication (supplicant)** | 802.1X |
| **MAC Authentication (no supplicant)** | 802.1X, MAB |
| **MAC Authentication (no supplicant) with Identity** | 802.1X, MAB, COA, Redirect-URL or VLAN Assignment plus upstream Layer3 Redirect/PBR |
| **Layer2 Network Access Assignment** | 802.1X, MAB, COA, Filter/VSA or VLAN Assignment |
| **Layer2 Network Access Quarantine** | 802.1X, MAB, COA, Redirect-URL or VLAN Assignment plus upstream Layer3 Redirect/PBR |

## [Vendor Support](/docs/manac/nac-v8.1.1/installation/technical-requirements#vendor-support)

| **Layer 2 Wireless** |  |
| --- | --- |
| Vendor | OS/Firmware Requirements |
| Aerohive | HM-6 - HiveManager HiveOS 6.4.r1, 6.6.r3 or higher, AP HiveOS 6.4r1, 6.5.r3, 6.6.r2 or higher HM-NG - HiveManager HiveManagerNG 11.13 or higher, AP HiveOS 6.5.r5 or higher |
| Cisco | AireOS - 7.2 or later IOS-XE (Catalyst 9800 VM) - tested on 16.12.2s |
| Extreme | Identifi - Tested on V2110 VM controller 10.41.02.0014 WiNG - Tested on VX9000 VM controller 5.9.7.0-011R |
| HPE-Aruba | ArubaOS 6.1.3.4 or later (Instant) - InstantOS 6.4.0.2-4.1 or later |
| Juniper-Mist | Certified on AP version 0.6.18694 |
| Meraki | Certified on beta build (July 2016) |
| Ruckus | ZoneDirector - 9.10 or later SmartZone - |
| Ubiquiti | Unifi - Cloudkey (controller) - Unifi 5.12.35, AP Unifi 4.3.20.11298 |
| Xirrus | Xirrus - APs connected to XMS-Cloud |
| Other | Contact OPSWAT Support |
| **Layer 2 Wired** |  |
| **Vendor** | **OS/Firmware Requirements** |
| Aruba | ArubaOS - tested on ArubaOS 7.4.1.7 ArubaOS-Switch - tested on WC.16.10.0002 |
| Cisco | LAN base or better (i.e. not LAN Lite) |
| Dell | N-Series - OS6 6.2.0.5 or later S-Series - OS9 9.13 or later |
| Extreme | Summit Gen1 - tested on ExtremeXOS 30.6.1-Patch1-11 |
| Juniper | EX Series switches - 15.1R3 or later |
| Meraki | Certified on MS 11.31 |
| Ruckus/Arris | ICX - 8.0.20 or later |
| Other | Contact OPSWAT Support |
| **Layer 3 Wired** |  |
| **Vendor** | **OS/Firmware Requirements** |
| Alcatel-Lucent | 6850/6900 - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) 9700 - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) |
| Brocade/Ruckus/Arris | ICX - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) |
| Brocade/Extreme | MLX - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) |
| Cisco | Catalyst - (IOS) - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) Catalyst - (IOS-XE) - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) Nexus - (NX-OS) - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) |
| Dell | N-Series/OS6 - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) S-Series/OS9 - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) |
| HP | 3800 - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) 5400/8200 - Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) |
| Other | Contact OPSWAT Support |

## [Wireless Integration Support](/docs/manac/nac-v8.1.1/installation/technical-requirements#wireless-integration-support)

| **Function/Feature** | **Switch Requirement** |
| --- | --- |
| **Hardware** | Aerohive, Aruba, Cisco, Cisco Meraki, Ruckus, Xirrus, Other - Contact OPSWAT Support |
| **Minimum Version** | Aruba Wireless Controller 6.3 or later, Cisco Wireless Controller 7.2, or later Cisco Meraki AP’s firmware (July 2016 or Later), HiveManager 6.4.r1, or later HiveManager NG Ruckus ZoneDirector 9.13 preferred (9.10 or later supported), Ruckus Cloud Managed Wi-Fi Xirrus Cloud Management System |
| **Controller Modes** | Aerohive HiveManager 6 Enterprise Mode, HiveManager NG, Aruba – Policy Enforcement Firewall (PEF) License, Cisco – Central Switching, Cisco Meraki, Ruckus, Ruckus AP’s connected to Cloud Managed Wi-Fi, Xirrus AP’s connected to the Xirrus Cloud Management System |

## [Layer3 Integration Switch/Router Support](/docs/manac/nac-v8.1.1/installation/technical-requirements#layer3-integration-switchrouter-support)

| **Function/Feature** | **Switch Requirement** |
| --- | --- |
| **Layer3 Authentication and Enforcement/Quarantine** | Platform, license and OS image must support sFlow or Netflow and Policy-Based Routing (PBR) |

## [Contextual Intelligence Publisher](/docs/manac/nac-v8.1.1/installation/technical-requirements#contextual-intelligence-publisher)

| **Requirements** | **Version** |  |
| --- | --- | --- |
| **Exinda** | v6.0 or higher |  |
| **iBoss** | v6.0 or higher |  |
| **Palo Alto** | v5.0 or higher |  |
| **Procera** |  |  |
| **SonicWALL** | v6.0 or higher |  |
| **Syslog** | Any | Must support LEEF, CEF or Key-Value Format |
| **RADIUS Accounting** | NA |  |

## [Notes](/docs/manac/nac-v8.1.1/installation/technical-requirements#notes)

Note

1 – Cisco Wireless Controllers are NOT supported

2 – Other environments may be supported, provided the syslog output is comparable to one of the supported environments.

3 – AD Connecter is required for OSX Single Sign On

4 – VMWare Dedicated CPU resource is required

5 – VMWare Dedicated Memory resources are required

6 – VMWare Dedicated 300GB of storage required

7 – Dedicated CPU resource is required

8 – Dedicated Memory resources are required

9 – Dedicated 300GB of storage required

10 – All features require RADIUS Accounting

11 – Full RBE requires user traffic be switched by the controller, VLAN assignment only is available with local switching

12 – Maximum capacity will vary based on PBR CAM table size, CPU utilization and other factors

13 – PBR on HP chassis models mandate only v2 modules be installed, PBR with v1 modules installed is not supported

14 – Some Cisco switches may require specific modules to support Netflow, refer to manufacturer’s documentation

15 – Most Aerohive Access Points require HiveOS 6.5r4. For specifics on your Access Point requirements please contact OPSWAT

16 – VLAN assignment using Aerohive User Profiles is not supported, please contact OPSWAT Support with any questions

17 – Aruba Instant AP’s do not require PEF license

18 – Flexible Authentication Required

19 – Cisco Meraki July 2016 Firmware with NAC Authentication (External Auth)

20 – Layer 3 Required for PBR
