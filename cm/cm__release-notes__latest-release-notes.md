<!-- source: https://www.opswat.com/docs/cm/release-notes/latest-release-notes -->

# SaaS Release Notes

| **Version** | v10.7.26092 |
| ---- | ---- |
| **Release date** | September 29, 2026 |
| **Release Summary** | This release strengthens **file security **with the new **File Audit Trail**, which traces a file's full journey in a single view. **Endpoint & Patch Management** expands patch control with **Dell and Lenovo driver & firmware updates**, **pre- and post-deployment automation scripts**, and **real-time performance monitoring & alerting**. Remote product management and visibility extend with quarantined file retrieval for MetaDefender Core, reboot and shutdown for MetaDefender Industrial Firewall devices, and installed applications visibility for MetaDefender Drive scanned-host records.  |

## Peripheral Media Protection Solution

New Features **Support Automatic Direction-Based Workflow for Peripheral Media Protection**

Peripheral Media Protection now automatically applies the right scan workflow based on file transfer direction.

![](https://uploads.developerhub.io/prod/97qW/epwcun48p1dcypxwh82s31bad31valua36brrcxc6qbnv66jyuupc7ql0mx6ok4m.png)

New Features** One-Time PIN Verification for Restricted MetaDefender Kiosk Workflows**

Administrators can generate one-time PINs that grant end users temporary access to restricted MetaDefender Kiosk workflows.

![](https://uploads.developerhub.io/prod/97qW/gtswnyfqf8nh7ujg1ub9qd1rctqt5tkz51cg68qhnazs5xzpmmbn3oj0p0zqar4v.png)

New Features** On-Access File Scanning Protection Mode Configuration for macOS**

Administrators can now configure On-Access File Scanning for macOS endpoints within Peripheral Media Protection policies.

![](https://uploads.developerhub.io/prod/97qW/i08iums3yj8qul8djpuh7ro6xmf3nmz6c9wt6m02asmz83irnoh0vx57i0ni7jkb.png)

Enhancements** Added "Allowed and Blocked Media by Group" Widgets to Peripheral Media Protection Dashboard**

The Peripheral Media Protection dashboard now includes dedicated widgets showing allowed and blocked removable media activity grouped by device groups.

Refer to [Peripheral Media Protection](https://www.opswat.com/docs/cm/product-management/peripheral-media-protection) for more details.

![](https://uploads.developerhub.io/prod/97qW/13vboh9hocrvwxfxditbxwyaj3b2mjwjfwi6f4s5myh8mz7zsbls2s3x8tpis2j3.png)

## Endpoint Security Solution

New Features **Patch Management Now Supports Driver and Firmware Updates**

Administrators can now detect outdated drivers, firmware, and BIOS on Dell and Lenovo Windows devices and deploy OEM vendor updates directly through on-demand, policy, and ring deployments.

Refer to [Driver & Firmware Updates](https://www.opswat.com/docs/cm/patch-management/driver---firmware-settings-on-endpoint) for more details.

![](https://uploads.developerhub.io/prod/97qW/ybcsv0de0v7mlf1o90msa5e69dvm85hgyoo0sfztds5e1n1igsuupzapna7mxolx.png)

New Features** Automation Scripts Now Available for On-Demand Patch Deployments**

Administrators can execute custom pre- and post-deployment scripts during on-demand updates (e.g., stopping services, taking backups, or verifying application health post-install).

Refer to [Deployment Scripts](https://www.opswat.com/docs/cm/patch-management/deployment-scripts) guidelines.

![](https://uploads.developerhub.io/prod/97qW/ityugyi863x87wcmlllkmqbsp4l66jc774ihlo4tbzxqitwtmk8hc9mai0prhs9g.png)

New Features **Real-Time Endpoint Performance Monitoring and Incident Alerts**

Administrators can monitor critical endpoint metrics from a single view, including CPU, memory, disk, and network usage, with configurable thresholds and automated alerts for high resource usage.

Refer to [Endpoint Performance Monitoring](https://www.opswat.com/docs/cm/endpoint-security-solution/endpoint-performance-monitoring) guidelines for more details.

![](https://uploads.developerhub.io/prod/97qW/aza92yrknvbfporfd5uv6i372jxuyy41v02v6mn9g7m6znn2dqolte19beteq4zs.png)

Enhancements **Handle Ubuntu Phased Updates in Patch Compliance**

Patch compliance reporting now accounts for Ubuntu phased updates, eliminating false-positive non-compliance alerts for devices not yet eligible for phased rollouts.

![](https://uploads.developerhub.io/prod/97qW/5wm0p52v88j0gtibithtcebvahomq47ui2m3apsjnl4japn24t117gd2fiqidgg4.png)

## Portable Malware Scanning

New Features** Installed Applications Visibility on MetaDefender Drive Scanned Hosts**

Scanned host records now list the installed applications detected by MetaDefender Drive, including application name, version, publisher, install date, and install location.

![](https://uploads.developerhub.io/prod/97qW/svofk6m0egcamszd1pvsaftr4js8q3yncbyr41w6sb042vs9muykhv0ssdo8en9t.png)

New Features **Show License Details for MetaDefender Drive**

Administrators can now view license details for managed MetaDefender Drive devices, including license status and expiration dates.

![](https://uploads.developerhub.io/prod/97qW/ih2lnttun3k6292qdhtu146584th9oadbrwnomy8bqkq0mttd7kq9zjhbp6av5n5.png)

## OT and Cyber-Physical Systems Solution

New Features** Remote Reboot and Shut Down for MetaDefender Industrial Firewall**

Administrators can remotely reboot or shut down MetaDefender Industrial Firewall devices from the console, eliminating the need for manual, on-site intervention.

**Please Note**: This feature is supported for MetaDefender Industrial Firewall version 3.5.1 or later.

![](https://uploads.developerhub.io/prod/97qW/d41biee4qnbc94v3dxbr9df295vi9yt15o0iudttw70mtr2fajfu58gbo54h1fde.png)

Enhancements** Support Toolkit Upgrade for MetaDefender Industrial Firewall**

Support OPSWAT Industrial OS platform and Toolkit upgrade for MetaDefender Industrial Firewall. Refer to [Update Application](https://www.opswat.com/docs/cm/product-management/update-application) guideline for more details.

![](https://uploads.developerhub.io/prod/97qW/8lpjrvh8pagq3zrdd4oe4hb75x4w6nlzrvaqu451jmpk2v29z5reziu08lewnbht.png)

## File Security Solution

New Features **End-to-End File Audit Trail**

File Audit Trail gives administrators one centralized view of a file's full journey, displaying each product that handled it, detailing scan outcome, processing timestamps, and file alterations.

Refer to [File Audit Trail](https://www.opswat.com/docs/cm/product-management/File-Audit-Trail) guidelines for more details.

![](https://uploads.developerhub.io/prod/97qW/2ztxcg4tpzukcz48e0owzdito4yk49yiyom5u60ccy70n18urgl4q96mgg1szq6z.png)

New Features **Retrieve Quarantine Files from MetaDefender Core**

Administrators can now view and remotely retrieve quarantined files from MetaDefender Core from centralized console. Administrators can also mark files as protected to prevent automatic cleanup.

See [Quarantined Files](https://www.opswat.com/docs/cm/product-management/quarantined-files) guidelines for detailed instructions.

![](https://uploads.developerhub.io/prod/97qW/17v4lb4obqnryx5weirijj4eu6fsjkk610rzpoe0bv2v5nwcn43bcsjtmfrals3f.png)

New Features** Centralized Password Storage Management for MetaDefender Core**

Password Storage entries can now be created, edited, and deleted in one central place and synced out to every managed MetaDefender Core instance.

Refer to [Password Storage](https://www.opswat.com/docs/cm/product-management/password-storage) for detailed instruction.

![](https://uploads.developerhub.io/prod/97qW/kpfeepg3jv9j07h24hmloyt01y94g14k8y8swicwsadp682rdgro0izsne1cu5kp.png)

## Network Access Control solution

New Features **Hyper-V Appliance Image**

NAC Edge is now available as a Hyper-V image. The NAC Edge Deployment page offers a Download. VHDX button alongside the existing OVA and QCOW2 images, with the version number and MD5 checksum shown beneath it so you can verify the download.

![](https://uploads.developerhub.io/prod/97qW/5dgv2nha06mnddhnturc0fw9jqvpdlt0pgmtv9bggmyf9nwqgnuw5d7v9uzhej9q.png)

New Features **Suffix Validation for EAP-PEAP**

EAP-PEAP configuration now offers optional suffix validation. Previously a domain user name such as [user@example.com](mailto:user@example.com) had its suffix removed and only the user name was authenticated. With suffix validation enabled, sign-in attempts presenting an unexpected domain suffix are rejected.

![](https://uploads.developerhub.io/prod/97qW/w40mz656ftdp40rgu2f8ee6wcx6e95fz8h8do3f0n6cjgihd1af1pl8ekc8uhnqm.png)

New Features** Clearer Captive Portal Message on Correlation Failure**

When NAC cannot correlate a device's MAC and IP address, the captive portal now explains what happened instead of failing without explanation.

![](https://uploads.developerhub.io/prod/97qW/c65t1r05c7emwqr21jekq8bv0h2cbyp88pkg6pv53wen3nrj47vz0z3ai0n6sw1c.png)

Enhancements** Cloud Native and OTS Integrations Removed**

The Cloud Native and OTS (OT Threat) integrations have been removed, along with their proxy components and supporting cloud infrastructure. The RadSec client and PKI server have also been removed

Enhancements** FreeRADIUS Logs Included When Applying Configuration Fails**

When a FreeRADIUS configuration fails to apply, View Output now includes the FreeRADIUS log in addition to standard output and error. Failures such as an invalid LDAP server configuration are frequently explained only in that log, so the cause is now visible without retrieving logs separately.

![](https://uploads.developerhub.io/prod/97qW/v3fkrtfj47bcqatj8tswa6njjsuc5mu8wdr8anzwt5sat5ffbcq8bknps5iy5jup.png)

## Additional Features

New Features** Redesigned Enroll Product Page **

Enroll Product page has been redesigned to provide a single-glance view of the onboarding path, clearly separating standalone product setup from endpoint device deployment.

![](https://uploads.developerhub.io/prod/97qW/11kuqm52doa97tm7qhuoxazvqvdqs9zs2wkgwq57bimm4g6g5l9xqc6tah74eiy5.png)

New Features **Support Syslog Forwarder for MetaDefender Industrial Firewall**

MetaDefender Industrial Firewall can now send their logs through My OPSWAT Central Management to an enterprise SIEM using a Syslog profile.

Refer to [Syslog Profile](https://www.opswat.com/docs/cm/integrations/syslog-profile) guidelines for detailed instruction.

![](https://uploads.developerhub.io/prod/97qW/o5vdzgh2ss4f4getluoqtkjrpyaest5eb2p4selmxvud0zt4odwg1pad8r0do8xi.png)

New Features** Display Map and Location Details**

Administrators can view device location details on an interactive map and access the location directly in Google Maps from the device marker.

![](https://uploads.developerhub.io/prod/97qW/qlj0ltzdehwfvucszreiadl7ruvdmoms824fg49fdftp6zok19rq2dy3214eo68z.png)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
