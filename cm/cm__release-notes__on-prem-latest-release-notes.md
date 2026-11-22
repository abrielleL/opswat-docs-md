<!-- source: https://www.opswat.com/docs/cm/release-notes/on-prem-latest-release-notes -->

# On-Premise Release Notes

## My OPSWAT Central Management v10.8.26110.2845

| **Version** | v10.8.26110.2845 |
| ---- | ---- |
| **Release date** | Nov 20, 2026 |

Enhancements **Security Update: Nginx Upgraded to 1.31.9 to Address Critical Vulnerability**

The Nginx web server has been upgraded to version 1.31.9, resolving critical security vulnerability CVE-2026-123007 and enforces stricter request validation to protect your deployment from potential exploits.

| **Version** | **v10.8.26110** |
| ---- | ---- |
| **Release date** | Nov 17, 2026 |
| **Release Summary** | This release expands centralized management capabilities across supported products. **Secure Access **now supports fully air-gapped SDP deployments, while **Endpoint Security** adds application allowlisting and performance monitoring for macOS and Linux. **Peripheral Media Protection **introduces backup & restore for MetaDefender Kiosk, alongside remote reboot & shutdown controls. **Additional improvements** include centralized upgrade management, encrypted backups, and automated file transfer job management. |

### **Peripheral Media Protection Solution**

New Features **Back Up and Restore for MetaDefender Kiosk Configuration**

Administrators can now back up and restore MetaDefender Kiosk configurations, with password-protected backups, manual or scheduled jobs, and centralized view into job records.

