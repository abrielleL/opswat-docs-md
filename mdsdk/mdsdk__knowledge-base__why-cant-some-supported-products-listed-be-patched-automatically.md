<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/why-cant-some-supported-products-listed-be-patched-automatically -->

# Why can’t some supported products listed be patched automatically?

## [Overview](/docs/mdsdk/knowledge-base/why-cant-some-supported-products-listed-be-patched-automatically#overview)

OPSWAT SDK provides patching capabilities for 3rd party applications to ensure they remain up to date and secure. However, not all applications can be patched in the same way. This article explains the two types of patching conducted by the OPSWAT SDK and why some products cannot be patched despite being supported.

## [Types of Patching](/docs/mdsdk/knowledge-base/why-cant-some-supported-products-listed-be-patched-automatically#types-of-patching)

The OPSWAT SDK supports two types of patching:

1. **Automatic Patching:** The SDK can apply updates/patches without user intervention. The patching process is executed automatically once a new version or a patch that fixes a vulnerability is available.
2. **Manual Patching:** We provide the option to retrieve the download URL and install the installer manually. Customers simply need to download it and proceed with installation using our method.

## [Why Some Products Cannot Be Patched Automatically](/docs/mdsdk/knowledge-base/why-cant-some-supported-products-listed-be-patched-automatically#why-some-products-cannot-be-patched-automatically)

Even though certain products are supported for patching, the method of patching depends on how the software vendor distributes updates. Some applications, like 7-Zip (arm64) or 7-Zip MSI (x64), support both automatic and manual patching. Others, like 360 Total Security, only support manual patching, meaning users must download and install the latest version manually.

## [Reasons Why Some Applications Are Manual Patch Only](/docs/mdsdk/knowledge-base/why-cant-some-supported-products-listed-be-patched-automatically#reasons-why-some-applications-are-manual-patch-only)

1. **Vendor Update Mechanism:** Some software vendors do not allow automatic patching and require user intervention for installation.
2. **Custom Installation Requirements:** Certain applications require specific installation steps, license agreements, or user input that prevent automation.
3. **Security or Compliance Policies:** Some vendors restrict automatic patching to prevent unauthorized updates.

## [Reference](/docs/mdsdk/knowledge-base/why-cant-some-supported-products-listed-be-patched-automatically#reference)

For a comprehensive list of 3rd party applications supported for patching by OPSWAT SDK, please visit [this page](https://www.opswat.com/products/metadefender/endpoint-security-sdk/patch-management?utm_campaign=APJ_VN_Search_OPSWAT_B_PM&utm_source=google&utm_medium=paid_search&utm_content=vietnam&utm_term=my%20opswat).
