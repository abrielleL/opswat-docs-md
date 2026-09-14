<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently -->

# How Can I Update The Engine Data More Frequently

## [Background](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#background)

The SDK Engine is delivered as two primary packages:

- **Engine Package**: which contains all the binaries of the SDK.
- **Data Package**: which contains the Scripts, Data, Support Charts, Integration Notes, etc. used by the SDK Engine for the Application Detection, Application Orchestration, and Compliance features.

**Notes:**

- There are a handful of other supporting packages available in the OEM Portal (such as Release Notes, Package Signatures, etc.), but this effort is focused only on the Engine and Data Packages.
- Data for other SDK Features (such as Vulnerability Assessment and Patching) is already provided separately.
- The full set of packages (including the Engine and Data Packages) is published on the OEM Portal every week (on Tuesdays) as a complete set.

## [Goal](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#goal)

The goal of this effort is to decouple the delivery of the Engine Package and Data Package, such that:

- We will deliver the Data Package multiple times per day,
- We will not require a corresponding Engine Package update when publishing the Data Package updates,
- We will make it easy for Customers to retrieve the Data Package independent of the Engine Package,
- We will not break backward compatibility for Customers who choose to download the packages as they do today.

## [The Data Package](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#the-data-package)

The Data Package comes in two flavors:

1. The **legacy Data Package** that can be downloaded either from the OEM Portal or using the OesisPackageLinks.xml method.

   - **Note that there are no changes to the format or processing of this Data Package.**
2. The **new Data Package** that can be downloaded either via the VCR Gateway or accessed inside the Analog Package.

### [The New Data Package (compliance.zip)](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#the-new-data-package-compliancezip)

The new version of the Data Package is a file named “compliance.zip” and contains a Data File for each platform (Windows, macOS, Linux, …)

The Data File (inside the Data Package) is a single file available per platform+architecture:

- compliance/**windows**/bin/libwaresource.dll
- compliance/**mac**/bin/libwaresource.dylib
- compliance/**linux**/bin/**arm64**/libwaresource.so
- compliance/**linux**/bin/**x64**/libwaresource.so
- compliance/**linux**/bin/**x86**/libwaresource.so

## [Data Package Downloading](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#data-package-downloading)

There are four different ways to download the Data Package:

### [1. OEM Portal](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#1-oem-portal)

This is the legacy method for downloading the legacy Data Package.

It requires having a MyOPSWAT Portal Account which is enabled for access to the OEM Portal.

From there, a user can download the various SDK Packages, including the legacy Data Package.

**Notes:**

- The SDK Packages that are available via the Portal are only updated weekly.
- **The format of this Data Package has not changed, and processing it has not changed.**

### [2. OesisPackageLinks.xml](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#2-oesispackagelinksxml)

This is another legacy method for downloading the legacy Data Package.

**WARNING**: We have stopped posting this XML file in a public location. Going forward, anyone wanting to continue using this XML file to download packages must get a token from us.

The XML file has moved behind the VCR Gateway:

- Old Link: <https://software.opswat.com/OESIS_V4/OesisPackageLinks.xml>
- New Link: [https://vcr.opswat.com/gw/file/download/OesisPackageLinks.xml?type=1&token=<access_token>](https://vcr.opswat.com/gw/file/download/OesisPackageLinks.xml?type=1&token=%3caccess_token%3e)

**Notes:**

- The SDK Packages that are available via the XML links are only updated weekly.
- **The format of this Data Package has not changed, and processing it has not changed.**

### [3. VCR Gateway](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#3-vcr-gateway)

To download the new Data Package (published multiple times per day), you may use the VCR Gateway via this URL:

- [https://vcr.opswat.com/gw/file/download/compliance.zip?type=1&token=<access_token>](https://vcr.opswat.com/gw/file/download/compliance.zip?type=1&token=%3Caccess_token%3E)

**WARNING**: using this method will require a VCR Gateway token to be provided, if you do not already have one.

### [4. Analog](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#4-analog)

For customers already using Analog, the new Data Package is now provided inside Analog.

In Analog there is a new set of folders to extract the Data File:

- analog/client/compliance/**windows**/bin/libwaresource.dll
- analog/client/compliance/**mac**/bin/libwaresource.dylib
- analog/client/compliance/**linux**/bin/**arm64**/libwaresource.so
- analog/client/compliance/**linux**/bin/**x64**/libwaresource.so
- analog/client/compliance/**linux**/bin/**x86**/libwaresource.so

## [What You Need To Do](/docs/mdsdk/knowledge-base/how-can-i-update-engine-data-more-frequently#what-you-need-to-do)

If you want to take advantage of the more-frequent Data Package updates, here are the changes you will need to make:

1. Download the new Data Package from the VCR Gateway (or use Analog).
2. Extract the appropriate Data File (libwaresource) from the Data Package using the new folder organization.
3. Distribute libwaresource to each endpoint.
4. Copy libwaresource into the main Engine folder that the Engine was installed to.

**Notes:**

- In-order to properly update this data file (libwaresource) the SDK will need to be exited before replacing libwaresource (via wa_api_teardown).
- Once the data file has been replaced, the SDK can be restarted (via wa_api_setup).
- This is in-keeping with the current method to update libwaresource outside of a normal engine update.