Refer to [Backup & Restore for MetaDefender Kiosk](https://www.opswat.com/docs/cm/product-management/backup---restore-for-metadefender-kiosk) guideline for details.

![](https://uploads.developerhub.io/prod/97qW/b32mw07bhubngm3259yp0ahf66bz61674o93rlfmzvz97skcn9f5f132fui3vb8a.png)

New Features **Remote Reboot and Shut Down for MetaDefender Kiosk**

Remote reboot and shutdown are now supported for enrolled MetaDefender Kiosk devices **version 4.8.7 or later**.

Refer to [Remote Reboot and Shutdown](https://www.opswat.com/docs/cm/product-management/remote-reboot-and-shutdown) guidelines for more details.

![](https://uploads.developerhub.io/prod/97qW/w4vhe40ejt0gqy43lfzmcy6jioux3s7qj56ewz39i8mgos62088jpa1i4zqls7bv.png)

Enhancements **Support Additional Filters for Peripheral Media Protection Dashboard**

The Peripheral Media Protection dashboard now supports filtering by device type, location, device, and user, with additional option to exclude specific groups from the results.

Refer to [Peripheral Media Protection](https://www.opswat.com/docs/cm/product-management/peripheral-media-protection) guidelines for detailed instruction.

![](https://uploads.developerhub.io/prod/97qW/65nu6q0dc5ozrlg5glnh5xn5sfmgvpkh30q65oaybinnkcbet8maknlpjffesj26.png)

### **Endpoint Security Solution**

New Features** Approve Temporary End-User Access with Challenge-Response Codes**

Administrators can now generate challenge-response codes for MetaDefender Endpoint and MetaDefender Endpoint Validation to approve temporary access requests from end users.

![](https://uploads.developerhub.io/prod/97qW/8x9ec1qtsa1ziu0nvur56fklagktkqcxcr7ybnwtejxdk038y50e5ty76keo4x14.png)

New Features** Control Application Allowlisting and Blocklisting for Managed MetaDefender Endpoint**

Administrators can now configure application allowlists and blocklists for managed MetaDefender Endpoint devices, defining which applications are permitted or blocked from running.

![](https://uploads.developerhub.io/prod/97qW/133y51xhlobk558ttjuemujfkq6juu0e4rwd5cq73wmwuesiiuul0zqr694nnp58.png)

New Features **View Security Score for MetaDefender Endpoint**

A new Security Score data table helps administrators review score information for enrolled MetaDefender Endpoint.

![](https://uploads.developerhub.io/prod/97qW/yektom9bd4fdquvdum1x1r18nc48xz34yxrivokl8x44xmkl4au82jrxvs6y4g9z.png)

Enhancements **View Third-Party Applications by Installed or Not Installed Status**

Administrators can now view and filter third-party applications by installed or not installed status. Available on MetaDefender Endpoint Windows persistent agent version 7.6.2612 or later.

View [Third Party Applications](https://www.opswat.com/docs/cm/patch-management/patch-centric-third-party-applications) for more details.

![](https://uploads.developerhub.io/prod/97qW/n7f7rlebjdmrn1mq443ons3um3nsvb98r1i0zbo9sie9e2q5kwiizl3i4wmadr4h.png)

Enhancements** Manage Patch Settings and Events in One Place**

Administrators can now access patch settings and related events directly within the Patch Management solution, bringing patch configuration and event monitoring together in one place.

![](https://uploads.developerhub.io/prod/97qW/9p9v1t2up8xt59c59c7mzgrmiaystmnsglzpgkuqawqwm6yuumgxk5062waxtqqq.png)

Enhancements** Temporarily Exempt Devices from Compliance Checks**

Administrators can now exempt individual devices or device groups from compliance checks for a timed period.

![](https://uploads.developerhub.io/prod/97qW/slhe9zgcb90rfxemej6bi2lnjzqit87mfysrkbpm3bchbzxpbbb855t5uujkk4an.png)

Enhancements** Support** **Encrypt MetaDefender Endpoint Backups with a Passphrase**

Admins can turn on passphrase encryption when creating a backup job, adding a protection requirement when restoring backup data. Requires MetaDefender Endpoint **version 7.6.2611 or later**.

Refer to [Backup & Restore for MetaDefender Endpoint](https://www.opswat.com/docs/cm/endpoint-security-solution/backup---restore) guidelines for more details.

![](https://uploads.developerhub.io/prod/97qW/g6gcdv1tjjn68gw2ti7s05jr8yxg27svwd9znpoz8y256ipmng5qbxhf5nvxeh94.png)

Enhancements **Recognize Windows 10 with Extended Security Updates as a Supported OS**

Windows 10 22H2 devices covered by Extended Security Updates are now correctly recognized as running a supported operating system.

![](https://uploads.developerhub.io/prod/97qW/m90fb2ryom2r1inwogeem864gdrqoe0pgwzibc5j4wxdf30up2boahljnruqys8x.png)

Enhancements **Display Detected Applications in MetaDefender Endpoint Device Details**

Device Details page now displays both managed and unmanaged third-party applications detected on Windows endpoints.

![](https://uploads.developerhub.io/prod/97qW/359sgdy9aba3bmbt3qmvfzagf9k8d36mb4i0l5vchzf73q799955nqncpczscyuq.png)

Enhancements **Endpoint Performance Monitoring Now Supports macOS and Linux**

Endpoint performance monitoring now extends to devices running the MetaDefender Endpoint agent on macOS and Linux.

See [Endpoint Performance Monitoring](https://www.opswat.com/docs/cm/endpoint-security-solution/endpoint-performance-monitoring) for more details.

![](https://uploads.developerhub.io/prod/97qW/npffz7mf04gh3qwef6reuz1iqo2f26sfgv9ekx80yf1ejr29ylcm91rc6tstrvkp.png)

Enhancements**Display Only Patches Available in the Local Patch Repository**

Administrators can configure to view only patches available from the Local Patch Repository, so every listed patch is ready to deploy without checking upload status.

![](https://uploads.developerhub.io/prod/97qW/tnhg72evoph4plruc8l2v1vae9tdf7gqmnl1dd8s68707io9amfoawjtpcbvao5p.png)

Enhancements **Faster Server Response for Large MetaDefender Endpoint Deployments**

Reduce response times for On-Premises deployments with a large number of managed endpoints.

### **Portable Malware Scanning**

New Features **Track** **Quarantine Files in MetaDefender Drive In-Session Scan Reports**

Track and export quarantined file details directly from MetaDefender Drive in-session scan reports. 

![](https://uploads.developerhub.io/prod/97qW/2j1sjfg1krpyosyi8udwglhi31wxw4yxxbsqh1694s274zy9bwajio3c8b46cwvo.png)

### **File Security Solution**

New Features ** Centrally Manage MetaDefender Managed File Transfer Automated Jobs **

Administrators can now configure, trigger, and review MetaDefender Managed File Transfer automated jobs from one console.

Refer to [MetaDefender Managed File Transfer Automation Jobs](https://www.opswat.com/docs/cm/product-management/metadefender-managed-file-transfer-automation-jobs) guidelines for more details.

![](https://uploads.developerhub.io/prod/97qW/osnjrhaebkwvodz4w9sxwl2d94gjqgd2qgm6aeybmqeqrp7uw8yuowptnitxmn5x.png)

New Features **Remote Application Upgrade for MetaDefender ICAP Server**

Remotely roll out software upgrades for MetaDefender ICAP Server across individual device and group, reducing manual maintenance effort.

Refer to [Remote Application Update](https://www.opswat.com/docs/cm/product-management/application-update-overview) guidelines for more details.

![](https://uploads.developerhub.io/prod/97qW/61fvfnbi4xpf248abonc14i6zsl5rwk0wyd4u9gr2ga8oyzvl9uzrkp8c1c3l9sf.png)

Enhancements** Support Additional Filters for File Security Dashboard**

**Admins can view **scanned file counts alongside object counts on the MetaDefender Core dashboard, and filter processing metrics by individual instance on both MetaDefender Core and MetaDefender ICAP Server dashboards.

![](https://uploads.developerhub.io/prod/97qW/ti5ifcyvdhcnybsfa6wqbtkqaq7agx423snsv08luqhro8ti5wstpjanenqxw3ed.png)

Enhancements** Display New Engine Results in File Processing History**

File processing history details now display two new engine results:

1. **OPSWAT Alin AI Deflection**: show verdict banner and scan details in a dedicated tab.

![](https://uploads.developerhub.io/prod/97qW/nyva7dry38n8vv2hng0v12t9t5xeyb4gfch6mpy6lcnikuz6fhnwkkdmo494d9fd.png)

2. **OPSWAT Predictive Alin AI**: show verdict banner with scan results available under the Metascan™ tab.

![](https://uploads.developerhub.io/prod/97qW/7k3rdlrj0qr7e1is34ih8dzhaffol86bzfexh5v3kpr2lo6euysmow0hgi6bbent.png)

Bug Fixes **Correct “Last Updated” Sorting on MetaDefender Core Policy List**

Fixed an issue where sorting the “Last Updated” column on the MetaDefender Core policy list ordered policies by creation date instead of last updated date.

Bug Fixes **Correct Engine Download Links After Switching to Internet Mode**

Resolved an issue where switching your module update source from Manual/Folder to Internet mode caused newly downloaded engines to use incorrect URLs.

### Secure Access Solution

New Features **Fully on-premises SDP Support**

Integrate with on-premises SDP Controllers to centrally manage SDP gateways, access pools, and user policies in fully air-gapped environments.

![](https://uploads.developerhub.io/prod/97qW/77xvb1kgbesea8k6cblelbjygr987j2omrt7li3ur96m45y4dj8ijidgfyv7m244.png)

New Features **IPv6 Support for Protected Applications**

SDP now supports secure access to IPv6-only protected applications. Administrators can define protected applications by IPv6 address or prefix, and configure IPv6 on the gateway to reach them.

Refer to [Add Protected Applications](https://www.opswat.com/docs/cm/secure-access-solution/add-protected-applications) guidelines for more details.

![](https://uploads.developerhub.io/prod/97qW/7fj1celorc3am5hjamzv9zf6unri6ch8xi8empjuvkzlhup8y54riochw42sxdm2.png)

### **Additional Features**

New Features** Built-in Syslog Server and Proxy Support**

My OPSWAT Central Management now collects logs from managed products over UDP, TCP, or TLS and forwards them to external Syslog servers through a single profile.

![](https://uploads.developerhub.io/prod/97qW/vv43n6x7m8s2i0jo3d3fjtsedlt0j2pcbl7co0bf5j1uth72adeszddrn2dq9cts.png)

Enhancements **Redesigned Platform Interface**

The platform interface has been revamped to provide administrators with streamlined navigation and a consistent visual experience across product consoles.

![](https://uploads.developerhub.io/prod/97qW/r7vs147dn5b4ur7itdqti8xwd4oowwahtavtmzc6d8icr63skpsdgadevenw9jsv.png)

Enhancements** Improved Security User Management Module**

The Security User Management module now includes improvements to account handling, permission management, and system stability for more secure and reliable user administration.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
