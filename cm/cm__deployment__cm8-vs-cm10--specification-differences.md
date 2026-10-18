<!-- source: https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences -->

# CM8 vs CM10: Specification Differences (Configuration Items, Operation, and Usage)

> **Purpose of this Document**
>
> This page lists the differences in specification between **My OPSWAT Central Management v8 (CM8)** and **My OPSWAT Central Management v10 (CM10)**. It covers configuration items, operation and day-to-day usage, so teams migrating with the official [Migration Plan: Upgrading from CM8 to CM10](https://www.opswat.com/docs/cm/deployment/upgrading-from-cm8-to-cm10) can find where each CM8 function lives in CM10 and what behaves differently.
>
> **Versions compared**
>
> - CM8 = My OPSWAT On-premises **2025.4.1-OP** with the Product Management component **2025.4.1** (docs: [/docs/myop](https://www.opswat.com/docs/myop/configuration), [/docs/product-management](https://www.opswat.com/docs/product-management)).
> - CM10 = My OPSWAT Central Management **10.7.x** (on-prem 10.7.26062, docs build 10.7.26091, [/docs/cm](https://www.opswat.com/docs/cm)).

**In This Guide**

- [Summary of Key Changes](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#summary-of-key-changes)
- [Navigation Map: Find CM8 function in CM10](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#navigation-map-find-cm8-function-in-cm10)
- [Detailed Differences by Area](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#detailed-differences-by-area)
  - [Product Enrollment and Inventory](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#product-enrollment-and-inventory)
  - [Groups and Configuration Management (Configuration → Policy)](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#groups-and-configuration-management-configuration--policy)
  - [Dashboards, Reports and Notifications](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#dashboards-reports-and-notifications)
  - [License Management](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#license-management)
  - [User Management, Authentication and RBAC](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#user-management-authentication-and-rbac)
  - [Audit Logs and SIEM Integrations](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#audit-logs-and-siem-integrations)
  - [Account-level Settings](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#account-level-settings)
  - [Server Settings (HTTPS, proxy, email, certificates, backup, monitoring)](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#server-settings-https-proxy-email-certificates-backup-monitoring)
  - [Product Updates and Engine / Module Updates](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#product-updates-and-engine--module-updates)
  - [API](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#api)
  - [Remote Command](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#remote-command)

- [New in CM10 (no CM8 equivalent)](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#new-in-cm10-no-cm8-equivalent)
- [Quick Guide: Common Kiosk Tasks in CM10](https://www.opswat.com/docs/cm/deployment/cm8-vs-cm10--specification-differences#quick-guide-common-kiosk-tasks-in-cm10)

## **Summary of Key Changes**

CM10 is not a redesign of the CM8 user interface. It is a different platform that merges the former My OPSWAT cloud console (Endpoint, Secure Access, NAC) with on-prem product management.

The biggest visible change is how menus are organized:

- **CM8** organizes menus by **product**.
- **CM10** organizes menus by **security solution**, such as File Security, Peripheral Media Protection, Portable Malware Scanning, and Endpoint Security. Each solution is an expandable group with its own **Dashboard** and **Policies**.

This is why the CM10 interface feels so different. For information related to MetaDefender Kiosk, you can look under *Inventory > Devices* or *Peripheral Media Protection*.

![](https://uploads.developerhub.io/prod/97qW/01gori2vhqj05p230rmj1oq5hn07fh0dj051s9ryc855udgild1h4enwz2b11jpb.png)

| Area | CM8 | CM10 | What it means for users |
| ---- | ---- | ---- | ---- |
| **Menu organization** | Product-centric: *Products → [product] → Instances / Groups / Overview* For Kiosk: *Products → MetaDefender Kiosk → K-Series / L-Series → Instances / Groups*; Overview at the Kiosk level | Solution-centric: ***Dashboard***, ***Inventory ****(Devices / Services / Groups)*, ***[Solution]**** → Policies*, *Updates*, *License*, *Logs*, *Settings*, *User Management*. | Use the navigation map in section 2 to find CM8 function. |
| **Configuration model** | Group configuration taken from a selected instance (*Set as Group Configuration* → *Apply Group Configuration*). It is versioned and requires strict product-version parity. | You manage configuration as **Policy**, created from the defaults of the latest product version, or *imported from an instance*. Edit it in the console, then **assign it to a group**. Optional auto-sync. Version-compatibility handling. | After migration, CM8 Group Configuration becomes the CM10 Policy Name. Configuration changes are now made on the Policy. |
| **Inventory** | Instances are listed per product. | One unified inventory, split into: **•Devices** (Kiosk Windows, Kiosk Linux, Media Firewall, Drive, Industrial Firewall, Endpoint) **•Services** (Core, ICAP, MFT, Aether; Storage Security on SaaS) Includes tags, filters, and health and connection status. | Find your Kiosks under **Inventory **→** Devices**. |
| **Console access** | `http://<IP>` by default. You can enable HTTPS later, but the HTTPS port can't be changed. | `http://<IP>:9000` by default. Products connect on ports **9000 **and **443**. HTTPS requires a **domain or proxy URL**; an IP address is not supported for HTTPS. **Main Service port** (default 9000) is configurable, with the option *Use a different port for Admin Console*. | You get more control over secure connections. |
| **Updates** | Module updates (Manual / Internet / SMB folder); Kiosk K/L-Series firmware update (Manual / Internet); auto-update toggle for Media Firewall only. | **Updates → Modules **(Internet / Manual), **Firmware** (Kiosk Windows / Linux), *Software*: remote **update / rollback jobs** with maintenance windows (Kiosk, Core, Industrial Firewall); *Endpoint Components*. | You get more control over product and engine versions for each group. |
| **Users and role-based access control (RBAC)** | Local / AD / SAML directories; roles with** None / View Only / Full Access** per feature. | Local, AD, SAML 2.0 and OIDC SSO, SCIM (Okta); roles with **Hide / Read / Write** per UI section, plus advanced permissions per group or per policy; role-based session timeout. | Roles must be re-designed in the new permission model. **Role changes:** in CM8 a new / changed role takes effect immediately (at most a page reload); in CM10 the user must **log out and log in again**. |
| **Notifications & SIEM** | Email only (4 threshold triggers + Kiosk summary reports). Prometheus metrics endpoint. | Notification Groups (email HTML/JSON), webhooks, Syslog (CEF), Google Cloud Logging, Splunk add-on;  | Alerting must be rebuilt as Notification Groups. |
| **Scope of management** | MetaDefender products (Core, Kiosk, ICAP, MFT, Media Firewall, and more) **plus** inventory-only products. | MetaDefender products **plus** Endpoint management, Patch Management, Secure Access (SDP, IdP MFA), NAC (RADIUS), Vulnerability management. | Many new menus (Endpoint, Patch, Secure Access, NAC) do not exist in CM8 and are not needed for Kiosk. Use Navigation Map to find each CM8 function. |

## Navigation Map: Find CM8 function in CM10

### **CM8 Menu: Products**

| Function | CM8 location | CM10 location (10.7) |
| ---- | ---- | ---- |
| List of product instances | Products → [product] → Instances tab  For Kiosk: Products → MetaDefender Kiosk → K-Series / L-Series → Instances | Inventory → Devices (Kiosk) |
| Product groups | Products → [product] → Groups tab | Inventory → Groups |
| Group configuration | Products → [product] → Groups → [group] → Configuration tab | Peripheral Media Protection → Policies (Kiosk); assign the policy at Inventory → Groups → [group] → Settings → Assign Policy |
| Single-instance configuration | Instance details → Configuration tab → Edit | Inventory → Devices → Kiosk tab → Settings tab → Edit |
| Product dashboards | Products → [product] → Overview | Peripheral Media Protection → Dashboard |
| Licenses | Licenses (left menu) → product tab | License (left menu) → Kiosk L-Series / Kiosk K-Series CM10 has no license |

### **CM8 Menu: **User Management

| Function | CM8 location | CM10 location (10.7) |
| ---- | ---- | ---- |
| Users, roles, directories | User Management → Users & Groups / Roles / User Directories | User Management → Users and Groups / Roles / Active Directory / SSO / IdP Mappings |

### CM8 Menu: Events History

| Function | CM8 location | CM10 location (10.7) |
| ---- | ---- | ---- |
| Audit / event log | Events History | Logs → Admin Events / Device Events / Service Events / Webhook Events (SaaS version also includes Syslog, Export, OAuth API, Patch, and Backup Restore events) |

### **CM8 Menu: Settings**

| Function | CM8 location | CM10 location (10.7) |
| ---- | ---- | ---- |
| Registration code | Settings → Global → Organization → Registration Code | Settings → Global → Account → Registration Code; also the *+Enroll Product* button |
| Session timeout / PIN requirement | Settings → Global → Organization → User Settings | Settings → Global → Account (*Enable Account PIN security prompt*, *Inactivity Timeout*) User Management → Roles |
| Data retention | Settings → Global → Organization → Data Retention | Settings → Global → Data Storage → Global data retention (days) |
| Certificates | Settings → Global → Certificates | Settings → Servers → Secure Connection (console certificate) Settings → Certificates (certificates distributed to Kiosk K-Series 4.7.11+) |
| HTTPS / Proxy / Email | Settings → Global → Server → Secure Connection / Proxy / Email | Settings → Servers → Secure Connection / Proxy Server / Email Server |
| Module (engine) updates | Settings > Products > Modules tab | Updates > Modules (Kiosk Linux / L-Series) |
| Product upgrades | Settings → Products → Products tab (Kiosk K-Series / L-Series Update, Media Firewall Update with auto-update toggle) | Updates → Software → Kiosk Windows and Kiosk Hardened Image (also Core, Industrial Firewall) → Jobs / Packages (update / rollback jobs) Updates → Firmware → Kiosk Windows / Kiosk Linux |
| Upgrade of CM itself | Settings → Products → Upgrade My OPSWAT | There's no in-console upgrade. Run the newer MSI or RPM on the server (OVA: bootc switch). |
| Reports & alerts | Settings → Reports & Notifications | Settings → Global → Notifications tab (Notification Groups + Assign Group) Settings → Reports → Report Manager |
| API keys | Settings → Integrations → APIs | OAuth application (client credentials); Settings → Integrations (Endpoint Identity, Webhook Integration, Syslog, Google Cloud Logging) |
| Backup | Settings → Global → Import/Export tab | Settings → Servers → Backup |
| Data migration to CM10 | Settings → Global → Data Migration (Processing History → CM10) | Not applicable. CM10 is the migration target. |

### **CM8 Menu: Outside The Console**

| Function | CM8 location | CM10 location (10.7) |
| ---- | ---- | ---- |
| Support package | SSH to appliance + `cent-generate-sup-package.sh` | `Run mocmSupportPackage.exe in CM installation folder`; or Help Center > Support Packages |

## Detailed Differences by Area

Each area starts with the CM8 menu you used and its equivalent location in CM10, so you can go straight from the settings you know to where they live now.

### Product Enrollment and Inventory

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| Enrollment direction | Product → CM (product clicks *Unmanaged* → Server API URL + Registration Code → *Enroll Now*) | Same product-initiated model. CM10 shows URL + code in the *+Enroll Product* dialog. Kiosk can also enroll during OOBE / setup wizard. |
| Server API URL | `http(s)://<CM8 server>` (port 443) | CM10 Server URL (ports 9000 / 443). Keep the same FQDN during migration to avoid re-enrollment. |
| After enrollment | Instance status Managed | Instance status Managed;  Kiosk local settings become **greyed out** (managed from CM). |
| Inventory view | Per product (Kiosk: Products → MetaDefender Kiosk → K-Series / L-Series → Instances / Groups): Instances tab; Actions Delete / Move to group / Acknowledge all threats / Export to CSV; bulk rename | Inventory → Devices / Services: health (Unknown, Operational, Minor, Significant, Critical, Blocker), connection (Connected / Disconnected > 24 h), version, group, location, last seen; filters by Product Type, Product Status, License Status, Health Status (10.3.2511); custom tags; export |
| Unenroll | Delete instance in CM or *Disconnect* in product | Delete from Inventory (Inventory → Devices / Services → [item] → Actions → Delete, or select rows > Select Action) or *Disconnect* in the product – same as CM8 |
| Supported Kiosk | K-Series (Windows) 4.7.3+; L-Series (Linux) 5.5.2+ | K-Series (Windows) and L-Series (Linux), listed under *Inventory *→* Devices* |
| Managed features | Inventory, dashboard, reports, configuration, license, auto-upgrade; module updates (L-Series) | Peripheral Media Protection dashboard and policies; license; remote update and rollback (Kiosk Windows 4.8.0+, Hardened Image 4.8.3+); firmware updates; certificates (4.7.11+); BadUSB protection; module updates (Kiosk Linux) |

 CM8 Enrollment dialog on the product

![CM8 – Server API URL + Registration code](https://uploads.developerhub.io/prod/97qW/sq1o9hugoy07geyu9f13r72qis0puhj2a2rinwkj5mus9ojm7swnoqi8leel4we5.png)

CM10 +Enroll Product dialog

![*CM10 – +Enroll Product: select product; registration code shown in the dialog (masked here)*](https://uploads.developerhub.io/prod/97qW/jcn2v1rgc4v8jzw7n9ivsna4oc4qrz1w6p4yrz8lmg929azatiebts9pd0fowgy8.jpeg)

CM8 Products > Instances

![*CM8 – Instances dashboard (per product)*](https://uploads.developerhub.io/prod/97qW/cyojlwasuiaue53wonvfubc613kw0l486iwobrslptd9bps5spsjstnyq3w4o6p3.png)

 CM10 Inventory

![*CM10 – Inventory > Devices (tabs per product: Kiosk Windows, Kiosk Linux, Media Firewall, Drive, Industrial Firewall, Endpoint)*](https://uploads.developerhub.io/prod/97qW/9d48o8sovkwxpvh75t4x9mhvrzrreypfvmj73xvvuoiq1h30rk2xgw5cy8fcqyzp.webp)

### **Groups and Configuration Management (Configuration → Policy)**

This is the biggest change in daily operation.

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| Group scope | Per product; default group created at first instance / license; instance belongs to one group | One product type per group; default group per product (not deletable);  |
| Where the configuration lives | On the **group** ("Set"), derived from one instance | In a **Policy** object, independent of instances, assigned to one or more groups (one policy per group) |
| How to create | Instances tab → instance menu → *Set as Group Configuration* | Depends on each solution For Kiosk: *Peripheral Media Protection *→* Policies* → *Create* (defaults of latest product version) or *Import Policy* from a Kiosk; row menu: Clone / Delete |
| How to edit | Two ways: (1) Group > Configuration tab > Edit directly, then Apply Group Configuration; (2) edit an instance's configuration, then Set as Group Configuration again | Edit the policy sections in the console → SAVE → PIN |
| How to deploy | Group > Configuration tab → *Apply Group Configuration* → select instances (delivered when the instance checks in) | *Inventory > Groups > [group] > Settings > Assign Policy* (+ Policy Version); optional *Automatically sync group policy for new devices* (Kiosk, CM10 10.5+; Services products: "new instances"); instance-level *Apply Group Settings* |
| Versioning / status | Configuration version (e.g. 1.0.1), * = locally modified, sync icon; Current / Custom / Out-of-date / Pending; *Not Compatible* tab | Policy version indicators (10.1.2507), Inherit vs Custom mode (10.1.2508), version-compatibility status (10.3.2512) Status columns on the group detail page (Devices / Instances tab): • **Auto Sync Policy**: Enabled / Disabled / Incompatible (device version not compatible with the policy version = CM8 *NOT COMPATIBLE*) / No Policy (no policy assigned to the group; *Apply Group Settings* disabled) • **Settings Update**: ✓ + time (synced) / Pending (waiting for the device to check in) / N/A (never synced or incompatible) |
| Version parity | **Strict**: source and target instances must run the same product version, otherwise "NOT COMPATIBLE" | No version-parity limitation when CM10 manages Kiosk 4.7.11+ |
| Per-product setting content | CM8 renders the product's own configuration model | The Kiosk policy is based on the Kiosk product configuration. |
| Additional central objects | — | Certificates (Kiosk K-Series 4.7.11+) assignable to policies / groups |

 CM8 Promote an instance, then apply to the group:

![*① Set as Group Configuration*](https://uploads.developerhub.io/prod/97qW/ylv0xin2weypfeec4fooiq0uaqdmot4j2kygen7yzo5d1lvlc0knnn5iujzuvwyw.png)

![*② Group Configuration tab (version, stats)*](https://uploads.developerhub.io/prod/97qW/ccjbwy53j1w91ftsmhnngfjiamlao0xq4p1idqgohd7x78qk81uduflb48kyqylb.png)

![*③ Apply Group Configuration*](https://uploads.developerhub.io/prod/97qW/a0bnhhnwf4len8fwpr8f7eid6ktcl6uexfmr9ur8ra6jezmuq63kp6yoxyiwzoas.png)

CM10 Import or create a policy, assign it to a group, enable auto-sync:

![*① Peripheral Media Protection > Policies > Import Policy (from a Kiosk instance)*](https://uploads.developerhub.io/prod/97qW/yt35han48jr3e3kn6a2j75vdq2w54qiinnm9wcgc9huq2n9djgxpldolpkv2l4bl.webp)

![*② Inventory > Groups – Assigned Policy and Policy Version per group*](https://uploads.developerhub.io/prod/97qW/n8betwjjfh5kl07bwvi1j2f91fyomutngqrebkth1dwf3wev69uznq0r96c5hat6.webp)

![*③ Group > Settings – Assign Policy + "Automatically sync group policy for new devices"*](https://uploads.developerhub.io/prod/97qW/nobpvaisfhoiuqls1wq4ei4641ii1iuf7hszbe9k1udcfwy7y2vpgc71qfdcvici.webp)

If auto-sync is not enabled for the group, open the device settings to enable it, or click Apply Group Settings.

Tip CM8 users are used to *Apply Group Configuration*. In CM10, assign the policy to the Kiosk group and enable *Automatically sync group policy for new devices* so newly enrolled Kiosks receive the group policy.

### **Dashboards, Reports and Notifications**

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| Dashboards | Per-product *Overview* (Kiosk); widget add / remove | Peripheral Media Protection → Dashboard; customizable dashboards (max 20 widgets / page) |
| Scan reports / history | Instance > Scan Reports (export .json / .pdf / .txt) | Kiosk session PDF reports: *Inventory > Devices > [Kiosk] > Overview > Scan Sessions* (7D / 30D, search by Session ID; Timestamp / Session ID / Processed Files / Files with Issues). Per session: *Download JSON* or *Generate Report* (PDF). By default the Kiosk submits a PDF only when files with issues were found; otherwise *Generate Report* builds one (older format, may differ from the latest Kiosk format). → JSON + PDF per session (CM8: .json / .pdf / .txt) |
| Scheduled reports | Summary report (Minutely … Monthly, email list, instances). Supported for Kiosk only. | Supported for Hardware products *Settings > Reports > Report Manager* (Daily / Weekly / Monthly); History tab |
| Alerts | Email only, 4 triggers: risk level, health status, CM storage < X GB, product free space < X GB | Notification Groups (HTML / JSON email, recipients, trigger events) assigned globally or per group; webhooks; in-app bell; Kiosk availability, certificate expiry and group-config-change events |

CM8 Notifications (email triggers)

![*CM8 – Reports & Notifications*](https://uploads.developerhub.io/prod/97qW/mcl8ep8op2qf37gobfcozwvkg8i5rwyxhzc90q13vlh17b881sphsclbrfipqd4d.png)

CM10 Notifications (email triggers)

![*CM10 - Notification Group*](https://uploads.developerhub.io/prod/97qW/i64erk5n4po88otg7nvw1bt1ppss86s8eqh2zl50703b532xhak1kncou0ywaw9p.png)

CM8 Products > MetaDefender Kiosk > Overview tab

![CM8 - Open MetaDefender from My Products menu](https://uploads.developerhub.io/prod/97qW/t28x1yhj6pruc2xmr648ko5jdkr9k4kq68ptjtr4bz321zjmj9zbvb6y60q74778.png)

![*CM8 - MetaDefender Kiosk dashboard*](https://uploads.developerhub.io/prod/97qW/xx9vgsd0dozvzjnznw34de9qzoc0o8h23b17rb80kjdvnlzudchi6rafr6rr6rkg.png)

CM10 Peripheral Media Protection > Dashboard

![*CM10 – Peripheral Media Protection (Kiosk) dashboard*](https://uploads.developerhub.io/prod/97qW/yfr6ttbhf6cy1y3lrhfi709v90tg2cy0tj3j9vx4mcnj03wym12ep56aovr5f7u2.webp)

### **License Management**

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| Products | My OPSWAT (CM server), Core, ICAP, Kiosk K-Series, Kiosk L-Series | Endpoint, Kiosk L-Series / K-Series, Core, MFT, Aether (formerly Sandbox), Industrial Firewall, Storage Security |
| Online activation | Licenses > [product tab] > Add New License > Activation Mode Online: enter License Key > Add; only one online license active per product type | Allows multiple license keys per product License > product > Add License (key + group); enrolled unlicensed instances pick up a license automatically |
| Offline activation | Add New License > Activation Mode Offline: 1. use the Product Deployment ID on the My OPSWAT portal to download a license file, 2. upload the activation file (Add More File for several). No group selection. | Same flow in the *Offline* tab; offline licenses cannot be allocated to groups (Group column: "Not applicable for offline activation") |
| License page display | Per product tab, two sections: **Online Activation** (status Active + License Key + Delete) and **Offline Activation** (list per Deployment ID: Instance Name / Availability / Expiration Date, Actions menu, search by Deployment ID) | One expandable card per product; online and offline licenses in the **same table** (Order / License Key / Status / Monitored / Group / Expiration Date). Online: masked key + Group (e.g. "All Groups", editable). Offline: "Offline Activation (<Deployment ID>)" |
| Group allocation | — | **Allocate Group License**: dedicate slots to groups; "All Groups" as fallback; audit log |
| CM server license | Licenses > My OPSWAT tab (Active / Deactivate, Deployment ID) | Settings > Global > Account tab > License section (Device Monitored / Devices Limit / Status) |
| Migration | Entitlement stays valid (no new purchase) but **licenses are not migrated automatically** – re-add the product licenses in CM10. |

CM8 License Management

![*CM8 – per product-type tabs*](https://uploads.developerhub.io/prod/97qW/wcua89qdeigcrdzzqd9euviepupb7yfzmlprcfq4tutb4r5efuw4q4zduxzgafi6.png)

CM10 License Management

![*CM10 – license by product family*](https://uploads.developerhub.io/prod/97qW/x29vugnfxw9w3w4wuqbu9nyl8c9t35lojtry5sa1leaq5cjvxesnmqu9brim1ffg.jpeg)

![*CM10 – Add License: choose Online / Offline and the Group(s) that can use the license*](https://uploads.developerhub.io/prod/97qW/wybuydz2tcvszn1s7wq2w1sgyr8zi24sria631e3ubnenjx0g8494i6l36m3wo09.jpeg)

### **User Management, Authentication and RBAC**

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| Menu | User Management > Users & Groups / Roles / User Directories | User Management > Users and Groups (Console Users / End Users) / Roles / Active Directory / SSO / IdP Mappings |
| Local users | Local directory with password policy and login-attempt policy (3 failures, 5 min lockout by default) | Local console users (on-prem), invited users (SaaS via OPSWAT account) |
| Active Directory | Bind user, host / port, TLS / StartTLS / None, timeout, user / group base DN; add AD users or groups; multi-group role resolution rules | Add New Directory → Test Connection; add AD users or groups; directory chosen on the login page |
| SSO | SAML 2.0 (IdP / SP initiated, single logout), IdP group → role mapping, default role | SAML 2.0 (Entra ID, Okta, PingOne, ADFS), OIDC (10.7), SP-initiated on-prem (10.5), JIT users created as Read-Only, SCIM provisioning with Okta |
| Roles | Administrator, View-Only + custom; per feature: None / View Only / Full Access | Per UI section: **Hide / Read / Write** + **Advanced Permissions** for specific Device Groups and Policies; up to 50 custom roles (10.6); feature permissions (e.g. Skip By Hash, Password Storage) |
| Session timeout | Global 30 min (max 480) | Global + per-role absolute custom timeout |
| Role change takes effect | Immediately (at most a page reload) | After the user **logs out and logs in again** |
| PIN | Set in User Profile; reset by admin | User Settings; "Forgot your PIN?" sends a temporary PIN by email |
| Migration | User accounts are **not** imported by CM8Importer. Re-create users and roles in the new model and re-configure AD / SSO after cut-over. |

CM8 Add Role (None / View Only / Full Access)

![*CM8 – Add Role*](https://uploads.developerhub.io/prod/97qW/a65d3yiieekgzrnhl44z2rrsdkmrh8055c95bru0mzmf1b75117zjzrookn870nc.png)

CM10 Create Role (Hide / Read / Write)

![*CM10 – User Management > Roles (default roles: Administrator, Read-Only, Help-Desk, Security-Admin, Security-Auditor)*](https://uploads.developerhub.io/prod/97qW/y1vbb0g97q5i3wvm1cdxfldvga8ooo9t4zkme1fiheqpr9mxx5tw4qck1la9ejjr.jpeg)

![*CM10 – Create New Role: Hide / Read / Write per section*](https://uploads.developerhub.io/prod/97qW/6g9b0yoidhdqmjd08tzmp0s325k2onyogumt60yufih0wql8fmfn0mcqk9c47qay.jpeg)

![*CM10 – Advanced permissions (Hide / Write for specific policies or groups)*](https://uploads.developerhub.io/prod/97qW/hbnumath7zg9mrfwqijahamw9rsjg1nif8ndavdb93oqyahfyk61pnkg21mlgd0j.jpeg)

CM8 Active Directory

![*CM8 – AD directory configuration*](https://uploads.developerhub.io/prod/97qW/2z72b3wf7azlfn6tnmzo4fadmfdawkhcywjsznkrnu8tvibttizpx9trbs2ds8c4.png)

CM10 Active Directory

![*CM10 – User Management > Active Directory > Add New Directory*](https://uploads.developerhub.io/prod/97qW/1fmjaa49lxih3wu2hyezi35qfv6fvnziqxshgmkgnay6bfayyxkdmfnwe55i1105.jpeg)

### **Audit Logs and SIEM Integrations**

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| Audit log | Events History (config sync, license events) | *Logs > Admin Events* (logon / logoff / failed auth, configuration change, registration-code revoke…), *Device Events*, *Service Events* (Core / MFT / ICAP…), *Webhook Events*; SaaS also has Syslog / Export / OAuth API / Patch / Backup Restore Events; CSV export with PIN |
| SIEM / log forwarding | N/A | Settings > Integrations (on-prem 10.7.26062 tabs: Endpoint Identity / Webhook Integration / Syslog / Google Cloud Logging): **Syslog (CEF)**, **Google Cloud Logging**, **Webhooks**, Splunk add-on (Splunkbase 5530).  |
| Note | For Kiosk, the CEF event list covers enrollment lifecycle events (enrolled, deleted, unenrolled). |

### **Account-level Settings**

| Item | CM8 (Settings > Global > Organization) | CM10 (Settings > Global > Account) |
| ---- | ---- | ---- |
| Registration code | One per organization; *Revoke Code* generates a new one (enrolled instances unaffected) | Registration section; *Generate new code* (refresh icon) creates a new one; the section also holds the *MetaDefender Endpoint Recovery Key*. **Imported** from CM8 so enrolled products keep working |
| User timeout | Default 30 min, max 480 min | Account > *Inactivity Timeout* |
| PIN for changes | *Require PIN for change activities* | *Enable Account PIN security prompt*; PIN is asked for most write actions (policy save, export, role change…) |
| Time zone | User time zone | Account time zone (Local / UTC), 24h / 12h format |
| Multi-organization | Switch Organization from user menu | Account model. Users are invited per account |

CM8  Global settings – Organization tab

![*CM8 – Settings > Global > Organization*](https://uploads.developerhub.io/prod/97qW/l2ofj20j2xfuih0vl276u0ylgv71lshoapsd34rlu58yatn5i2sfk2ll6weckx54.png)

![*CM8 – User timeout and PIN requirement*](https://uploads.developerhub.io/prod/97qW/folj5dimgs773wznzoqfu34y37ec7lztslfahuq7kvpeuodvhxauywefdor59j3m.png)

CM10 Settings (platform-wide)

![*CM10 – Settings > Global > Account (Recovery Key, Registration Code, PIN prompt)*](https://uploads.developerhub.io/prod/97qW/q0e7vc8vrebvurd533rp43ysd31a73ptp11qtc0efmf0gpzjoyv6zcp7xmcs0rs0.jpeg)

### **Server Settings (HTTPS, proxy, email, certificates, backup, monitoring)**

| Configuration item | CM8 | CM10 |
| ---- | ---- | ---- |
| **HTTPS / secure connection** | Settings > Global > Server > Secure Connection: toggle *Enable HTTPS*, choose TLS version(s), port fixed; certificate uploaded in Certificates tab; *Server URL* field used in report links. | Settings > Servers (tabs: Email Server / Secure Connection / Proxy Server / Backup / Trace Log) > Secure Connection: three modes – *Current IP Address* (HTTP only), *Custom Domain* (upload .crt + .key), *Proxy URL* (reverse proxy). Ports: *Main Service port* (9000) + checkbox *Use a different port for Admin Console*.  HTTPS with a bare IP is not possible in CM10. |
| **Proxy** | Settings > Global > Server > Proxy: Server address, Port, Username / Password (Basic only), "Use the same proxy for HTTPS", **Bypass list** (CIDR / wildcards). | Settings > Servers > Proxy Server: *Enable External Proxy for HTTP and HTTPS*; auth **Basic** (address, port, user / password, HTTPS proxy option) or **Kerberos** (KDC address / port, Realm, SPN, user / password). |
| **Email (SMTP)** | Settings > Global > Server > Email: type *Microsoft 365* (Tenant ID, User ID, Client ID, Client Secret) or *Others* (sender, name, server, port, None / TLS / StartTLS, Login auth); Send Test Email. | Settings > Servers > Email Server: Enable SMTP; Send From, SMTP Server, Port, None / StartTLS / TLS, Authentication None / Login, Username / Password. |
| **Certificates** | Settings > Global > Certificates: server certificate (HTTPS) + *Trust Certificates* for email / AD / proxy; "Verify SSL certificates" option. | Console certificate under *Secure Connection*. *Settings > Certificates* = certificate store that can be distributed to Kiosk K-Series (4.7.11+) per instance or per policy.  New capability: central certificate distribution to Kiosk. |
| **Backup / restore** | Settings > Global > Import/Export: select data categories, AES-256 encrypted .zip, manual only, max 10 GB; import replaces configuration. | Settings > Servers > Backup: **scheduled** (daily, UTC time) or manual; .CMX files; kept 30 days; restore only via Setup Wizard on a fresh install. |
| **Troubleshooting** | Prometheus metrics at `localhost:9100/metrics`. | Help Center > Support Packages, optional diagnostic data to OPSWAT; *Settings > Servers > Trace Log* (max rotated file size, delete logs older than N days, retain N files, min log level).  |
| **Data retention** | Single value for event logs + product reports (Settings > Global > Organization > Data Retention): default 30 days, maximum 18250 days. | *Settings > Global > Data Storage*: Global data retention (days) + Advance settings, plus a separate MetaDefender Endpoint section (default 30 days); processing-history retention 3–365 days depending on file status (10.3.2511+); trace logs default 14 days (10.6). |

CM8 Settings > Global > Server > Secure Connection

![*CM8 – Enable HTTPS toggle*](https://uploads.developerhub.io/prod/97qW/aoged2q4wu85twyfwzwrzoxlr62yr2zh9o35sxx2d5j2220go96g1l0rj70959rw.png)

CM10 Settings > Servers > Secure Connection

![*CM10 – Settings > Servers > Secure Connection: HTTPS is not available for an IP address; use Custom Domain or Proxy URL*](https://uploads.developerhub.io/prod/97qW/jbrd4mw4l7hr3ujafl3exe6vfa25n9s5u6l4cvrtv7npeh6cgrnsnmrt4crfllg4.jpeg)

CM8 Proxy (Basic auth, bypass list)

![*CM8 – Settings > Global > Server > Proxy*](https://uploads.developerhub.io/prod/97qW/90aaa7321f1otxnahuxrqfhg6y0y2l4y0nry1v4sy5bwe0katuspqusf8nno1lw2.png)

CM10 Proxy (Basic / Kerberos)

![*CM10 – Settings > Servers > Proxy Server (Basic / Kerberos, HTTP / HTTPS proxy)*](https://uploads.developerhub.io/prod/97qW/eo1mnbkotbxwrmfvz5bmhgt7fefvjdm8rwwzlhyym2udr1r5tlwrly2pp3vbvtwh.jpeg)

CM8  Email – Microsoft 365 / Others

![*CM8 – Microsoft 365 email configuration*](https://uploads.developerhub.io/prod/97qW/dkklm7nuf19imev5jbllvkt80kx1dz1trg3fqx86j45uxgooglingcgdmrklqzib.png)

CM10 Email Server (SMTP)

![*CM10 – Settings > Servers > Email Server*](https://uploads.developerhub.io/prod/97qW/jmyiqj577oje0flor4kxaaifsc9gijnwvz5mq2ph90253u2t6lxd21w10x8vacsk.jpeg)

CM8  Certificates

![*CM8 – Add Certificate (server certificate)*](https://uploads.developerhub.io/prod/97qW/4foghyx981j4lhn8j8huhi7ty9ju6cwwicxu9jicy2jgrspmzcogm90gq4iye3t5.png)

CM10 Certificates

![*CM10 – Settings > Certificates > Import Certificate (separate files or bundle)*](https://uploads.developerhub.io/prod/97qW/gtaslc7y1ghlf753wmbfor4chkz743cgy4e5d7dwsf9yhzwl9blase18t1qz0tmn.jpeg)

CM8 Import / Export

![*CM8 – Export: select data categories*](https://uploads.developerhub.io/prod/97qW/l451l4ouuwqqq86hamgija1fuaej4qpq83bfi1b7kk769xuixfmdj8o3dj7famyb.png)

CM10  Backup

![*CM10 – Settings > Servers > Backup (scheduled daily backup, kept 30 days)*](https://uploads.developerhub.io/prod/97qW/jwr8hqgjo1j9r4fepdx7hm0d05pg2kab0u7h4uyys9f11dqfdhqz8wt1evkvcz8q.jpeg)

## **Product Updates and Engine / Module Updates**

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| Module (engine) update sources | Settings > Products > Modules tab: **Manual** (.yml + .zip), **Internet** (Minutely … Monthly), **Folder** (SMB share). Paused if free disk < 20 %. | *Updates > Modules* for Kiosk Linux: **Internet** (Daily / Weekly at a time) or **Manual** (.yml + .zip). |
| Product (application) upgrade | Settings > Products > Products tab: Kiosk K-Series Update (Internet + Recurrence Pattern); Kiosk L-Series Update (Update Source Manual / Internet); Media Firewall Update with the only auto-update toggle ("only available for MetaDefender Media Firewall"); Upgrade My OPSWAT (.tgz) | *Updates > Software > Kiosk (also Core, Industrial Firewall) > Jobs*: target groups / Kiosks, target version, download window, maintenance window, concurrency, stop-on-failure, auto reboot, email report; rollback jobs |

CM8 Module Updates

![*CM8 – Settings > Products > Modules tab*](https://uploads.developerhub.io/prod/97qW/753db6a67pt21bdl7n7r681pnvn6qj5cskhpkgnmqlwvmh0g4171zye8ipm4zrr4.png)

![*CM8 – SMB folder source*](https://uploads.developerhub.io/prod/97qW/gn0f8u9g7mu0m58cm3a4kygc5m832veyfx1s378hfo4wjvxyqxzt4t40n60ys8by.png)

CM10 Module Updates

![*CM10 – Updates > Modules (Source: Internet / Manual / Folder; Package and Assignment tabs)*](https://uploads.developerhub.io/prod/97qW/qs2sefjdwoaf83d9djbz8341kgn7wlupwoclxdn29wbjtb4cdx22af4d2vo3fnxb.jpeg)

CM8  Product Updates

![*CM8 – Settings > Products > Products tab (Kiosk K-/L-Series, Media Firewall, Upgrade My OPSWAT)*](https://uploads.developerhub.io/prod/97qW/9z8msrbj9s81xln0bpyukygcqfen4i3wjstuz5f0ef7sfuzxgwnq97dwyi1readd.png)

CM10 Product Update Job

![*CM10 – Updates > Software > Kiosk > Jobs (Create Update Job / Create Rollback Job)*](https://uploads.developerhub.io/prod/97qW/hrk2i3bia8mgdaftsmgo78crid1242bxkkhk51wcijnim9uyyxxgk7ray3nbrxrr.jpeg)

![*CM10 – Create Update Job: target groups or instances*](https://uploads.developerhub.io/prod/97qW/l0pao302rf2h4ve5bo37jb3j6r3q028jy6aarpvru2jr23hsdvt6yo2g24g8eucw.jpeg)

![*CM10 – Create Update Job: update preparation, maintenance window, update options*](https://uploads.developerhub.io/prod/97qW/5u06mq8zzsuatadged7a24ih7zm3qvscajni1nl4dpnv7p0aq6ilguaychgz9c1g.jpeg)

### **API**

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| Authentication | Secret key → `POST /api/console/get-token` → bearer token | OAuth 2.0 client credentials → `/o/oauth2/token` (~12 h token); ~10 requests / min per API |
| Coverage | Read-mostly: inventory, Core / Kiosk processing overview, blocked files, scan reports, process history; only write = Core module update source | Devices, device actions, logs, reports, Kiosk configuration (YARA / skip-by-hash) |
| Compatibility | Endpoints and authentication are different. Scripts / integrations built on the CM8 API must be rewritten. |

## **Remote Command**

| Item | CM8 | CM10 |
| ---- | ---- | ---- |
| **Remote support package** | N/A | SUPPORTED Generate / download a Kiosk support package remotely (Kiosk Windows 4.8.1+): Inventory > Devices > [Kiosk] > Actions > Generate Support Package, or Help Center > Support Packages. |
| **Remote script execution** | N/A | SUPPORTED Run PowerShell / cmd / bash / sh scripts now or on a schedule (Once / Daily / Weekly / Monthly), up to 500 instances per job (Kiosk 4.8.3+): Inventory > Scripts. |
| **Remote application update / rollback** | N/A | SUPPORTED  Update jobs with maintenance window, concurrency and auto-reboot; rollback to the previous version (Kiosk Windows 4.8.0+, Hardened Image 4.8.3+): Updates > Software > Kiosk > Jobs. |

## **New in CM10 (no CM8 equivalent)**

- **Deployment:** Windows MSI / RHEL RPM, distributed mode with MongoDB replica set, HA on AWS, scheduled backups, diagnostic data.
- **Product management:** policy objects with import / clone, auto-sync, staged module rollout, remote application update and rollback jobs, remote support packages, central certificate distribution, Skip by Hash, Password Storage, group license allocation, custom tags, Direct Instance Management API.
- **Endpoint Security:** MetaDefender Endpoint management, compliance policies, deep compliance, application control, playbooks, vulnerability management, endpoint discovery, rebranding of remediation pages, Endpoint Backup & Restore.
- **Patch Management:** OS and third-party patching (on-demand, policy, ring deployment incl. Patch Tuesday), SLA tracking, PDF reports.
- **Secure Access / NAC:** SDP (zero-trust access gateways), SAML / OIDC SSO, IdP MFA, access rules, RADIUS NAC (MetaDefender NAC v10).
- **Integrations:** Syslog CEF, Google Cloud Logging, webhooks, Splunk add-on;
- **Administration:** Hide / Read / Write RBAC with per-group / per-policy scoping, role-based session timeout, SCIM provisioning, richer audit logs.

> Note
>
> The "v8 vs v10" comparisons in the CM10 *Secure Access > NAC* docs refer to **MetaDefender NAC v8**, not Central Management v8.

## **Quick Guide: Common Kiosk Tasks in CM10**

| Task | CM8 steps | CM10 steps |
| ---- | ---- | ---- |
| Enroll a new Kiosk | On the Kiosk: Unmanaged → Server API URL + Registration Code → Enroll Now | CM10: *+Enroll Product* to get the Server API URL and Registration Code → enter them on the Kiosk (or during the Kiosk OOBE / setup wizard) |
| Change settings for all Kiosks in a group | Group > Configuration tab > *Edit* → *Apply Group Configuration*; or edit one Kiosk → *Set as Group Configuration* → *Apply Group Configuration* | *Peripheral Media Protection > Policies* → edit the policy (or *Import Policy* from a Kiosk) → SAVE + PIN → make sure the policy is assigned at *Inventory > Groups > [group] > Settings > Assign Policy* |
| Change one Kiosk only | Instance > Configuration > Edit | *Inventory > Devices > [Kiosk] > Settings > Edit* |
| Add a new Kiosk group | Products > Kiosk > Groups > Add New Group | *Inventory > Groups > Create New Group* → name, product type Kiosk, policy |
| Update engines on Kiosk (L-Series / Linux) | Settings > Products > Modules tab | *Updates > Modules* |
| Upgrade Kiosk software | Settings > Products > Products tab > Kiosk K-Series / L-Series Update | *Updates > Software > Kiosk > Jobs* → Create Update Job (rollback job if needed) |
| Add a Kiosk license | Licenses > Kiosk tab > Add | *License > Kiosk L-Series / K-Series > Add License* (select group; online only) |
| Get an email when a Kiosk is unhealthy / offline | Settings > Reports & Notifications > triggers | *Settings > Global > Notifications* → create a Notification Group (Kiosk availability event) → *Assign Group* or per group |
| View Kiosk scan activity | Products > Kiosk > Overview; Instance > Scan Reports | Peripheral Media Protection > Dashboard; *Inventory > Devices > [Kiosk] > Overview > Scan Sessions* |
| Create a read-only operator | Roles: View-Only | *User Management > Roles* → Read on required sections, Hide the rest |
| Collect logs for support | SSH + [cent-generate-sup-package.sh](http://cent-generate-sup-package.sh) (CM server) | Account menu > Help Center > Support Packages (tabs: Contact Support / Support Packages / Additional Resources); remote Kiosk support package (Kiosk Windows 4.8.1+) Run mocmSupportPackage.exe in CM installation folder to collect CM log |

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
