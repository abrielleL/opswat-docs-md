<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-7-26062-onprem -->

# Release Notes for v10.7.26062

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| **Version** | v10.7.26062 |
| --- | --- |
| **Release date** | July 10, 2026 |
| **Release Summary** | This release expands patch management with **ring-based deployment and customizable patch reports**, adds **MetaDefender Storage Security integration**, and brings **Kiosk Hardened Image upgrades** directly into My OPSWAT Central Management. Additional capabilities for On-Premises deployments include **Backup & Restore** for MetaDefender Endpoint and **Staged Module Rollout** for MetaDefender Core.  Alongside these capabilities, the left navigation menu has been revamped for simpler, more intuitive navigation. |

## [**Peripheral Media Protection Solution**](/docs/cm/release-notes/release-notes-for-v10-7-26062-onprem#peripheral-media-protection-solution)

**New Features** **Remote Hardened Image Upgrades for MetaDefender Kiosk**

Administrators can now remotely roll out and roll back **MetaDefender Kiosk Hardened Images** across individual devices or entire groups from a single console.

**Please note:** This feature is supported for MetaDefender Kiosk version 4.8.3 and later.

Refer to [Update Application](/docs/cm/product-management/update-application) guideline for more detailed instruction.

New Features  **Remote Script Execution Command on Kiosk Devices**

Trigger script execution command on managed Kiosk devices remotely from My OPSWAT Central Management, enabling centralized automation and maintenance without physical access to each Kiosk. Refer to our [Scheduled Remote Execution](/docs/cm/product-management/Scheduled-Remote-Execution) guideline for detailed instructions.

Enhancements **Enhanced "By Kiosks" Report Details**

By Kiosks reports now include additional detail fields

Enhancements**"Last Seen" Filter on Media Firewall Device List**

The Media Firewall device list now supports filtering by "Last Seen" activity, quickly surfacing inactive or active devices without scanning the full device inventory manually.

Bug Fixes **Server Errors Under High Request Volume**

Fixed an issue where My OPSWAT Central Management returned 502 and 499 errors when processing a high volume of concurrent requests.

Bug Fixes **Upgrade Job Rejection for Legacy Kiosk Hardened Images**

Fixed an issue where upgrade jobs were rejected for Kiosk devices running legacy hardened images.

## [Endpoint Security Solution](/docs/cm/release-notes/release-notes-for-v10-7-26062-onprem#endpoint-security-solution)

New Features **Backup & Restore for MetaDefender Endpoint**

Backup and restore for MetaDefender Endpoint can now be managed centrally through My OPSWAT Central Management, enabling fast recovery without manual reconfiguration.

**Please note**: This feature is available for MetaDefender Endpoint Windows Persistent v7.6.2607 and later.

Refer to [Backup & Restore](/docs/cm/endpoint-security-solution/backup---restore) documentation for further instructions.

New Features **Ring-Based Patch Deployment**

Patch deployment now supports ring-based rollout for both OS updates and third-party application patches, enabling controlled validation before production release.

New Features **Customized Patch Management Reports**

Customized patch reporting is available with flexible export formats, scheduled delivery, and visual dashboards.

Enhancements **Revamped Left Menu Navigation Menu**

The left navigation menu has been completely restructured to improve usability, surfacing only the controls relevant to your active environment, reducing navigation overhead and providing a cleaner management hierarchy.

Refer to our [Left Menu Revamped Announcement](/docs/cm/knowledge-base/Left-Menu-Revamped-v10-7-26062) for further details.

Enhancements **Restructured Endpoint Security Policy**

The Endpoint Security policy has been restructured into three distinct, purpose-built policies, including Endpoint Security, Download Protection, and Peripheral Media.

