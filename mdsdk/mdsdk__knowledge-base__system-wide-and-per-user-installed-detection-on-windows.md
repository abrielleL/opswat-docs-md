<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows -->

# System-wide and Per-user Installed Detection on Windows

## [**Overview**](/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows#overview)

OESIS Framework now supports detecting across system-wide and per-user installations on Windows endpoints by introducing a new parameter to the `DetectProducts` method and extending `GetVersion` method.

### [**Key concept**](/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows#key-concept)

To better understand the detection results, OESIS categorizes Windows installations into two types:

- **System-wide Installation**: The product is installed in a common location (e.g., `C:\Program Files`) and ***is available to all users*** on the endpoint. In the `instances` output, these are identified by the value `"System Wide Instance"`.
- **Per-user Installation**: The product is installed specifically for ***a single user profile*** (e.g., `%LocalAppData%`). These instances are only accessible when that specific user is logged in. In the `instances` output, these are identified by the user's account name (e.g., `DOMAIN\username`).

## [**Prerequisites and Scope**](/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows#prerequisites-and-scope)

- **Platform**: Windows only.
- **Methods involved**:

  - `DetectProducts` (Method ID: `0`)
  - `GetVersion` (Method ID: `100`)
- **Permissions**:

  - **Elevated privileges** (e.g., administrator or system service) are required for detecting per-user products of all users, and may be required for GetVersion as well to target a specific per-user `instance_id`.
- **Backward compatibility**: If you do **not** use the new parameter, `DetectProducts` behaves as in previous versions.

## [Enabling Detection for installed products of every user in DetectProducts](/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows#enabling-detection-for-installed-products-of-every-user-in-detectproducts)

### [New Input Parameter: detect_all_users_products](/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows#new-input-parameter-detect_all_users_products)

- **Name**: `detect_all_users_products`
- **Type**: `boolean`
- **Required**: No (Optional)
- **Applies to**: Windows only
- **Default behavior:** If omitted or set to `false`, `DetectProducts` behaves exactly as it did before: checking system-wide install locations plus the hive of the user account making the call. It does not check any **other** user's profile, and the output has no `instances` field.

When `detect_all_users_products` is set to `true`:

