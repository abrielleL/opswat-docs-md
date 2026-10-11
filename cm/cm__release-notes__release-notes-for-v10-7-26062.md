<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-7-26062 -->

# Release Notes for v10.7.26062

| **Version** | v10.7.26062 |
| ---- | ---- |
| **Release date** | June 30, 2026 |
| **Release Summary** | This release expands patch management with **ring-based deployment and customizable patch reports**, adds **MetaDefender Storage Security integration**, and brings **Kiosk Hardened Image upgrades** directly into My OPSWAT Central Management. Alongside these capabilities, the left navigation menu has been revamped for simpler, more intuitive navigation. |

## **Peripheral Media Protection Solution**

New Features **Remote Hardened Image Upgrades for MetaDefender Kiosk**

Administrators can now remotely roll out and roll back **MetaDefender Kiosk Hardened Images** across individual devices or entire groups from a single console.

**Please note:** This feature is supported for MetaDefender Kiosk version 4.8.3 and later.

Refer to [Update Application](https://www.opswat.com/docs/cm/product-management/update-application) guideline for more detailed instruction.

![](https://uploads.developerhub.io/prod/97qW/eiaftg0o5bnautlkmqgk4t7k4h20y5bvf4v6grekb4jp9luwym1kpuv657nsd4cx.png)

New Features  **Remote Script Execution Command on Kiosk Devices**

Trigger script execution command on managed  Kiosk devices remotely from My OPSWAT Central Management, enabling centralized automation and maintenance without physical access to each Kiosk. Refer to our [Scheduled Remote Execution](https://www.opswat.com/docs/cm/product-management/Scheduled-Remote-Execution) guideline for detailed instructions.

![](https://uploads.developerhub.io/prod/97qW/h6ai1asj126w9duf6cnqzd228erchzqu6tki2teddfm1n4yui5tew1psgesupkh6.png)

Enhancements  **Enhanced "By Kiosks" Report Details**

By Kiosks reports now include additional detail fields to align with the reporting depth previously available in OCM v7, ensuring continuity for customers who have migrated to My OPSWAT Central Management.

![](https://uploads.developerhub.io/prod/97qW/5xvh1q7rzyfrqvycuzevfimxjyzndmgs9fw3bpvda0ff0axgqs1mos6i9s3kgvyn.png)

Enhancements**"Last Seen" Filter on Media Firewall Device List**

The Media Firewall device list now supports filtering by "Last Seen" activity, quickly surfacing inactive or active devices without scanning the full device inventory manually.

![](https://uploads.developerhub.io/prod/97qW/fv78lynh3pc1c18bp9j6b5i0k3b56j83wveb9pwizoz1vo3tqtsrfb9xiv8sar91.png)

Bug Fixes **Server Errors Under High Request Volume**

Fixed an issue where My OPSWAT Central Management returned 502 and 499 errors when processing a high volume of concurrent requests.

## Endpoint Security Solution

New Features **Ring-Based Patch Deployment**

Patch deployment now supports ring-based rollout for both OS updates and third-party application patches, enabling controlled validation before production release.

![](https://uploads.developerhub.io/prod/97qW/3odgg1t35l8vg3uwlextmq2ofqdto0nhan4t69j14p0eu0qwoj88jiypq1dsq8tr.png)

New Features **Customized Patch Management Reports**

Customized patch reporting is available with flexible export formats, scheduled delivery, and visual dashboards.

![](https://uploads.developerhub.io/prod/97qW/2g3t58lbvqc6byzg843gcha9dgnxfmn9pkq5ssrmqm5huoz3fje71u90tmta9zce.png)

Enhancements **Revamped Left Menu Navigation Menu**

The left navigation menu has been completely restructured to improve usability, surfacing only the controls relevant to your active environment, reducing navigation overhead and providing a cleaner management hierarchy.

Refer to our [Left Menu Revamped Announcement](https://www.opswat.com/docs/cm/knowledge-base/Left-Menu-Revamped-v10-7-26062) for further details.

![](https://uploads.developerhub.io/prod/97qW/oy6c99xx62klaaglb20sx714rxkgd6ku5zqv6993hp6ako301xkgnqxpb3z3oefk.png)

Enhancements **Restructured Endpoint Security Policy**

The Endpoint Security policy has been restructured into three distinct, purpose-built policies, including Endpoint Security, Download Protection, and Peripheral Media.

Refer to our [Policy Restructured guideline](https://www.opswat.com/docs/cm/knowledge-base/Left-Menu-Revamped-v10-7-26062#policy-restructured) for breakdown of new policy structure.

![](https://uploads.developerhub.io/prod/97qW/fmym4qf1i9g6nmomppix40t8xtmyxy5e0jfq85sm43xncrs3klj63s4scr5ir24v.png)

Enhancements **Custom Information and Re-Identity Command for On-Demand Devices**

The "Re-Identity" command and "Custom Information" field are now supported for on-demand devices across Windows, macOS, iOS, and Android.

For minimum version supported and action availability across device types, refer to our [detailed documents](https://www.opswat.com/docs/cm/knowledge-base/why-can-t-i-apply-certain-actions-on-some-of-my-managed-devices-).

![](https://uploads.developerhub.io/prod/97qW/4k0zfen0mzaj5qhi2hafgvlxggukz8tteapnu8yx73ll3d7afw66d6cfpuxvwux2.png)

## **OT and Cyber-Physical Systems Solution**

New Features **Support Upload Configuration Files for** **MetaDefender Industrial Firewall**

Admins can now upload, manage, and apply configuration files directly to MetaDefender Industrial Firewall instances managed through My OPSWAT Central Management.

![](https://uploads.developerhub.io/prod/97qW/thw384up9meai4rn059jjoq3nfe62qfedllih9hdbjep5ehl6nkw3gy798etczbt.png)

## File Security Solution

New Features **MetaDefender Storage Security Integration**

My OPSWAT Central Management now supports integration with MetaDefender Storage Security, enabling **centralized enrollment, real-time health management, policy configurations, and license management** of Storage Security instances from a single console.

**Please note:** This feature is supported from MetaDefender Storage Security version 4.5.0 onward.

![](https://uploads.developerhub.io/prod/97qW/2cjvg84gunvbektlvgfyrnb41wqk3mztm65051u7d1lxt3i2gp9yywi8jwbcxraz.png)

Enhancements **"Number of Files" Column Added in File Processing History View**

The File Processing History view now includes a "Number of Files" column for each processing session.

![](https://uploads.developerhub.io/prod/97qW/t56c5hlywmtdqr78o2kflbyi9z4988pv8vicqevuz06cm6dgakxos50fyl127qdd.png)

Bug Fixes **Module Updates via UNC Path Not Applying**

Fixed an issue where importing module updates from a remote server via UNC path (\server\folder) did not work. Module updates from remote folders now function correctly.

## Network Access Control Solution

New Features **FreeRADIUS Configuration Customization**

Administrators can now customize the FreeRADIUS configuration to fit advanced deployment requirements. Instead of replacing the entire template, you can upload specific customized files, and apply to FreeRADIUS.

![](https://uploads.developerhub.io/prod/97qW/vdcsn0d8re3gnxf74dq4xmhs4s4pjt0dtn70k3954cvc3gksymvhfgurstovss26.png)

New Features **Custom RADIUS Server Certificate Support**

Administrators can now bring their own custom RADIUS server certificates for greater trust and control. Custom certificates are preserved when the authentication mode changes, and their content is protected.

![](https://uploads.developerhub.io/prod/97qW/ci97jevrolufdxjhsjsg36ooaisfk4hjr753vd0iyxkn1n0l8sul7mhdckq01yt8.png)

New Features **Custom Remediation Page per Rule**

A new rule action lets administrators assign a custom remediation page to specific rules, giving finer control over the end-user experience during remediation.

![](https://uploads.developerhub.io/prod/97qW/vihfqx2o9bfm1ar5yqit6m9t7cha53pd14p6gkx0gwl5bi85ub15hxbpfu1kry3d.png)

Enhancements **Add the Test connectivity option for EAP-PEAP authentication**

Administrators can now validate their EAP-PEAP configuration before saving. A new **Test connectivity and credentials** button confirms that NAC can reach the Active Directory domain and that the supplied credentials are valid, catching domain, credential, or DNS issues up front.

![](https://uploads.developerhub.io/prod/97qW/clc5v63fts52c2app4iisaw1bsyg77je11g8k5qd7udmpc5vg0mpw8akkuiemdmk.png)

## Additional Features

New Features **OIDC Integration for Tenant Authentication**

My OPSWAT Central Management now supports OpenID Connect (OIDC) as an authentication method for tenant login. Refer to [OIDC SSO Integration Guide](https://www.opswat.com/docs/cm/secure-access-solution/OIDC-SSO-Integration-Guide) for more detailed instruction.

New Features **Okta Identity Provider Provisioning**

Administrators can now configure Okta as an identity provider with full user provisioning support, enabling automatic synchronization of user access between Okta and My OPSWAT Central Management. Refer to [dedicated documentation](https://www.opswat.com/docs/cm/user-management/ocm-account-provisioning-with-okta) for configuration details.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