Refer to our [Policy Restructured guideline](/docs/cm/knowledge-base/Left-Menu-Revamped-v10-7-26062#policy-restructured) for breakdown of new policy structure.

Enhancements **Custom Information and Re-Identity Command for On-Demand Devices**

The "Re-Identity" command and "Custom Information" field are now supported for on-demand devices across Windows, macOS, iOS, and Android.

For minimum version supported and action availability across device types, refer to our [detailed documents](https://www.opswat.com/docs/cm/knowledge-base/why-can-t-i-apply-certain-actions-on-some-of-my-managed-devices-).

## [**OT and Cyber-Physical Systems Solution**](/docs/cm/release-notes/release-notes-for-v10-7-26062-onprem#ot-and-cyber-physical-systems-solution)

New Features **Support Upload Configuration Files for** **MetaDefender Industrial Firewall**

Admins can now upload, manage, and apply configuration files directly to MetaDefender Industrial Firewall instances managed through My OPSWAT Central Management.

## [Hardware Supply Chain](/docs/cm/release-notes/release-notes-for-v10-7-26062-onprem#hardware-supply-chain)

Bug Fixes **Engine Downloads for MetaDefender Drive**

Fixed an issue where MetaDefender Drive instances enrolled to an On-Premises deployment failed to download engine and database updates, returning a 404 error.

## [File Security Solution](/docs/cm/release-notes/release-notes-for-v10-7-26062-onprem#file-security-solution)

New Features **Staged Rollout for** **MetaDefender Core** **AV and Module Update Distribution**

AV and module updates distribution for MetaDefender Core now supports staged rollout, reducing the risk of untested updates reaching production.

Refer to [Staged Module Rollout](/docs/cm/file-security-solution/staged-module-rollout) guideline for detailed instructions.

New Features **MetaDefender Storage Security Integration**

My OPSWAT Central Management now supports integration with MetaDefender Storage Security, enabling **centralized enrollment, real-time health management, policy configurations, and license management** of Storage Security instances from a single console.

**Please note:** This feature is supported from MetaDefender Storage Security version 4.5.0 onward.

Enhancements **Improved Module Update Interface for MetaDefender Core**

The Module Update page has been redesigned for clearer navigation and a more consistent view of update state across MetaDefender Core instances.

Enhancements **"Number of Files" Column Added in File Processing History View**

The File Processing History view now includes a "Number of Files" column for each processing session.

Bug Fixes **Module Updates via UNC Path Not Applying**

Fixed an issue where importing module updates from a remote server via UNC path (\server\folder) did not work. Module updates from remote folders now function correctly.

Bug Fixes **MetaDefender Core Version Not Refreshing After Upgrade**

Fixed an issue where the MetaDefender Core version displayed in My OPSWAT Central Management was not updated after a successful upgrade on instances.

Bug Fixes **Deleted MD Core Instances Reappearing in All Services Tab**

Fixed an issue where deleted MetaDefender Core instances continued to appear in the All Services tab after a page refresh, despite the delete action appearing successful.

Bug Fixes **Configuration Not Showing for the First Enrolled Instance**

Fixed an issue where the first MetaDefender Storage Security (MDSS) instance enrolled in a fresh On-Premises environment stayed stuck on "The instance has not fully reported its configuration" and never displayed its configuration (vPack).

## [Network Access Control Solution](/docs/cm/release-notes/release-notes-for-v10-7-26062-onprem#network-access-control-solution)

New Features **FreeRADIUS Configuration Customization**

Administrators can now customize the FreeRADIUS configuration to fit advanced deployment requirements. Instead of replacing the entire template, you can upload specific customized files, and apply to FreeRADIUS.

New Features **Custom RADIUS Server Certificate Support**

Administrators can now bring their own custom RADIUS server certificates for greater trust and control. Custom certificates are preserved when the authentication mode changes, and their content is protected.

New Features **Custom Remediation Page per Rule**

A new rule action lets administrators assign a custom remediation page to specific rules, giving finer control over the end-user experience during remediation.

Enhancements **Add the Test connectivity option for EAP-PEAP authentication**

Administrators can now validate their EAP-PEAP configuration before saving. A new **Test connectivity and credentials** button confirms that NAC can reach the Active Directory domain and that the supplied credentials are valid, catching domain, credential, or DNS issues up front.

## [Additional Features](/docs/cm/release-notes/release-notes-for-v10-7-26062-onprem#additional-features)

**New Features** **OIDC Integration for Tenant Authentication**

My OPSWAT Central Management now supports OpenID Connect (OIDC) as an authentication method for tenant login. Refer to [OIDC SSO Integration Guide](/docs/cm/secure-access-solution/OIDC-SSO-Integration-Guide) for more detailed instruction.

New Features **Okta Identity Provider Provisioning**

Administrators can now configure Okta as an identity provider with full user provisioning support, enabling automatic synchronization of user access between Okta and My OPSWAT Central Management. Refer to [dedicated documentation](/docs/cm/user-management/ocm-account-provisioning-with-okta) for configuration details.

Enhancements **Enhanced Get Started Page with Guided Onboarding**

The redesigned Get Started page provides a structured onboarding guide and interactive navigation tour, helping administrators get familiar with the console faster from first login.

Enhancements **SSO Login No Longer Requires Email Verification for Accounts Without Mailboxes**

Email verification is no longer required for SSO accounts that are not associated with an invited My OPSWAT Central Management user.

Enhancements **Deployment ID Displayed During Offline License Activation**

The offline license activation dialog now shows the Deployment ID, making it easy to identify which instance a license key belongs to when managing multiple deployments.

Enhancements **Improved Installer Pre-Check Validation**

My OPSWAT Central Management installer now runs hardware and environment pre-checks before setup begins, surfacing warnings with clear remediation guidance.

##
