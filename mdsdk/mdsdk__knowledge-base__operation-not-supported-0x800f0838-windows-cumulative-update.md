<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update -->

# “Operation is not supported” error (0x800f0838) when installing a Windows cumulative update on Windows 11 24H2/25H2 and Windows Server 2025

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Summary](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#summary)

If your integration patches Windows by downloading the cumulative update's `.msu` file and installing it directly, using `GetLatestInstaller` (method `50300`) followed by `InstallFromFiles` (method `50301`) on the Windows Update Agent signature `1103`, the install can fail on Windows 11 version 24H2 and later and on Windows Server 2025 with the native error "Operation is not supported" (`0x800f0838`).

This is caused by a change in how Microsoft services Windows, not by an SDK defect. This article explains why it happens and gives two SDK-based ways to fix it:

- **Option 1 (recommended):** install online through the Windows Update Agent with `GetMissingPatches` and `InstallMissingPatches`. Windows fetches the missing piece automatically.
- **Option 2:** for devices that cannot reach Windows Update, install the checkpoint update first by its `patch_id`, then install the latest cumulative update.

## [Error details](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#error-details)

| Item | Detail |
| --- | --- |
| Message | Operation is not supported |
| Native return code (hex) | `0x800f0838` |
| Native return code (decimal) | `-2146498504` |
| SDK call that reports it | `InstallFromFiles` (method `50301`) when installing a Windows `.msu` (see `install_return_code` in the result) |
| SDK product signature | `1103` (Windows Update Agent) |
| Affected systems | Windows 11 version 24H2 and later (including 25H2), Windows Server 2025 |
| Related Microsoft articles | KB5044786; September 2024 checkpoint cumulative update KB5043080 |

## [Why this happens](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#why-this-happens)

Starting with Windows 11 version 24H2 and Windows Server 2025, Microsoft uses **checkpoint cumulative updates**. A checkpoint (for example, the September 2024 update, KB5043080) sets a new baseline, and every cumulative update released after it contains only the changes since that checkpoint. A newer cumulative update therefore cannot be installed unless its checkpoint is already on the device.

When the checkpoint is missing, or Windows cannot bring every installed component up to the new baseline, the Windows servicing engine (CBS) rejects the newer package with `0x800f0838`. A common trigger that Microsoft describes: a Feature on Demand (FoD) or Language Pack (LP) was added from a local source while the device had no connection to Windows Update or WSUS. That component cannot be updated to the latest cumulative update without a connection to Windows Update or WSUS.

### [What this means for SDK integrations](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#what-this-means-for-sdk-integrations)

By default, `GetLatestInstaller` returns only the **latest** cumulative update for the device. Installing that single `.msu` with `InstallFromFiles` is the same as double-clicking it: Windows receives one file and has no way to fetch the checkpoint it depends on, so the install fails. The two options below either let Windows fetch what it needs (Option 1) or give it the checkpoint yourself, in the right order (Option 2).

## [Resolution](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#resolution)

**Which option should I use?** If the endpoint can reach Windows Update or your WSUS or Configuration Manager server, use Option 1. Use Option 2 only for isolated or air-gapped endpoints, or when your product must deliver the `.msu` files itself.

### [Option 1 (recommended): install online through the Windows Update Agent](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#option-1-recommended-install-online-through-the-windows-update-agent)

Instead of downloading and running the `.msu` yourself, ask the SDK to install the update through the Windows Update Agent (WUA) on the device. WUA works out which checkpoint is missing, downloads it, and installs everything in the correct order, so no KB lookup or manual ordering is needed.

**Before you start:** the endpoint must be able to reach Windows Update (or your WSUS or Configuration Manager server), and the SDK must run with administrator rights.

1. **Get the list of missing updates.** Call `GetMissingPatches` (method `1013`) with signature `1103`. Leave `retry_internet_services` at its default of `true` so that, if a WSUS server cannot supply the update, WUA falls back to Microsoft's online service.

{ "input": { "method": 1013, "signature": 1103, "retry_internet_services": true } }

2. **Pick the cumulative update** from the returned `patches` array (match on `kb_id` or `title`).
3. **Install it.** Call `InstallMissingPatches` (method `1014`) with signature `1103`, passing the `title` and `product` values exactly as they were returned in step 1.

{ "input": { "method": 1014, "signature": 1103,
"patches": [ { "title": "<title from GetMissingPatches>",
"product": "<product from GetMissingPatches>" } ] } }

4. **Check the result.** Each entry in the returned `patches` array should have `state` = `installed`. Restart the endpoint if the update's `reboot_required` value is `true`.
5. **Verify.** After the restart, call `GetInstalledPatches` (method `1023`) and confirm the KB is listed, or call `GetMissingPatches` again and confirm it is no longer listed.

### [Option 2: install the checkpoint first, then the latest update](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#option-2-install-the-checkpoint-first-then-the-latest-update)

Use this option when the endpoint cannot use Windows Update or WSUS (for example, an air-gapped system). Use the `patch_id` input of `GetLatestInstaller` and `InstallFromFiles` to install the September 2024 checkpoint (KB5043080) **first**, and only then install the latest cumulative update.

**Before you start:** load the patch database with `LoadPatchDatabase` (method `50302`) as your integration normally does, and run the SDK with administrator rights.

#### [Step 1: Find the checkpoint's patch_id](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#step-1-find-the-checkpoints-patch_id)

Use the `patch_id` that matches the endpoint's operating system and architecture:

| Operating system | Architecture | `patch_id` for KB5043080 |
| --- | --- | --- |
| Windows 11, version 24H2 | x64 | `1aeb2be2-332e-4950-834f-256e9c75dee9` |
| Windows 11, version 24H2 | arm64 | `74f72ad5-bb0a-474e-9dda-1c87e92ef891` |
| Windows Server 2025 | x64 | `27466e51-07f6-4026-812f-9fbb1f0e91f2` |

These IDs come from the OPSWAT patch catalog (`patch_system_aggregation.json`, matched on `kb_id` 5043080). If you ship a different catalog version, confirm the ID there or contact OPSWAT Support.

#### [Step 2: Download the checkpoint](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#step-2-download-the-checkpoint)

Call `GetLatestInstaller` (method `50300`) with signature `1103`, the checkpoint `patch_id`, and `download` = `1` to save the `.msu` to a local folder:

{ "input": { "method": 50300, "signature": 1103,
"patch_id": "1aeb2be2-332e-4950-834f-256e9c75dee9",
"download": 1, "path": "C:\\Packages" } }

Confirm that the result's `security_update_id` is `5043080`, and note the downloaded file's path.

#### [Step 3: Install the checkpoint](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#step-3-install-the-checkpoint)

Call `InstallFromFiles` (method `50301`) with signature `1103`, the path from Step 2, and the same `patch_id`:

{ "input": { "method": 50301, "signature": 1103,
"path": "<path returned in Step 2>",
"patch_id": "1aeb2be2-332e-4950-834f-256e9c75dee9" } }

If the result has `require_restart` = `1`, restart the endpoint before continuing.

#### [Step 4: Download and install the latest cumulative update](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#step-4-download-and-install-the-latest-cumulative-update)

Call `GetLatestInstaller` again with signature `1103` and `download` = `1`, but **without** `patch_id`, so the SDK selects the latest cumulative update for the device. Then install the downloaded file with `InstallFromFiles` as in Step 3 (you can pass the `patch_id` returned by `GetLatestInstaller`). Restart if `require_restart` = `1`.

If `GetLatestInstaller` returns `type_id` = `2` (more than one file), call it again with `index` = `1`, `2`, … until it returns `WA_VMOD_ERROR_OUT_OF_RANGE` (`-1039`), and install the files in the order returned.

#### [Step 5: Verify](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#step-5-verify)

Call `GetInstalledPatches` (method `1023`) and confirm that both KB5043080 and the latest cumulative update are listed.

Order matters

Installing the latest cumulative update before the checkpoint fails again with `0x800f0838`. If KB5043080 is already installed and the error still occurs (the Feature on Demand or Language Pack case above), use Option 1, because that case can only be repaired with a connection to Windows Update or WSUS.

## [Related articles](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#related-articles)

- [How do GetProductVulnerability and GetLatestInstaller work together to remediate Windows OS vulnerabilities?](/docs/mdsdk/knowledge-base/how-getproductvulnerability-and-getlatestinstaller-work-together)
- [How can I interpret SDK error codes related to Windows Update Agent?](/docs/mdsdk/knowledge-base/how-can-i-interpret-sdk-error-codes-related-to-wua)
- [Understanding GetMissingPatches output when invoking with Windows Update Agent (WUA)](/docs/mdsdk/knowledge-base/understanding-getmissingpatches-output-when-invoking-with-wua)

## [References](/docs/mdsdk/knowledge-base/operation-not-supported-0x800f0838-windows-cumulative-update#references)

- [OESIS method reference](https://software.opswat.com/OESIS_V4/html/c_method.html) (GetMissingPatches, InstallMissingPatches, GetInstalledPatches, GetLatestInstaller, InstallFromFiles)
- [Microsoft Support: "Operation is not supported" error installing a post-checkpoint update by double-clicking the .msu package (KB5044786)](https://support.microsoft.com/help/5044786)
- [Microsoft Learn: Checkpoint cumulative updates and Microsoft Update Catalog usage](https://learn.microsoft.com/windows/deployment/update/catalog-checkpoint-cumulative-updates)
- [Microsoft Update Catalog](https://catalog.update.microsoft.com)

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
