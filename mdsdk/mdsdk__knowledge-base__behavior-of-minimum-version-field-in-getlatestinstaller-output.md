<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/behavior-of-minimum-version-field-in-getlatestinstaller-output -->

# Behavior of minimum_version field in GetLatestInstaller output

This article is applied to OESIS Framework from version **4.3.5244 .0** and later releases deployed on Windows systems.

## [Background](/docs/mdsdk/knowledge-base/behavior-of-minimum-version-field-in-getlatestinstaller-output#background)

Previously, the `minimum_version` field in **GetLatestInstaller** (method `50300`) sometimes reported the OS version instead of the application version.

This article explains the logic of the `minimum_version` field in the GetLatestInstaller method output.

## [Logic and Behavior of the minimum_version field](/docs/mdsdk/knowledge-base/behavior-of-minimum-version-field-in-getlatestinstaller-output#logic-and-behavior-of-the-minimum_version-field)

The logic for the `minimum_version` field in **GetLatestInstaller** is now as follows:

### [1. For OS Patching (Signature 1103)](/docs/mdsdk/knowledge-base/behavior-of-minimum-version-field-in-getlatestinstaller-output#1-for-os-patching-signature-1103)

- **When** GetLatestInstaller is invoked with Windows Update Agent - signature `1103` (used for OS KBs):

  - **Then** `minimum_version` shows the OS version (retrieved via detection).

### [2. For Microsoft products that follow System Patching Workflow](/docs/mdsdk/knowledge-base/behavior-of-minimum-version-field-in-getlatestinstaller-output#2-for-microsoft-products-that-follow-system-patching-workflow)

- **When** GetLatestInstaller is invoked with signatures supported with System Patching Workflow (see [the list of supported Microsoft Applications](/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support#supported-operating-systems--applications) or look for the `"support_system_patch": true` flag in the product definition in file `analog.zip/analog/server/products.json`):

  - **Then** `minimum_version` shows the current version of the Microsoft product (detected version).

### [3. For the 3rd-party product Patching](/docs/mdsdk/knowledge-base/behavior-of-minimum-version-field-in-getlatestinstaller-output#3-for-the-3rd-party-product-patching)

- **When** GetLatestInstaller is invoked with signatures of 3rd party products (any products not covered by the cases above):

  - **Then** `minimum_version` shows the version extracted from download links (matches the current description of minimum_version).

## [Known Issues & Limitations](/docs/mdsdk/knowledge-base/behavior-of-minimum-version-field-in-getlatestinstaller-output#known-issues--limitations)

- Patching workflow for .NET is still tied to signature 1103 and will be fixed in the near future.

## [FAQ](/docs/mdsdk/knowledge-base/behavior-of-minimum-version-field-in-getlatestinstaller-output#faq)

**Q: How is the OS version detected for minimum_version?**

A: The OS version is retrieved via the GetVersion method in our SDK.

**Q: How do I check if a signature is** **supported with System Patching Workflow?**

A: A signature is considered supported with System Patching Workflow if it exists in [Supported Operating Systems & Applications](/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support#supported-operating-systems--applications) table and its entry in the file `analog.zip/analog/server/products.json` is marked with `"support_system_patch": true` .

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
