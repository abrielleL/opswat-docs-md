<!-- source: https://www.opswat.com/docs/cm/product-management/generate-support-package -->

# Generate Support Package

This comprehensive guide provides step-by-step instructions on how to generate, monitor, and download support packages for product instances from My OPSWAT Central Management.

- [When to use a support package](https://www.opswat.com/docs/cm/product-management/generate-support-package#when-to-use-a-support-package)
- [Supported products](https://www.opswat.com/docs/cm/product-management/generate-support-package#supported-products)
- [Remote support package generation](https://www.opswat.com/docs/cm/product-management/generate-support-package#remote-support-package-generation)
  - [Step 1: Generate support package](https://www.opswat.com/docs/cm/product-management/generate-support-package#step-1-generate-support-package)
  - [Step 2: Monitor package generation status](https://www.opswat.com/docs/cm/product-management/generate-support-package#step-2-monitor-package-generation-status)
  - [Step 3: Download a package](https://www.opswat.com/docs/cm/product-management/generate-support-package#step-3-download-a-package)
  - [Step 4: Contact OPSWAT Support](https://www.opswat.com/docs/cm/product-management/generate-support-package#step-4-contact-opswat-support)
- [Storage limits and retention](https://www.opswat.com/docs/cm/product-management/generate-support-package#storage-limits-and-retention)
- [Troubleshooting](https://www.opswat.com/docs/cm/product-management/generate-support-package#troubleshooting)

## **When to use a support package**

Create a support package when you are working with OPSWAT Support on issues such as service failures, unexpected behavior, connectivity problems, configuration issues, or product-side errors that require deeper investigation.

- **For My OPSWAT Central Management on-premises**: generate a package from My OPSWAT Central Management server to collect logs and configuration data. Refer to [specific guideline.](https://www.opswat.com/docs/cm/knowledge-base/how-to-generate-a-support-package-for-my-opswat-central-manageme)
- **For supported managed products**: generate a package remotely from My OPSWAT Central Management console and then download it after processing completes.

## **Supported products**

- MetaDefender Core: version 5.19.0 or later
- MetaDefender Kiosk Windows: version 4.8.1.xxxx or later

## **Remote support package generation**

**Before you begin**

- Make sure the target product version supports remote support package generation.
- Make sure the target instance is enrolled, active, and connected to My OPSWAT Central Management.
- Make sure your user account has access to the relevant product inventory or Help Center workflow.

### **Step 1: Generate support package**

#### **A. From Help Center > Support Package**

**Navigation:** User profile dropdown > Help Center > Support package tab > Generate Support Package

1. Select the supported product type.
2. Choose the appropriate product and timeframe, if prompted.
3. Click **Generate**.

![](https://uploads.developerhub.io/prod/97qW/r4c6sv0nyxo6zd943ro72i1byta0xgtngrb3zcn6vjpxbzxp54eo5417uvi2mdc2.png)

#### **B. From Product Instance Details > Support Package**

**Navigation**: Inventory > Product Instance Details > Action menu > Generate Support Package

1. Select the supported product type.
2. Choose the timeframe, if prompted.
3. Click **Generate**.

![](https://uploads.developerhub.io/prod/97qW/qz4s8fb8xrdu5iidkd2q1ex03oo2y3quonay5bixg9pchfaqy55fx0h2dy98di0v.png)

### **Step 2: Monitor package generation status**

**Navigation**: User profile dropdown > Help Center > Support package tab

Track the Status until processing completes.

- **In Queue**: Waiting for the instance to pick up request.
- **Pending**: Request has been accepted and is waiting to be processed.
- **In Progress**: The managed instance is generating or uploading the package.
- **Download Available**: The package is ready to download.
- **Failed**: The package could not be generated or uploaded successfully.

![](https://uploads.developerhub.io/prod/97qW/1aora1sne0kki28cd8t998y1wufoyva45pizn0chm3m7fq423fkzwp6r3uaa6wih.png)

### **Step 3: Download a package**

Once generation finishes successfully, the package can be downloaded from My OPSWAT Central Management.

1. Select the download action.
2. Save the file locally and confirm that the archive opens correctly.

### **Step 4: Contact OPSWAT Support**

After generating the package, [open a support case](https://www.opswat.com/support/contact-support) and attach the support package or requested log archive.

### **Delete a package**

Administrators can delete packages from the interface when they are no longer needed.

1. Open the support package list in My OPSWAT Central Management.
2. Locate the package you no longer need.
3. Select the delete action.

## **Storage limits and retention**

Support package management uses smarter storage controls to keep package history manageable.

- A maximum of **2 support packages per instance** is retained.
- When a new package is created beyond this limit, older packages are automatically cleaned up.
- Cleanup behavior follows your configured data retention settings.

## **Troubleshooting**

- **If generation takes a long time:** Large log sets can increase package creation time.
- **If a package fails:** Verify that the instance is online, connected to My OPSWAT Central Management, and running a supported version.
- **If a device restarts during generation:** The request may fail and need to be created again.
- **If network connectivity is interrupted:** My OPSWAT Central Management may retry depending on the product workflow, but you should verify the final status.
- **If storage is full:** Remove older packages you no longer need before creating new ones.