- OESIS attempts to detect, for every user profile on the endpoint (not just the caller's), whether that user has the product installed, including:

  - System‑wide installations.
  - Per‑user installations for all user profiles, not just the current user.
- The detection results are **consolidated**:

  - Only **one signature** is returned for each product.
  - A new `instances` object appears in the method output under each detected product to provide a **per‑instance breakdown**.

**Important**

Detecting product for all users typically requires **elevated privileges** (for example, administrator or system service). Without appropriate permissions, OESIS may return `WAAPI_ERROR_ACCESS_DENIED`.

A minimal example request on Windows might look like:

{
"input": {
"method": 0,
"category": 10,
"detect_all_users_products": true
}
}

You can continue to use all other existing `DetectProducts` input fields as before; only the new `detect_all_users_products` flag is added.

### [Output Changes: The instances Field](/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows#output-changes-the-instances-field)

When `detect_all_users_products` is enabled on Windows, each product in returned `detected_products` may include an `instances` field:

- **Field:** `detected_products[].instances`
- **Type:** object (key-value map)
- **Presence:** Only appears when `detect_all_users_products` is specified in the request (Windows).

Each entry inside `instances` has the form:

"instances": {
"<instance_id>": "<owner description>"
}

- The **key** (`<instance_id>`) is an opaque identifier for that installed instance.
- The **value** describes who owns the instance, could be:

  - `"System Wide Instance"`
    → The product is installed **system‑wide** for all users.
  - domain and username in format `DOMAIN\\samAccountName`
    → The product is installed for a specific Windows user account
    (for example, `DESKTOP-M85K9UP\\HM` or `LOCAL\\test`).

Additionally, when `detect_all_users_products` is `true`, because a result is now merged across multiple users, `display_name` returns `"n/a"` and `uninstall_hive` returns `[]` (even if `show_uninstall_hive` is `true`) for every product.

Example Windows output with system‑wide and per‑user instances:

{
"result": {
"method": 0,
"code": 0,
"timing": 5331,
"timestamp": 123456789,
"detected_products": [
{
"categories": [
10
],
"instances": {
"2a334bf63929cf983eece4a9e998361f": "DESKTOP-M85K9UP\\SIUUUUUUUU",
"4865499167ce5f271a7c65d1ba878290": "DESKTOP-M85K9UP\\HM",
"4868d5d5fe61c01751b3d3c4d2da92ef": "DESKTOP-M85K9UP\\test",
"8edd6b29b9c9c01294202c096ddb2b26": "System Wide Instance"
},
"labels": {
"adware": false,
"bloatware": false,
"pua": false,
"toolbar": false
},
"product": {
"id": 701,
"name": "GIMP"
},
"sig_name": "GIMP 3+",
"signature": 4032,
"vendor": {
"id": 469,
"name": "Spencer Kimball, Peter Mattis and the GIMP Development Team"
}
},
...
]
}
}

In this example:

- **One** product entry (GIMP 3+) is returned.
- The `instances` object shows:

  - A **system‑wide** installation.
  - Separate installations for three specific user accounts on the same machine.

**Technical Note**

The `instance_id` is a hash computed from the owning identity. It stays the same for the same owner across separate `DetectProducts` calls, as long as that user's domain/username doesn't change. Treat it as an identifier that:

- Comes from `DetectProducts`, and
- Is later used with `GetVersion` to query the version of that specific instance.
## [Query the Version of a Specific Instance with GetVersion](/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows#query-the-version-of-a-specific-instance-with-getversion)

This section explains how to use `GetVersion` together with the `instance_id` returned by `DetectProducts` to retrieve version information for a **specific installation instance** on Windows (system‑wide or per‑user).

**Cross‑platform note**

`instance_id` field in `GetVersion` is not new globally. It has been introduced for **macOS** and **Linux** to distinguish multiple instances of the same product for one user (different install paths).

With this update, **Windows** now also supports `instance_id`, but for a different context.

An example input structure for `GetVersion` with `instance_id` on Windows might look like:

{
"input": {
"method": 100,
"signature": 4032,
"instance_id": "2a334bf63929cf983eece4a9e998361f"
}
}

Where:

- `method`: `100` (represents `GetVersion`).
- `signature`: The product signature returned by `DetectProducts`.
- `instance_id`: A string obtained directly from `detected_products[].instances` in the `DetectProducts` result.

**Note**

The same `GetVersion` method can evaluate both **system‑wide** and **per‑user** instances because `DetectProducts` normalizes per‑user signatures to the system-preferred signature (if exists).

## [Example Workflow with DetectProducts and GetVersion](/docs/mdsdk/knowledge-base/system-wide-and-per-user-installed-detection-on-windows#example-workflow-with-detectproducts-and-getversion)

Use the following pattern to obtain per‑instance version details:

1. **Run** `DetectProducts` with multi‑user detection (Windows)

   - Set `detect_all_users_products = true` in your `DetectProducts` request.
   - Ensure the process runs with appropriate privileges to see all user installations.
2. **Locate the target product and its instances**
   In `detected_products`, find the desired product and inspect the `instances` map, for example:

   "instances": {
   "2a334bf63929cf983eece4a9e998361f": "DESKTOP-M85K9UP\\UserA",
   "4865499167ce5f271a7c65d1ba878290": "DESKTOP-M85K9UP\\UserB",
   "8edd6b29b9c9c01294202c096ddb2b26": "System Wide Instance"
   }
3. **Select an** `instance_id`
   Choose the key that corresponds to the instance you care about:

   - A specific user (e.g., `"2a334bf63929cf983eece4a9e998361f"` → `DESKTOP-M85K9UP\\UserA`).
   - Or the system‑wide instance (`"8edd6b29b9c9c01294202c096ddb2b26"` → `System Wide Instance`).
4. **Call** `GetVersion` **with** `signature` **and** `instance_id`
   Use the product’s `signature` from `DetectProducts` and the selected `instance_id`:

   {
   "input": {
   "method": 100,
   "signature": 4032,
   "instance_id": "2a334bf63929cf983eece4a9e998361f"
   }
   }
5. **Read the version result for that instance**

   - `GetVersion` returns the same output structure as before.
   - The difference is that the data now **specifically corresponds** to the selected instance (that user or system‑wide installation).

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
