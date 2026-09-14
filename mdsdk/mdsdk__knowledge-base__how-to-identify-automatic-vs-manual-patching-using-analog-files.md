<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-identify-automatic-vs-manual-patching-using-analog-files -->

# How to Identify Automatic vs Manual Patching Using Analog Files

This article explains how to distinguish between **automatic patching** and **manual patching,** both on the client and server sides.

## [**Automatic vs Manual Patching**](/docs/mdsdk/knowledge-base/how-to-identify-automatic-vs-manual-patching-using-analog-files#automatic-vs-manual-patching)

| **Patching Type** | **Description** |
| --- | --- |
| **Automatic patching** | Products that support both **downloading** and **installing** patches through the following methods:   - `GetProductPatchLevel` - `GetLatestInstaller` - `InstallFromFiles` |
| **Manual patching** | Products where **GetLatestInstaller** is **not supported**, and only the following methods can be used:   - `GetProductPatchLevel` - `InstallFromFiles` |

In short:

- **Automatic patching** → `GetLatestInstaller` **+** `InstallFromFiles` are supported.
- **Manual patching** → only `InstallFromFiles` works for installation, while `GetProductPatchLevel` is available in both cases.

Info

By default, for any signature in our database, `GetLatestInstaller` supports both download values, 0 and 1.

Exceptions apply only to specific signatures that do not support `download=0` (i.e., they can’t return a URL but can still be downloaded).

---

## [**Client-Side Information**](/docs/mdsdk/knowledge-base/how-to-identify-automatic-vs-manual-patching-using-analog-files#client-side-information)

At the client side, you can use the **patch.dat** file to identify which products are supported for third-party patching and how they are categorized. When you load this file using `LoadPatchDatabase`, it lists all signatures (products) that are supported for 3rd-party patching.

The following fields help you distinguish between automatic and manual patching:

| **Field** | **Description** |
| --- | --- |
| `details.support_signatures` | Lists all third-party signatures where all methods (`GetLatestInstaller`, `InstallFromFiles`, and `GetProductPatchLevel`) are fully supported - **automatic patching**. |
| `details.support_install_signatures` | Lists signatures where only `InstallFromFiles` and `GetProductPatchLevel` are supported - **manual patching**. |
| `details.self_update_signatures` | Lists signatures where automatic patching is supported, but only for installer download (not URL). |

### [New: download=2 Parameter](/docs/mdsdk/knowledge-base/how-to-identify-automatic-vs-manual-patching-using-analog-files#new-download2-parameter)

We have recently introduced support for the parameter `download=2` in `GetLatestInstaller`. This means that for signatures listed in **support_signatures** and **self_update_signatures**, the SDK can now return the **patch_id** that will be used to install the product.

This allows better mapping and handling of installation workflows.

---

## [**Server-Side Information**](/docs/mdsdk/knowledge-base/how-to-identify-automatic-vs-manual-patching-using-analog-files#server-side-information)

At the server side, you can check patching support using the following files from the analog.zip package:

| **File** | **How to Use** | **Description** |
| --- | --- | --- |
| **products.json** | Check if the product has `system_patching` or `3rd_party_patching` set to **true**. | If either value is `true`, the product supports **automatic patching**. If both are `false`, the product is **manual**. |
| **products.json** | Review the field `"usable_download_link": true/false` | This indicates whether the product supports retrieving the installer URL (`download_0`). If it’s set to `false`, only installer retrieval is supported. |

Support

If you need more guidance on how to use analog files or interpret patching information, refer to our **How_to_use_Analog_files guide** or [contact OPSWAT Support for assistance](https://my.opswat.com/support).
