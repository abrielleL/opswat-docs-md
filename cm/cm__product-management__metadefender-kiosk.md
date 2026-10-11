<!-- source: https://www.opswat.com/docs/cm/product-management/metadefender-kiosk -->

# Enroll MetaDefender Kiosk

Enrolling MetaDefender Kiosk instances into My OPSWAT Central Management centralizes your oversight and standardizes security controls across your infrastructure.

**In This Guide**

- [Auto Enroll MetaDefender Kiosk (On-Premise Deployment)](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk#auto-enroll-metadefender-kiosk-on-premise-deployment)
  - [Step-by-step Instructions](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk#step-by-step-instructions)
- [Manual Enroll MetaDefender Kiosk (All Deployments)](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk#manual-enroll-metadefender-kiosk)
  - [Step-by-step Instructions](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk#step-by-step-instructions)

## Auto Enroll MetaDefender Kiosk (On-Premise Deployment)

The Auto Enrollment feature allows MetaDefender Kiosk to discover **My OPSWAT Central Management On-Premises** server on the same local network and submit an enrollment request automatically.

![](https://uploads.developerhub.io/prod/97qW/iyx9jy98wt3yhknl3rdmghjoquaemj027o0anezcopdy0gn078ixedxzonhbsqs8.png)

Note This feature requires My OPSWAT Central Management On-Premises version 10.7.26092 or later.

### **Step-by-step Instructions**

- Log in to the My OPSWAT Central Management console.
- Click Enroll Product to open the enrollment management interface.
- Review the pending Kiosk enrollment requests and take one of the following actions:
  - **Approve an Enrollment Request**:** **Select the device and click **Approve**. The Kiosk completes enrollment and connects to My OPSWAT Central Management on its next check-in.
  ![](https://uploads.developerhub.io/prod/97qW/gncana7nwvl77gnvvcakibyiekughcbzr0a6jpvt5khroch3cvyjg099l0oglr6r.png)
  - **Assign to a Group**: Select or assign a **Group** for the approved Kiosk to apply predefined configuration and policies.
  ![](https://uploads.developerhub.io/prod/97qW/vy7qs5hil7cp1p6z1q9dy34rmhqcehuy90okg8isgf7hab8ntkx33grn7lulgvjj.png)
  - **Reject an Enrollment Request**: If a request is unexpected, duplicate, or misconfigured, click **Reject** to dismiss it from the pending list.

- ![](https://uploads.developerhub.io/prod/97qW/a9e2a9ry79ys2uakg8e6ibzltcmoxrmt11z5b0054nngznc45o3da0reo139y4ne.png)
  - **Block a Device**: Block device from automatically request enrollment.
  ![](https://uploads.developerhub.io/prod/97qW/bq0cedpqddozzqh3zo29pirxtvxbkgu4kzda9crapeld2a685tektjn0r163lylb.png)

## Manual Enroll MetaDefender Kiosk (All Deployments)

This method to enroll MetaDefender Kiosk works for both SaaS and On-Premises deployment.

### **Step-by-step Instructions**

1. Log in to the My OPSWAT Central Management console.
   - Click Enroll Product to open the enrollment management interface.
   - Choose **MetaDefender Kiosk** from the Product Type drop down list.
   - Copy the provided **Server URL** and **Registration Code**.
   ![](https://uploads.developerhub.io/prod/97qW/rjpa6xj8846mmv376n0tvlesymbtxzgohyv1djoxhq1abi5m1ogw8miir9v36huo.png)
2. Log in to **MetaDefender Kiosk Management Console**.
   - Select the **Unmanaged** button in the top-right corner.
   - Enter the **Server URL** and **Registration Code** from Step 1.
   - Select **Enroll Now**.

![](https://uploads.developerhub.io/prod/97qW/5vdpf1lzedqy3t5vrpk58axsuy2bhab1hmka8fukv5lk2uatz96umxmi67djtwiv.png)

Once connected, the Kiosk status will change to "**Product is Managed**”.

![](https://uploads.developerhub.io/prod/97qW/p3oxhx8lwcq7v8jwo5jryve9dihkwviqrhlr3nyurnjtjfu9yphlqnzl59yy30cf.png)

Once installation is complete, navigate to **Inventory > Devices** in My OPSWAT Central Management console to verify that the instance is active.

### Kiosk OOBE Setup Wizard [During Installation]

The MetaDefender Kiosk Out-of-box Experience (OOBE) Setup Wizard allows for immediate enrollment during initial configuration.

- Navigate to the enrollment step within the OOBE Setup Wizard.
- Input the **Registration Code** and **Server URL**. Refer to [Step 1: Retrieve Enrollment Details](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk#step-1-retrieve-enrollment-details) for guidance.
- Select **Enroll** to finalize the connection.

Once installation is complete, navigate to **Inventory > Devices** in My OPSWAT Central Management console to verify that the instance is active.

![](https://uploads.developerhub.io/prod/97qW/gh2gt1ofbe402dha9hd7mnjrvnrowzexfrnrdpvwwfz21uwxys0y7e8nh2adz99s.png)

### Kiosk Setup Wizard [During Installation]

The MetaDefender Kiosk Setup Wizard offers immediate enrollment into My OPSWAT Central Management during installation.

- Navigate to the enrollment step within the Setup Wizard.
- Input the **Registration Code** and **Server URL**. Refer to [Step 1: Retrieve Enrollment Details](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk#step-1-retrieve-enrollment-details) for guidance.
- Select **Enroll** to finalize.

![](https://uploads.developerhub.io/prod/97qW/i0tu3awlpetlcibsqvln9qc1mm4ld307j6k2nzfus5c24ze4uzozw1xl2va2sok1.png)

Once installation is complete, navigate to **Inventory > Devices** in My OPSWAT Central Management console to verify that the instance is active.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
