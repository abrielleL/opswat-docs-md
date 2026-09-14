<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua -->

# Understanding GetMissingPatches output when invoking with Windows Update Agent (WUA)

This article is applied to MetaDefender Endpoint Security SDK releases on **Windows** with **Windows Update Agent (WUA)** Integration.

## [**Overview**](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#overview)

The `GetMissingPatches` method, when invoking with **Windows Update Agent (WUA)** (Signature: 1103), works directly with Microsoft’s WUA API. Our SDK sends the appropriate input parameters to Microsoft’s API, retrieves the results, and then converts them into a **standardized output format**. This standardized output is returned as the `json_out` **object** of the `GetMissingPatches` method.

This article provides a detailed explanation of the fields included in the **GetMissingPatches** `json_out` **object**, helping you correctly interpret their values and integrate them into your application.

---

## [**Sample output**](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#sample-output)

Below is the sample output of **GetMissingPatches** (method 1013) when using with WUA (signature 1103).

json_outCopy{
"result" : {
"method" : 1013,
"code" : number,
"timing" : number,
"timestamp" : string,
"patches": [
{
"id": string,
"title": string,
"description": string,
"revision": number,
"product": string,
"vendor": string,
"severity": string,
"category_id": string,
"category": string,
"category_description": string,
"category_parent": string,
"security_update_id": string,
"kb_id": string,
"date": string,
"size": number,
"reboot_required": boolean,
"optional": boolean,
"deployment_action": number,
"preview_patch": boolean
},
...
],
"patches_source": string
}
}

We will skip the fields `method`, `code`, `timing`, and `timestamp`, as they are basic outputs of every method in the SDK.

---

## [**Understanding patches_source**](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#understanding-patches_source)

