<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-2-2510 -->

# Release Notes for v10.2.2510

### Release Date: October 21, 2025

Version: v10.2.2510

**Peripheral Media Protection Solution**

- Introduced the ability to show or hide additional information in the Kiosk device list.

Added a new option to show or hide extended information in the Kiosk device list, allowing users to customize the level of detail based on operational needs.

![](https://uploads.developerhub.io/prod/97qW/cja8n6elnclyl2bvcd18zfbtqmnw4s4ba2jqmua0794inmyly0cmap19n986hk7g.png)

- Added an option to disable Peripheral Device Control.

Added a configuration toggle to disable Peripheral Device Control when needed, offering greater flexibility for environments where device control is not required.

![](https://uploads.developerhub.io/prod/97qW/j6d1gjygmem8i58pyj43e1iga8vhdwwx4dujprrr4ez5w1kcams2aablcux7kx1x.png)

**Endpoint Security Solution**

- Added the ability to disable all notifications for MetaDefender Endpoint.

Added the ability to disable all notifications from MetaDefender Endpoint, helping reduce noise and improve user experience in managed environments.

![](https://uploads.developerhub.io/prod/97qW/kkcmxorci86euu9ubjq165t7pn9k84yac801s9qmbto3ssm42p7bz13beobldhjl.png)

- Enabled remote reboot actions for persistent agents.

Enabled administrators to remotely trigger reboot actions for persistent agents, streamlining maintenance and troubleshooting across distributed endpoints.

![](https://uploads.developerhub.io/prod/97qW/wmppryq4sfxb1szw5ki1ssmpyscjbreujoo5402yh5s2p6m84r7405xx3appra3w.png)

- Added support to display the list of installed applications in Device Details.

Enhanced the Device Detail view to include a list of installed applications, providing deeper insight into endpoint software inventory for security and compliance checks.

![](https://uploads.developerhub.io/prod/97qW/0nhg8yrabtubabpj53rgqyb1xb8krlvbzgktoload3ih1ngt1r6wf99wpxf39kfs.png)

- Introduced a new Playbook action to move devices to a specific group based on CVSS score.

Introduced a Playbook automation that moves devices to specific groups based on their CVSS score, enabling dynamic risk-based response strategies.

![](https://uploads.developerhub.io/prod/97qW/0762z07skgzriyoaepkfc3cw17vwk0tvcwqc4tznm5qkk8662z0lhw4ntwxh9u8c.png)

- Enabled scheduled full system scans.

Introduced support for scheduling full system scans, allowing administrators to proactively detect threats at defined intervals.

![](https://uploads.developerhub.io/prod/97qW/mcgvfdygtz0ov6t6acwvlyugasbx90wxy49vgx5wkpqikoodho07nzl7dhirzdj4.png)

- Added tagging support for missing patches.

Implemented tagging functionality to identify and label missing patches, aiding in vulnerability tracking and remediation planning.

![](https://uploads.developerhub.io/prod/97qW/gjzjllc7vbtpzhtfdcuvcagt42dlmia7dht22vrz96pr6ywvo54jtbsgksah29ac.png)

- Displayed start and end times for device exemption periods.

Added the ability to display start and end times for device exemptions, improving auditability and policy enforcement transparency.

![](https://uploads.developerhub.io/prod/97qW/dg33vlutxmpin85fizaix05o8dyxtwdpxlpmtuqo7ngog5v7x78fr100bjx6smb7.png)

**File Security Solution**

- Introduced auto-sync options for MetaDefender File Transfer when using group policy.

Enabled automatic synchronization of MetaDefender File Transfer settings when using group policy, simplifying configuration management across large environments.

- Added ICAP Dashboard support.

Introduced a new ICAP Dashboard for centralized monitoring and analysis of ICAP traffic, helping administrators track performance and usage trends.

![](https://uploads.developerhub.io/prod/97qW/5gzgxy4dv85g8vxr1i8qwoqqrto85gbokmmzbi47dl1e7japh65hluzns5utft6n.png)

- Enhanced Processing History to show Core tags and Kiosk session IDs.

Updated the Processing History view to include Core tags and Kiosk session IDs, providing more context and traceability for scanned files.

![](https://uploads.developerhub.io/prod/97qW/cfmj96jxcwhurhk0954ssqu3kgcv1fx76k9aksh5ko366z7kupj7u1al41ietrk7.png)

**Secure Access Solution - NAC**

- Email Domain Restrictions for Guest Registration

Added a new option to restrict specific email domains from being used during guest registration, helping organizations enforce tighter access control policies.

- Improved RADIUS NAC Event Logging

Enhanced logging capabilities for RADIUS Network Access Control (NAC) events, providing better visibility and traceability for network authentication activities.

- Security Improvements

Implemented various security enhancements across the platform to strengthen system resilience and ensure compliance with best practices.

**Additional features**

- Ability to define a default role for SSO users.

Added the ability to define a default role for users authenticated via Single Sign-On, streamlining user provisioning and access control.

![](https://uploads.developerhub.io/prod/97qW/sgohqkkb3h3bwoxhtci5mwniw1frl6yox0vpgp9qx2phayjg7e63727e67acok3v.png)

- Added support for Google Cloud Platform log storage.

Introduced support for storing logs in Google Cloud Platform, expanding cloud integration options for centralized log management.

![](https://uploads.developerhub.io/prod/97qW/kgucxujdvzeixma5yicag0lhi2cedmucill52qysuue4fk2r6u8zusfv8h8ep4qn.png)

- Introduced OAuth API to retrieve the list of instances in inventory.

Added a new OAuth-secured API to retrieve the list of instances in inventory, enabling secure and scalable integration with external systems.

- Bug fixes and enhancements to improve user experience.
