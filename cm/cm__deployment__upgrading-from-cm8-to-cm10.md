<!-- source: https://www.opswat.com/docs/cm/deployment/upgrading-from-cm8-to-cm10 -->

# Migration Plan: Upgrading from CM8 to CM10

The document provides an overview plan for all customers who are using My OPSWAT On-premise version 202x (also known as Central Management v8) to upgrade to My OPSWAT Central Management v10.

Depending on your data and current infrastructure, the migration time can be a day or several weeks.

## Prerequisites

1. Minimum Central Management v8 version: 2025.4.1
2. Minimum My OPSWAT Central Management v10 version: 10.3.2511

If you are using the older version, you need to upgrade to the minimum version to support the migration plan. For upgrade instructions, see:

- [Upgrade My OPSWAT](https://www.opswat.com/docs/myop/deployment/upgrade) for Central Management v8
- [Upgrading My OPSWAT Central Management ](https://www.opswat.com/docs/cm/deployment/upgrading-my-opswat-central-management)for My OPSWAT Central Management v10

## Plan Overview

Central Management v8 is deployed using an OVA-based appliance, whereas My OPSWAT Central Management v10 introduces support for MSI-based installation. Directly upgrading the OVA will not retain existing data. Therefore, a structured migration process is required to ensure data continuity and system integrity. Basically, you will need to install v10 on a separate server and migrate data from the v8 server to the v10 server.

There are 6 steps to migrate from v8 On-Prem to v10 On-Prem:

**Step 1:** Identify the use case and required features

**Step 2:** Determine the necessary data for migration

**Step 3:** Assess network requirements and prepare the environment

**Step 4:** Migrate the configuration settings and inventory data

**Step 5:** Migrate OPSWAT products

**Step 6:** Migrate historical data

The migration time can be an hour or several weeks, depending on the customer's use case and expectations.

## Plan Detail

### **Step 1:** Identify the use case and required features

Review the products currently in use and their usage.

- Using _____ MetaDefender Endpoint
- Using _____ MetaDefender Kiosk (Hardware / Software)
- Using _____ MetaDefender Core
- Using _____ MetaDefende ICAP
- Using _____ MetaDefende MFT
- Using _____ MetaDefende Drive
- Using _____ MetaDefende Sandbox
- Using _____ MetaDefende Media Firewall
- Using other products **___**

If you're using products that are not listed above, it means My OPSWAT Central Management 10 does not support integration with those products.

### **Step 2:** Determine the necessary data for migration

Review the required features.

- Using Proxy
- Using AD integration
- Using SSO
- Using HTTPS
- Using SMTP
- Using features in CM8 but not available in CM10:**___**
- Auto-reconnect MetaDefender Endpoints
- Able to re-deploy all MetaDefender Endpoints
- Keep all groups & Configuration
- Keep all Policy & Configuration
- Auto reconnect MetaDefende Core/Kiosk
- Keep Processing History in ____ days
- Keep Event Log in ____ days

> **Notice for License Migration**
>
> Your existing Central Management v8 licensing entitlement remains valid after migrating to My OPSWAT Central Management v10. No additional license purchase is required as part of the migration process.
>
> Please note that license information is not migrated automatically. After migration, you must re-add your existing product licenses to My OPSWAT Central Management v10.
>
> If you encounter any license-related issues, please contact [OPSWAT Support](https://www.opswat.com/support/contact-support) for assistance.

### **Step 3:** Assess network requirements and prepare the environment

It's important to assess network requirements and prepare the switching plan. Here are 3 common deployments. If you are not using one of them, please contact [OPSWAT Support](https://www.opswat.com/support/contact-support).

> **Warning**
>
> Do NOT switch at this step. Use the info on this step to prepare the environment only.

1. **Deployment A**: OPSWAT MetaDefender Products are connecting to CM8 FQDN.

If you are using an FQDN for v8. You can plan to update your local DNS to switch to the new IP of the v10 server. In this example:

- Before switching:
  - CNAME: [localdomain.opswat.com](http://localdomain.opswat.com)
  - IP: 192.168.200.10 **(current v8 IP)**
- After switching
  - CNAME: [localdomain.opswat.com](http://localdomain.opswat.com)
  - IP: 192.168.200.20 **(new v10 IP)**

![](https://uploads.developerhub.io/prod/97qW/dyy18qu98i0yuty0cr7cw9gn1dr76k3pl5n8euq3qo5enwpxt72fuzr7os25nskd.png)

2. **Deployment B**: OPSWAT MetaDefender Products connect to a reverse proxy. Redirect traffic from proxy to Central Management.

If you are using a reverse proxy. You can plan to update the rule to redirect from v8 IP to v10 IP:

![](https://uploads.developerhub.io/prod/97qW/qqkw4lqn0eszwirtw3j13nkim702kq857mlle4ybyhom6f1ae9ohvvrant8qx4o0.png)

3. **Deployment C**: OPSWAT MetaDefender Products connect directly to the Central Management IP Address

This deployment might have downtime since you need a plan to re-assign IP from the current v8 deployment to v10 server.

If it is not possible to retain the same network interface for all OPSWAT products when connecting to the new My OPSWAT Central Management v10, you will need to re-enroll those products into the new My OPSWAT Central Management IP.

![](https://uploads.developerhub.io/prod/97qW/vl7bml7l9bd7z3zb223dsapen4jb54nv23ab1fiqzwr3nru0ryd5zff86511yjzu.png)

If your current deployment matches one of these deployments. It's time to prepare the environment. Let's install CM10 on a separate server.

Follow the [Pre-Onboarding Setup](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-on-premises#pre-onboarding-setup) to install My OPSWAT Central Management v10. Don't forget to install the required software and prepare enough disk space based on the [System Requirement](https://www.opswat.com/docs/cm/deployment/system-requirements) document. Some common questions for your reference:

- [Why does My OPSWAT Central Management v10 stuck at loading?](https://www.opswat.com/docs/cm/knowledge-base/why-does-my-opswat-central-management-v10-stuck-at-loading-)
- [Why does OPSWAT Central Management v10 installation folder consume a lot of disk space?](https://www.opswat.com/docs/cm/knowledge-base/Why-does-OPSWAT-Central-Managementv10-installation-folder-consum)

> **Please Note**
>
> Ensure that the same Recovery Key and Registration Code are used for both Central Management v8 and v10. Using different credentials will result in the need to re-enroll all connected MetaDefender products.
>
> Additionally, verify that both v8 and v10 are operating within the same network environment. Update firewall rules as needed to allow MetaDefender products to communicate with v10 over ports **9000 and 443**. Note that the required ports may vary depending on your specific deployment configuration.

### **Step 4:** Migrate the configuration and inventory data

The configuration and inventory data include system configuration, user info, a list of enrolled products & configuration. You need to run the following steps to migrate data.

1.  Follow steps in [Import/Export - My OPSWAT Central Management v8 - Legacy](https://www.opswat.com/docs/myop/configuration/import-export) to backup Product Configurations and My OPSWAT Configurations

![](https://uploads.developerhub.io/prod/97qW/kl0jf9ati451djg1gtlr05x9xoruw0eo8y6oc2v1kc5zk5hvlonnxthoj5mn2ald.png)

> **Import Scope**
>
> Only** Product Configurations **and **My OPSWAT Configurations** are imported into CM10.  Nothing outside these areas is modified.
>
> - **Product Configurations**: MetaDefender instances, including their license information, instance configuration, and group configuration (imported into CM10 as policies)
> - **My OPSWAT Configurations**: Registration code, SMTP, server URL, and TLS/HTTPS
>
> Other data such as user accounts, logs, proxy settings, and unsupported product types (any product **other than **MK4, MK5, Core, or ICAP) **are not imported**. These data can be set up manually in CM10 if needed.

2. Download and run the CM8Importer on CM10 server to convert data

- Download the [CM8Importer](https://cm10-onpremise.s3.ap-southeast-1.amazonaws.com/cm8Importer/10726062_cm8importer.zip)
- Extract and copy the cm8importer to "CM10 installation location" <default in "**C:\Program Files\OPSWAT**">
- Copy the backupdate from step (i) to "CM10 installation location" <default in "**C:\Program Files\OPSWAT**">
- Put the backup file and CM8Importer.exe to the same folder
- Run the following command:
  - On Windows - Command Prompt

```powershell
$cm8importer -baseURL=”<CM10-URL + port>” -encryptionPassword=”<export file encrypted password>” -inputFile=”<export file path>”
```

3. Verify the active data

Waiting for the importing process. It's similar to this one

![](https://uploads.developerhub.io/prod/97qW/j49ipiauza1bjdk8o3xg7x7pgfjr3o489taahef0297a3q9ccnks5d7z1rlfukfw.png)

Active data includes system configuration, list of enrolled products & configuration. You would need to verify some important data as below

3.1. Verify the User Access

Try to access v10 with your credentials. You will need to reset the password and PIN on the first login. The master account is the most important account that you create when setting up the v10. Ensure you can log in as the master account and one imported account from the v8.

> **Info**
>
> If you are using SSO configuration or Active Directory. You can verify the integration after switching to v10. However, ensure that you can use the master account and one imported account from the v8 before going to the next step.

3.2. Verify the system configuration

Compare the configuration between v8 and v10. The UI can be different. For any values that exist in v8, they should be the same in v10. For any new configurations in v10, the default value will be set. You can contact [OPSWAT Suppor](https://www.opswat.com/support/contact-support)t if you need to clarify any configuration.

3.3. Verify the Inventory and Product Configurations

- Compare the list of product groups between v8 and v10
- Compare the list of MetaDefender Products between v8 and v10.

> **Info**
>
> In v8, all similar products belong to different Groups. Each group will have separate settings. The default value is set for any non-existent group settings from v8.

3.4. Verify the Set configuration and Policy Configuration

You can compare the individual product configuration by going to the product detail settings.

The Set setting will be migrated to Policy. You can compare the Set setting to the policy. For example, the Set Name will be converted to Policy Name.

### **Step 5:** Migrate the history data

This step will copy all the processing history scan data from v8 to v10.

> **Info**
>
> Migrating historical data involves copying records from v8 to v10. The duration of this process can vary significantly---from about an hour to several days or even weeks---depending on the size of your data. While this step may take time to complete, it does not block your deployment. You can either proceed with the next steps in parallel, wait until the migration finishes, or skip this step entirely by retaining the CM8 instance for historical queries.

1.  Login v8 Console ( version >= 2025.4.1 )
2. Navigate to Settings > Global > Data Migration
3. Enter the following info:
   1. My OPSWAT Central Management v10 URL
   2. Registration code
   3. Start Date & End Date
4. Click "Start Migration"
5. Then wait for the process

![](https://uploads.developerhub.io/prod/97qW/g88raevsj97kcam8dmc70xtb2x61cwls4vume81gqbdg8f5zcw958y9gg2co5qp5.png)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
