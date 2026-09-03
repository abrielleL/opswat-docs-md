<!-- source: https://www.opswat.com/docs/my/release-notes/v2026-3-2 -->

# v2026.3.2 - Jul 28th

| **Version** | v2026.3.2.0 |
| ---- | ---- |
| **Release date** | July 28th, 2026 |
| **Release Summary** | This release introduces **Hardware RMA Requests**, enabling you to request a return or replacement for defective OPSWAT hardware directly in My OPSWAT Portal. The Support experience has also been enhanced with the addition of **follow-up cases** for long-closed tickets. Moreover, partners will now benefit from automated **Deal Registration status emails** at every stage of the pipeline. |

### New Features

#### **Hardware RMA Requests**

Customers can now submit hardware RMA (Return Merchandise Authorization) requests directly in My OPSWAT Portal, then track status and communicate with OPSWAT on each request from the Support page.

![](https://uploads.developerhub.io/prod/JYvy/xa62dq3nvtkui3df3jdjtrw4crilp8ahqxjhvzcdjw9raud5hhkunmhe28m46fgb.png)

Partners can submit requests on behalf of their customers. 

![](https://uploads.developerhub.io/prod/JYvy/em7jpgq1vb2gfr1yqkymupr08g8836nyc2hflrwb1q096pyudo5mb8o5jbz7h47g.png)

> **Please note:**
>
> You need Full Access to **Support Service - RMA Cases** permission to submit RMA requests, View Only permission to view existing RMA cases. If you do not see the RMA options described below, ask your organization administrator to grant this permission.

**Further reading:** [Hardware RMA Requests](https://www.opswat.com/docs/my/support-services/hardware-rma-requests)

---

#### **Submit a Follow-Up Case for Closed Cases**

![](https://uploads.developerhub.io/prod/JYvy/cvase22fe7p9yve7mwio6s6isq2zjlzeg13cea5xnhl6zoft803ns3q6afwqyvr1.png)

You can now open a follow-up case for a support case that has been closed for more than 14 days and can no longer be reopened.

---

---

#### **[For Partners] Deal Registration Stage Email Notifications**

Partners now receive automated email notifications as a registered deal moves through each pipeline stage.

---

### **Enhancements**

#### **Inline Images in Case Descriptions and Comments**

You can now paste or insert images directly inside the **Description** field when submitting a support case, and inside comments on an existing case.

---

#### **Trust Center Update Subscription**

You can now subscribe to Trust Center updates from **My Information > Preferences**. Opt in to receive notifications about new documents, changes to subprocessors, and other updates to the OPSWAT Trust Center.

**Access path:** My Information > Preferences

---

#### **Optional Scan Results in False Detection Reports**

Scan results are no longer required when reporting a false detection for products that cannot export them. The scan results upload is now optional for MetaDefender Cloud, MetaDefender  ICAP, MetaDefender  Kiosk, and MetaDefender Managed File Transfer, and remains required for MetaDefender Aether and Core.

---

#### **Masked License Keys in Support Cases**

License keys shown in support case details are now masked, displaying only 2 final segments (8 characters) of the key. This protects sensitive license information while still letting you identify the relevant license.

---

### **Bug Fixes**

** **Bug fixes** Submit A Case Button Now Always Available**

Fixed an issue where the **Submit A Case** button was hidden for some users until several seconds after starting a chat, making it hard to find how to open a case. The button is now always visible to all users.