According to [Microsoft’s documentation](https://learn.microsoft.com/en-us/windows/deployment/update/how-windows-update-works#identifies-service-ids), Windows Update Agent (WUA) can query updates from several different sources. The `patches_source` field indicates which source is being used. Possible values might include:

| **Possible Values** | **Description** |
| --- | --- |
| `"Windows Update"` | The default source of the Windows Update Agent. |
| `"Microsoft Update"` | Provides updates for a wider range of Microsoft products (e.g., .NET, PowerShell), in addition to the updates from Windows Update. This value appears if the user has enabled **“Receive updates for other Microsoft products”** or if mode `0` is selected as the input for `GetMissingPatches`. |
| `"WSUS or Configuration Manager"` | This value will appear when the WUA is working with the WSUS server or Configuration Manager that is set up for the endpoint system. |
| File path to `wsusscn2.cab` | When using WUA in offline mode, `patches_source` will contain the file path of the `wsusscn2.cab` file that the SDK is working with. Typically, this file is located at `%SystemDrive%\wsusscn2.cab`. |
| `"Unknown"` | If the source does not fall into any of the categories mentioned above, it will be classified as `Unknown`. |

## [**Understanding patches' fields**](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#understanding-patches-fields)

The patches object contains a list of patch entries. Each entry provides details for a single missing update.

The detailed fields are **reported directly from Microsoft’s WUA API**, while others are **processed by SDK logic** to ensure consistency for a standardized output.

Warning

Some fields are only included in the `json_out` if the SDK is able to retrieve data for them. If no information is available, the field will simply **not appear** in the output.

### [**1. Fields reported directly from WUA API**](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#1-fields-reported-directly-from-wua-api)

These values are passed directly from Microsoft’s WUA API without modification.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `id` | string | Unique ID of the update. | `"b612df79-0a67-4ef5-80b3-3cc051ce8ee9"` |
| `title` | string | Title of the update. | `"Windows 11, version 24H2"` |
| `description` | string | Description of the update. | `"Install the latest version of Windows: Windows 11, version 24H2."` |
| `revision` | integer | Revision number of the update. | `1` |
| `product` | string | Product this update applies to. (Currently always empty.) | `""` |
| `category_id` | string | ID of the update’s category. | `"3689bdc8-b205-4af4-8d4a-a63924c5e9d5"` |
| `category` | string | Category to which the update belongs. See the [Category Values table](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#category-values) below for possible values. ([Reference](https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/configure-classifications-and-products)) | `"upgrade"` |
| `category_description` | string | Description of the update’s category. | `"A new product release bringing a device to the next version..."` |
| `category_parent` | string | Parent category name. | – |
| `security_update_id` | string | Associated security bulletin IDs. | – |
| `kb_id` | string | Knowledge Base (KB) article IDs. | `"5055523"` |
| `date` | string | Last published date (UTC, epoch format). | `"1744070400"` |
| `size` | integer | Maximum download size of the update in bytes. | `2112397348` |
| `reboot_required` | boolean | Whether update requires restart. | `false` |
| `deployment_action` | integer | Numeric code of deployment action for the update.  See the ” [DeploymentAction Values](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#deploymentaction-values) table below or [Microsoft's documentation](https://learn.microsoft.com/en-us/windows/win32/api/wuapi/ne-wuapi-deploymentaction) for possible values. | `1` |

#### [Category Values](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#category-values)

The values from `patches[].category` in the SDK output is based on the WUA update classifications defined in [Microsoft's documentation](https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/configure-classifications-and-products). For convenience, the key values are summarized below.

| **Value** | **Description** |
| --- | --- |
| `"critical_update"` | Specifies a widely released fix for a specific problem that addresses a critical, non-security-related bug. |
| `"definition_update"` | Specifies a widely released and frequent software update that contains additions to a product's definition database. |
| `"feature_pack"` | Specifies new product functionality that is first distributed outside of a product release and that's typically included in the next full product release. |
| `"security_update"` | Specifies a widely released fix for a product-specific, security-related vulnerability. |
| `"service_pack"` | Specifies a tested, cumulative set of all hotfixes, security updates, critical updates, and updates that are applied to a product. Additionally, service packs may contain additional fixes for problems that are found internally since the release of the product. |
| `"tool"` | Specifies a utility or feature that helps to complete one or more tasks. |
| `"update_rollup"` | Specifies a tested, cumulative set of hotfixes, security updates, critical updates, and updates that are packaged together for easy deployment. An update rollup generally addresses a specific area, such as a security or product component. |
| `"update"` | Specifies a widely released fix for a specific problem. An update addresses a non-critical, non-security-related bug. |
| `"upgrade"` | Specifies an upgrade for Windows 10 or later features and functionality. These updates are also known as feature updates for Windows operating systems. |
| `"unknown"` | In case the SDK fails to get the category of the update, it will be unknown. |

#### [DeploymentAction Values](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#deploymentaction-values)

`patches[].deployment_action` field in the SDK output is passed directly from the Microsoft Windows Update Agent (WUA) API without modification.

The numeric values map to the WUA constants defined in [Microsoft's documentation](https://learn.microsoft.com/en-us/windows/win32/api/wuapi/ne-wuapi-deploymentaction). For convenience, the key values are summarized below.

| Value | Identifier | **Description** |
| --- | --- | --- |
| `0` | `daNone` | No explicit deployment action is specified on the update. The update inherits the value from its bundled updates. |
| `1` | `daInstallation` | The update should be installed on the computer and/or for the specified user. |
| `2` | `daUninstallation` | The update should be uninstalled from the computer and/or for the specified user. |
| `3` | `daDetection` | The update is deployed only to determine the applicability of the update. The update will not be installed. |
| `4` | `daOptionalInstallation` | The update may be installed on the computer and/or for the specified user. |

### [**2. Fields require further processing by SDK**](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#2-fields-require-further-processing-by-sdk)

These fields require additional processing by the SDK to interpret or normalize values.

#### [vendor](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#vendor)

- **Type:** string
- **Description:** The vendor that provides this update.
- **Logic:**

  - This field will be omitted if the update a **Driver Update**.
  - `"Microsoft Corporation"` if the update is not a driver update and source is **Windows Update/Microsoft Update**.
  - `"unknown"` if the source is **WSUS/Configuration Manager**.

#### [severity](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#severity)

- **Type:** string
- **Description:** This will fetch the Microsoft Security Response Center severity rating of the update.
- **Logic:**

  - This field is primarily reported from WUA API via `IUpdate::get_MsrcSeverity` ([Reference from Microsoft](https://learn.microsoft.com/en-us/windows/win32/api/wuapi/nf-wuapi-iupdate-get_msrcseverity#remarks)).
  - If severity cannot be retrieved, SDK classifies based on the update category.

Info

For a detailed explanation of how the SDK determines update severity, please refer to the dedicated article: [How OESIS determines Severity of GetMissingPatches for WUA](/docs/mdsdk/knowledge-base/how-sdk-determine-the-severity-of-getmissingpatches-for-wua)

#### [optional](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#optional)

- **Type:** boolean
- **Description:** Indicates if this is an optional update.
- **Logic:**

  - This field is derived from `deployment_action` field. Check the [DeploymentAction Values](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#deploymentaction-values) table above for possible values of `deployment_action` field.
  - It is set to `true` when `deployment_action` equals `4`, and `false` otherwise.

#### [preview_patch](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua#preview_patch)

- **Type:** boolean
- **Description:** __Indicates if this is an preview update.
- **Logic:** Set by SDK to indicate if update is a **preview update**.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
