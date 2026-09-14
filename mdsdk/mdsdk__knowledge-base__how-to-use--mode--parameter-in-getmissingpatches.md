<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-use--mode--parameter-in-getmissingpatches -->

# How to use the "mode" parameter in GetMissingPatches for different update agents?

This article is applied to MetaDefender Endpoint Security SDK releases deployed on Windows, Linux and MacOS.

## [**Overview**](/docs/mdsdk/knowledge-base/how-to-use--mode--parameter-in-getmissingpatches#overview)

The `GetMissingPatches` method in the MetaDefender Endpoint Security SDK supports a `mode` parameter that modifies how patches are detected based on the underlying platform. This KB article explains the available options for the `mode` parameter across different supported update mechanisms.

When calling the `GetMissingPatches` method, the request structure includes the `mode` parameter as part of the input:

json_inCopy{
"input" : {
"method" : 1013,
"signature" : number,
....
"mode": number,
}
}
## [Platform-Specific "mode" Behaviors](/docs/mdsdk/knowledge-base/how-to-use--mode--parameter-in-getmissingpatches#platform-specific-mode-behaviors)

### [Windows Update Agent (WUA)](/docs/mdsdk/knowledge-base/how-to-use--mode--parameter-in-getmissingpatches#windows-update-agent-wua)

| Mode | Description |
| --- | --- |
| **0** (default) | **GREEDY SCAN**: Retrieves as many available patches as possible on the system — including security, non-security, drivers, and Microsoft product updates. It does **not** follow the Windows Update UI settings. |
| **1** | **WUA UI MIMIC SCAN**: Returns patches shown in the Windows Update UI (via *Settings → Windows Update*), respecting user-configured update policies. |

Info

Even if you disable third-party Microsoft product updates in the UI, mode `0` will still detect those updates, while mode `1` will not.

### [Dandified YUM (dnf)](/docs/mdsdk/knowledge-base/how-to-use--mode--parameter-in-getmissingpatches#dandified-yum-dnf)

| Mode | Description |
| --- | --- |
| **0** (default) | Standard detection using base settings for all supported Linux distros. Retrieves patches from the current configured repo for the system’s build version. |
| **1** (Amazon Linux 2023 only) | Forces patch source to the **latest build** using `--releasever=latest`. Ensures patch detection from the most current release even if the local system is on an older build. |

Info

On Amazon Linux 2023, using mode `0` may return no results if the system is already up to date with its current build, even though newer packages exist.

### [Advanced Packaging Tool (apt)](/docs/mdsdk/knowledge-base/how-to-use--mode--parameter-in-getmissingpatches#advanced-packaging-tool-apt)

| Mode | Description |
| --- | --- |
| **0** (default) | Retrieves missing patch info from both local and **online sources**. Includes detailed metadata such as `patches[].date`. **Requires internet access.** |
| **1** | Offline-only detection. Faster but omits external metadata like `patches[].date`, which will default to `0`. |

### [Apple Software Update](/docs/mdsdk/knowledge-base/how-to-use--mode--parameter-in-getmissingpatches#apple-software-update)

Warning

This feature is currently in **beta**.

| Mode | Description |
| --- | --- |
| **0** (default) | Retrieves patches with full metadata, including `patches[].date` and `patches[].kb_id`, from official Apple sources. **Requires internet connection.** |
| **1** | Offline-only mode. Retrieves patch data from the Apple CLI, skipping external metadata. Useful for faster responses when online resources are unavailable. |

Info

If Apple doesn't publish OS-specific metadata, fields such as `kb_id` and others may be missing even in mode `0`.

Support

If **further assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
