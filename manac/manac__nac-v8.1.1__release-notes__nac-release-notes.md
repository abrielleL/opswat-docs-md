<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/release-notes/nac-release-notes -->

# NAC Release Notes

## [8.2.0 MetaDefender NAC - 31 October, 2024](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#820-metadefender-nac---31-october-2024)

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- ⁠Win Policy key: 7155.216
- ⁠MAC Policy key: 8085.176

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- ⁠Added support for SAML authentication for NAC administrators
- Added support for captive portal advertisement using DHCP option 114 (Instructions [here](https://www.opswat.com/docs/manac/knowledge-base/how-to-configure-dhcp-option-114-on-dhcp-server))
- Added support for new RADIUS Attributes

  - Foundry-CoA-Command
  - ⁠HP-Port-Bounce-Host
  - ⁠HP-Captive-Portal-URL
  - ⁠HP-User-Role

#### [What's Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- Fixed inconsistent handling of HTTP traffic received over GRE tunnel interface vs regular interface
- Fixed bug in CoA-sending logic in cluster environments (introduced in 8.1.1)
- Fixed bug in RADIUS Accounting filtering logic when certain attributes are missing (introduced in 8.1.1)

## [8.1.1 MetaDefender NAC - 10 June, 2024](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#811-metadefender-nac---10-june-2024)

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- Windows Policy Key: 7155.216.
- Mac Policy Key: 8085.176.

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Optimized processing of RADIUS Accounting to better handle controller-less environments with high accounting rates

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- Fixed email validation during guest enrollment so that "Prohibited Email Domains" are checked using case-insensitivity.
- Fixed a bug that could prevent the NAC from sending enforcement updates to networking equipment after an update to the internal firewall.

## [8.1.0 MetaDefender NAC - 10 May, 2024](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#810-metadefender-nac---10-may-2024)

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- Windows Policy Key: 7155.216.
- Mac Policy Key: 8085.176.

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- New Logo updated.
- Change the product name from **MetaAccess NAC** to **MetaDefender** **NAC.**

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Web server security improvements.
- Optimized SNI-Proxy connection handling logic to avoid connection exhaustion in high-traffic environments

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- Blank Web UI on first login to the appliance.
- Fixed validation on email input fields that previously rejected some valid email addresses.

## [8.0.10 MetaAccess NAC - 17 May, 2023](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#8010-metaaccess-nac---17-may-2023)

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- Windows Policy Key: 7104.198
- Mac Policy Key: 8085.176

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Added support for sending email notifications when enforcement is enabled/disabled
- Settings necessary for setting up end-user SAML authentication are now exposed through the web console
- Improved accessibility of several pages to better conform with WCAG guidelines

## [8.0.9 MetaAccess NAC - 17 March, 202](https://docs.opswat.com/manac/release-notes/metaaccess-nac-release-notes#807-metaaccess-nac---10-january-2022)3

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- Windows Policy Key: 7104.198
- Mac Policy Key: 8085.176

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Web server security improvements
- Admins may now register multiple guest accounts with the same email (with a warning) provided username is unique

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- Fixed a bug where users who had been placed into the Temporary Access group would receive the FailedOpenAuth role after their temporary access expired if their normal group contained an LDAP authentication policy

## [8.0.8 MetaAccess NAC - 22 December, 2022](https://docs.opswat.com/manac/release-notes/metaaccess-nac-release-notes#807-metaaccess-nac---10-january-2022)

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- Windows Policy Key: 7104.198
- Mac Policy Key: 8085.176

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Remediated potential security issues in RADIUS server
- Added [SNI-based](https://en.wikipedia.org/wiki/Server_Name_Indication) HTTPS proxying:

  - External HTTPS resources can now be discriminately allowed for blocked clients based on FQDN directly, eliminating the need to maintain ever-shifting lists of allowed IPs. Contact your OPSWAT Support representative if you are interested in leveraging this feature.

## [8.0.7 MetaAccess NAC - 10 January, 2022](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#807-metaaccess-nac---10-january-2022)

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- Windows Policy Key: 7104.198
- Mac Policy Key: 8085.176

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Remediated Squid-related security issues
- Optimized Policy Key for Windows to prevent redundant communications
- Optimized RBE in CoA mode to prevent redundant CoA packets being sent to NASes
- Updated Policy Manager UI to allow spaces in AD role qualifies
- Updated RADIUS UI to include more info about supported certificate formats
- Update Contextual Intelligence UI to include CIDR-based filtering options

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- The "Verify" button in the Contextual Intelligence UI now handles TLS connections properly
- Fixed documentation links in various parts of the UI

## [8.0.6 MetaAccess NAC - 15 September, 2021](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#806-metaaccess-nac---15-september-2021)

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- Windows Policy Key: 7094.187
- Mac Policy Key: 8085.176

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Improve the firewall configuration to allow administrators to do ICMP monitoring over GRE tunnels to both Primary and Backup nodes in HA deployments
- Discontinue supporting weak/insecure algorithms:

  - Key-exchange:

    - diffie-hellman-group-exchange-sha1
    - diffie-hellman-group1-sha1
  - Ciphers:

    - blowfish-cbc
    - 3des-cbc
    - 3des-ctr
- Change wording on the “Enable” button in RADIUS configuration UI to prevent confusion

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- Fix a minor bug that prevented Policy Key version from showing under the application in Windows Apps & Features
- Update the link to download DHCP Syslog and AD Connector installers
- Allow Policy Key to be installed on new M1 Macs more seamlessly. *(Automatically grants brief temporary access to M1 Macs after the PK "Download" button is clicked so devices can install Rosetta if needed)*

## [8.0.5 MetaAccess NAC - 18 June, 2021](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#805-metaaccess-nac---18-june-2021)

#### [Agent Release Version:](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-release-version)

- Windows Policy Key: 7093.186
- Mac Policy Key: 8085.176

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- Added the ability to include/exclude specific IP subnets in Contextual Intelligence.

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Proxy Rule name now accepts only 0-9, a-z, and A-Z characters and maximum 255 characters. If an existing rule has special characters or more than 255 characters, you need to fix the rule name to able to save changes.
- Enhance security.

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- Policy Key detected SentinelOne Antivirus agent incorrect if a user upgraded SentinelOne Antivirus agent.
- Local home server pools in RBE configurations were duplicated if a MetaAccess NAC instance uses the proxy mode and is upgraded from a version 8.0.1 or earlier to a version 8.0.2/8.0.3/8.0.4.
- Administrators could not set end dates for guest users more than 1000 days from a created date.

## [8.0.4 MetaAccess NAC - 15 April, 2021](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#804-metaaccess-nac---15-april-2021)

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- Fixed a few bugs in the Policy Manager UI that may prevent users from setting custom enforcement options for anti-virus policies.

## [8.0.3 MetaAccess NAC - 1 April, 2021](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#803-metaaccess-nac---1-april-2021)

#### [Agent Version](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#agent-version)

- Windows Policy Key: 7092.184
- Mac Policy Key: 8085.176

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- Introduce the Clear-Role feature, which allows MetaAccess NAC to look for the changes of RADIUS attribute, identify whether the device has switched to another network and then assign the appropriate role.

#### [What Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#what-changedimproved)

- Upgrade to TLS version 1.2 and fix various security vulnerabilities
- Upgrade SSH library to support modern HMAC algorithms e.g: Ciphers, Host Key Algorithms, Key Exchange Algorithms, MAC Algorithms.

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- Prevent browser’s caching so customers do not have to clear cache to see the new UI

## [8.0.2 RC2 MetaAccess NAC - 1 February, 2021](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#802-rc2-metaaccess-nac---1-february-2021)

#### [What's New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- No new features for this hot fix

#### [What's Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- Optional capability to use newer HMA algorithm when connecting with SSH to routers/switches; in some cases the connection could not be made with the older library/algorithm. This must be enabled in napconf for this release, will become the default in the future.

## [8.0.2 MetaAccess NAC - 14 January, 2021](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#802-metaaccess-nac---14-january-2021)

#### [What's New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- Support for Dell OS 10 network device integration
- Added the ability to proxy RADIUS while also leveraging the MetaAccess NAC’s embedded RADIUS server, thereby permitting customers to, for example, use the embedded RADIUS server while also proxying requests to a service such as EDUROAM.

#### [What's Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- Alert the OPSWAT NAC admin by email if the NAC stops receiving updates from the AD Connector
- “Weekly Usage” report again displays ***Policies*** section
- “Device out of Compliance – Summary” report can be scheduled
- MAC Address ignore-list now will permit VPN interfaces to create client record
- Improved automated upgrade for macOS Policy Key
- Improve the validation of uploaded custom certificates

#### [What's Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- SAML SSO: fixed issues related to the option to “Generate Certificate” in the SAML -> Service Provider feature
- macOS Big Sur version is now displayed as 11.0 in Device Management Console

## [8.0.1 MetaAccess NAC - 10 November, 2020](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#801-metaaccess-nac---10-november-2020)

#### [Note](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#note)

- For a full summary of everything that has changed between version 7.0.1 and 8.0.1, see the 8.0.1 entry on the [Digest Release Notes](/docs/manac/nac-v8.1.1/release-notes/legacy-safeconnect-digest-release-notes) page.

#### [What's New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-2407 rebranding to OPSWAT language and styles
- PM-2406 Alcatel is now a supported layer 2 integration for RADIUS enforcement

#### [What's Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-2290 authorized devices may now use a MAC address prefix instead of listing large numbers of MAC addresses individually

#### [What's Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-1284 Policy Key MSI now supports silent installs correctly
- PM-2410 changing certain RADIUS configuration options no longer breaks the UI

## [7.0.8 - 28 September, 2020](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#708---28-september-2020)

#### [What's New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-2368 Support iOS 14
- PM-2367Support MacOS Big Sur (MacOS 11)
- PM-2356 Added a "Decline" link to the notification emails for device enrollment
- PM-2338 Add new NAS type for Extreme XOS (Wired)
- PM-1782 Add UI elements to reflect HA status
- PM-885 Allow proxying RADIUS accounting to an upstream home server

#### [What's Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-2359 Updated MacOS End of Life to account for MacOS devices running on 10.10-10.12 versions.
- PM-2189 Dual boot devices should now be identified by the OS they are booted on(Windows-Linux).

#### [What's Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-2402 Fixed an issue where changes to RADIUS mode would not remain if no change were made to the settings
- PM-2388 ADConnector Firewall UI rules we note applied to firewall configuration files

## [7.0.7 - 7/28/2020](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#707---7282020)

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-2322 Limit use of duplicate phone numbers for guest registration
- PM-2328 Generic AV policy based on Windows APIs - a device will be considered compliant if based on Windows Security they have AV installed, enabled, and up to date.

#### [What’s Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-2329 Changing from LDAP to LDAPS on an existing authentication policy will allow testing when using the option for default certificates
- PM-2324 SafeConnect now handles the COA disconnect message from Cisco 9800 controller
- PM-2326 New version of the weekly usage report does not include policy compliance data and offers better performance – customers that wish to maintain the old behavior, please contact OPSWAT Support. We will be re-enabling this in the future in a more performant fashion.
- PM-2295 Updated Ubiquiti COA handling to work better with open network.

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-2250 Improved files sync'ing between HA nodes
- PM-2340 Under some cases RADIUS log download failed in Firefox
- PM-2339 RADIUS log downloads not working as designed for date ranges
- PM-2323 Summary reports documents do not contain the detailed data shown in the preview

## [7.0.6 – 5/19/2020](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#706--5192020)

#### [What's New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-2299 Extreme Wireless has been added as a NAS type under RADIUS configuration.
- PM-2089 Purchased license count information is now available in the SafeConnect UI.

#### [What's Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-2300 The AD Connector has been revamped to adapt to newer Windows Server versions and leverage new code-level platform capabilities.
- PM-2257 HA customers will now be able to view information about the node state (Master/Backup) in the lower-left corner of the Console Networking Configuration screen.

#### [What's Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-2291 Subnet Mappings page not loading after qualifier container is deleted while being used by a group.
- PM-2281 Updated label name of the Contextual Identity module to correlate with the action taking when enabling/disabling this option.
- PM-2265 Resolve issue where enforcement in HA nodes could not be re-enabled after upgrade.

## [7.0.5 - 3/13/2020](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#705---3132020)

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-2252 Ubiquiti Wireless has been added as a NAS type under RADIUS configuration
- PM-2086 Mist-Juniper-Wireless has been added as a NAS type under RADIUS configuration
- PM-2272 Extreme- Identifi Wireless has been added as a NAS type under RADIUS configuration
- PM-2269 Dell OS6 has been added as a NAS type under RADIUS configuration

#### [What’s Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-2247 Updating the DNS server(s) inside the console configuration tool will no longer restart networking or any other services
- PM-2261 SafeConnect now allows for guests to be created more than 30 days in the future
- PM-2269 Dell NAS type in RADIUS configuration now supports COA
- PM-2282 New RBE roles no longer require VSAs to be populated for the corresponding role

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-2260 Home servers in RADIUS configuration are not listed in order based on their priority
- PM-2222 Substring based IP filters not working in Device Manager for some device views
- PM-2229 Slow LDAP connections can cause negative client and system behavior

## [7.0.4 – 2/20/2020](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#704--2202020)

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-1613 SAML web pages now support the full set of authentication use cases.
- PM-1374 Implemented an additional metric for SafeConnect to leverage in device identification, providing better detection of new clients.

#### [What’s Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-1498 To improve system efficiency, the weekly usage report is no longer able to be previewed.
- PM-2234 The configuration utility will now require an additional prompt when testing and changing network configurations beyond the initial setup.

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-2131 An edge condition where the primary database can encounter an unexpected state, resulting in a resync being required
- PM-1665 Advanced options are hidden when a guest has an expiration set to "Never Expire"

## [7.0.3 – 1/24/2020](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#703--1242020)

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-2211 Limited re-brand of SafeConnect NAC to reflect the OPSWAT acquisition
- PM-2214 Customers are now able to specify a custom email address for reports to get sent from.
- PM-1419 Enhanced device identification to allow for better matching of device fingerprints.
- PM-2192 New parser capability added for Palo Alto Threat Prevention Service.

#### [What’s Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-2205 Notification added to Subnet Mappings when a change to a subnet affects a pre-existing group.
- PM-2228 SafeConnect's Azure support was refreshed to ensure better support for Azure going forward.

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-2221 When multiple NAS IPs were listed for a client, SafeConnect encountered an issue tracking changes between them.
- PM-2197 Bulk uploading authorized devices failed after upgrades.
- PM-2208 Non-impacting issue in which SafeConnect attempted to listen for duplicate threat detection inputs.
- PM-2130 SafeConnect needed to be reloaded after an upgrade to allow for client enforcement.
- PM-1643 Enrolled devices had a device profile of Unknown rather than the enrolled device type.
- PM-1645 Some web messages, e.g. device enrollment forms, were unable to be previewed.
- PM-1823 Admin interface for device enrollment had inconsistencies between the fields for days and number of seconds.

## [7.0.2 – 11/20/2019](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#702--11202019)

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-2132 Customers are now able to leverage any subdomain of myweblogon.com as their hostname (e.g. impulse.myweblogon.com) for improved customer branding.

#### [What’s Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-2169 Included newest Mac OS PK.
- PM-1936 Updated bulk upload templates with improved grammar and proper field names.
- PM-1803 Updated SafeConnect to reflect proper browser compatibility changes.
- PM-1602 Increased the guest email address character limit to 255 characters when saved through the admin interface.
- PM-1434 Safeconnect no longer has to verify the reachability of custom hostnames.

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-2206 Fixed an issue where the Fortinet DHCP syslog parser did not handle certain input as expected.
- PM-2196 Fixed an issue where enforcement roles VSA names could not be saved if they contained a number.
- PM-2170 Fixed an issue where the RADIUS agent wouldn't start after an upgrade.
- PM-2144 Fixed an issue where Threat Enforcement could not be enabled through the UI.
- PM-1970 Fixed an issue in clusters where Policy Key devices could overload SafeConnect nodes with traffic.
- PM-1841 Fixed an issue where setting "Never" for temporary access caused negative end user behavior.
- PM-1592 Fixed an issue where spaces in Role Qualifiers were not parsed correctly.
- PM-1184 Fixed an issue where role names containing spaces caused errors during the enrollment process.

## [7.0.1 – 9/9/2019](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#701--992019)

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-1868 FireEye is now supported as a Threat Enforcement (IDS) source.
- PM-1272 UI session time outs will now be based on last activity, not login time.

#### [What’s Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-2036 The weekly usage report has been optimized for better performance.
- PM-2010 The Contextual Intelligence Publisher output now includes the "class" attribute required by a Fortigate system to be able to perform RADIUS SSO.
- PM-1998 The Contextual Intelligence Publisher will not allow invalid network configurations to be saved.
- PM-1975 Custom RADIUS certificates whose private key require a passphrase can now be uploaded via the UI.
- PM-1972 Add ability to use CIDR format for NAS-IP-Address RADIUS attribute in Policy Manager.
- PM-1381 The Block/Open Access note field will now present a helpful error when invalid characters are used. The textbox is limited to alpha numeric, typical punctuation, and white space.
- PM-2131 The synchronization process for HA environments is now improved.
- PM-2081/2024 Administrative UI webpages have received various security improvements.

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-2156 Role changes were not happening successfully due to the credentials used to connect to an internal database being improperly set.
- PM-2106 Under some situations, clicking "Apply and Use" in the RADIUS UI broke MAC Authentication Bypass.
- PM-2100 The RADIUS server would not be configured as expected after a migration.
- PM-2015 Under some situations, RADIUS server certificates which were uploaded through the UI were converted to the wrong format.
- PM-1995 RADIUS would not work with compound name attributes for LDAP group overrides.
- PM-1991 The "Last Updated User" field was not updated when editing a Block Access entry.
- PM-1990 Editing Block Access entries cleared the expiration date field.
- PM-1987 Policy Key devices would be incorrectly blocked for failing the NAT policy if they started a session with an IP which did not match the previous session's.
- PM-1950 The RBE UI showed the server's IP to be 127.0.0.1 instead of the actual IP of the node.
- PM-1849 The RADIUS log viewer where data would spin trying to load in some cases.
- PM-1120 The enrollment widget would not pop up as expected on the device details page.
- PM-1063 The MAC address displayed for a device in the Device Manager was not the MAC address of the device's active interface.
- PM-1000 Fixed an issue where an HA pair would join to an AD domain using the same NetBIOS name for both servers.
- PM-2042 Fixed an issue where in some cases devices which were failing anti-virus policies were shown the generic block page.

## [7.0.0 – 7/10/2019](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#700--7102019)

#### [What’s New](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-new)

- PM-1876 The Configuration Manager includes a help page which walks users through SafeConnect setup. – _Essentials tier only _
- PM-1767 RADIUS integrations now support LDAP based authentication. This removes the requirement of SafeConnect maintaining a persistent join connection to a single active directory server and better supports redundancy.
- PM-1763 Customers can now set their hostname to a subdomain of myweblogon.com (impulse-university.myweblogon.com). This removes the need for customers to get their own custom certificate as well as help with automated captive portal detection.
- PM-456 A new host type has been added for "Thin Client".

#### [What’s Changed/Improved](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-changedimproved)

- PM-1985 The "Routers and APs" host type qualifier is now included in the "Host Types for non-PK devices" qualifier set.
- PM-1875 RADIUS Configuration page has an updated look which makes set up simpler and more straightforward.

#### [What’s Fixed](/docs/manac/nac-v8.1.1/release-notes/nac-release-notes#whats-fixed)

- PM-1910 Fixed an issue where report related stored procedures took a long time to run, which in some cases would cause system impact.
- PM-1737 Fixed an issue where the " FailOpenAuthGroup" role was added to clients when devices which had authenticated with SAML switched groups.
- PM-1958 Fixed an issue where the menu on the top right of the SafeConnect UI would not store new user passwords which include special characters correctly.
