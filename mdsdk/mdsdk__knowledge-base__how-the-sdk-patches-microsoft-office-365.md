<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365 -->

# How the SDK patches Microsoft Office 365: native update vs. full package

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Overview](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#overview)

The SDK patches Microsoft Office 365 (Click-to-Run, signature `3029`) differently from most products. There is no static installer URL: the list of files to download is built on the device by a script that reads the device's Click-to-Run (C2R) configuration.

You choose between two update methods with the `background_patching` input of `GetLatestInstaller` (method `50300`) and `InstallFromFiles` (method `50301`):

- **Native update** (`background_patching: 1`). The endpoint runs Microsoft's own updater and downloads only the changes from Microsoft's CDN. The endpoint needs internet access. `GetLatestInstaller` still downloads a small package (`setup.exe` plus `config.xml`), and `InstallFromFiles` needs it.
- **Full package** (`background_patching: 0`, the default). The SDK downloads a complete Office build into a zip file. The endpoint installs from that zip and does not need internet access if the package is complete. This is the only method that works for central distribution or air-gapped devices.

Use the same value on both calls

Pass the same `background_patching` value to `GetLatestInstaller` and `InstallFromFiles`. A native-update package installed without `background_patching: 1` fails with `-28`, because it does not contain the Office files.

The SDK updates an existing Office Click-to-Run installation. It does not perform a fresh install.

| Item | Detail |
| --- | --- |
| Product | Microsoft Office 365 (Click-to-Run), signature `3029` |
| Methods | `GetLatestInstaller` (`50300`) and `InstallFromFiles` (`50301`) |
| Supported update channels | Current, Monthly Enterprise, Semi-Annual |
| Not supported | Current Channel (Preview), Beta, Semi-Annual (Preview) |

## [background_patching and online are different settings](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#background_patching-and-online-are-different-settings)

Two unrelated settings both sound like "online". Keep them apart:

| Setting | What it controls |
| --- | --- |
| `online: 1` | Where the SDK gets its patch metadata: OPSWAT's cloud patch data instead of local files. It does not affect how Office is updated. |
| `background_patching` | The Office update method: `1` runs Microsoft's native updater on the endpoint, `0` builds and installs a full package. |

This article calls the two Office methods **native update** and **full package**, not "online" and "offline", to avoid confusion with the `online` setting.

## [Why there is no static download URL](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#why-there-is-no-static-download-url)

`GetLatestInstaller` does not return a download link for Office:

- **The file list is built on the device.** The download script builds the URL list at run time: `setup.exe` from `officecdn.microsoft.com` every time, plus one URL per Office file in full package mode.
- **An Office update is not one file.** It is `setup.exe` plus a `config.xml` built for that device and, in full package mode, the whole `Office\Data\<version>\` folder. The file list depends on the device's channel, architecture and languages, so no single URL can describe it.
- **URL-only requests are rejected.** `download: 0` (URL only) returns `WA_VMOD_ERROR_PRODUCT_NOT_SUPPORTED` (`-1026`). Use `download: 1`. `download: 2` (patch ID only) works when Office is installed, but returns an empty link.

If Office Click-to-Run is not installed, `GetLatestInstaller` returns `-1026` and `InstallFromFiles` returns `WAAPI_ERROR_NOT_FOUND` (`-28`).

## [Native update (background_patching: 1)](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#native-update-background_patching-1)

### [How it works](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#how-it-works)

- `GetLatestInstaller` with `download: 1` and `background_patching: 1` downloads a small package: `setup.exe` and a `config.xml` that records the OPSWAT target version. It does not download the Office files.
- `InstallFromFiles`, called on that package with `background_patching: 1`, runs Office's own updater (`OfficeC2RClient.exe /update`). Microsoft's Click-to-Run service downloads the update from Microsoft's CDN.

### [What to expect](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#what-to-expect)

- **Internet:** required. Before starting, the SDK pings `microsoft.com`, `8.8.8.8` and `1.1.1.1`. With no connection, the install fails with `WAAPI_ERROR_NO_CONNECTION` (`-17`). The check uses ICMP ping, so a device that reaches the internet only through an HTTPS proxy fails with `-17` even if it can reach the CDN. Allow outbound ICMP to at least one of these hosts.
- **Open apps:** with `force_close: 0`, Office apps stay open and the updater runs without forcing them closed. With `force_close: 1`, the SDK closes Office apps before the update.
- **Restart:** expect `1003` (restart needed) often. It is returned when an Office update was already pending before the run (nothing is attempted, and every retry returns `1003` until the device restarts), or when the update is staged but not yet applied when the run ends.
- **Version:** not pinned. The device moves to the latest build in its channel. The OPSWAT target version is used to skip the update when the device is already current, and to check the result afterwards: if the version has not changed and is still below the target, the result is `-28`. Click-to-Run policy on the device, such as an update path or target version set by Group Policy, can still limit where the updater goes.

## [Full package (background_patching: 0)](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#full-package-background_patching-0)

### [How it works](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#how-it-works)

- `GetLatestInstaller` builds a `config.xml` from the device's registry, pinned to the OPSWAT target version with updates disabled. It then downloads every Office file from Microsoft's CDN into `Office\Data\<version>\` and zips the folder. This is a full Office build, so expect several GB.
- `InstallFromFiles` runs `setup.exe /configure config.xml` against the local files.

### [What to expect](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#what-to-expect)

- **The package must match the device.** `config.xml` has to match the target device on channel, architecture, product ID, languages and excluded apps. Any mismatch fails with `WA_VMOD_ERROR_INSTALLATION_FAILED` (`-1034`). The script log then shows the expected and detected configuration.
- **Open apps:** Office apps block the install. If any are open and `force_close` is `0`, the install does not start and returns `-1030` (cannot close blocking processes). With `force_close: 1`, the SDK closes them, and stops and restarts the Click-to-Run service around the install.
- **Update setting:** the package installs with Office updates disabled. Afterwards the SDK restores the device's previous `UpdatesEnabled` registry value, if that value existed before the install.
- **Internet at install time:** not needed, as long as the package is complete. The package's `config.xml` sets no source path, so the Office Deployment Tool (`setup.exe`) reads the Office files from the folder next to it and contacts Microsoft's CDN only for files it cannot find. If a file is missing on a device without internet, the install fails with `setup.exe`'s own error. `GetLatestInstaller` creates the zip only after every file has downloaded, so ship the zip exactly as produced and do not rebuild or trim it.
- **Disk space:** the zip is extracted before install, so the endpoint needs room for both the zip and the extracted Office build, each several GB.

## [Comparison](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#comparison)

|  | Native update (`background_patching: 1`) | Full package (`background_patching: 0`) |
| --- | --- | --- |
| Value on both calls | `1` on `GetLatestInstaller` and `InstallFromFiles` | `0` (or omitted) on both |
| Internet on the endpoint | Required, to Microsoft's CDN (and ICMP for the pre-check) | Not needed at install time, if the package is complete |
| Download size | Changes only, through Microsoft's updater | Full Office build, several GB |
| Office open during update | Allowed; may return `1003` (restart needed). Closed only with `force_close: 1`. | Fails with `-1030` unless `force_close: 1` |
| Version | Latest in the device's channel, not pinned | Pinned to the OPSWAT target version at download time |
| Air-gapped devices or central distribution | No | Yes, one package per Office setup |
| Typical failures | No connection (`-17`), Click-to-Run service not running (`-1`), restart needed (`1003`), update did not start (`-1034`) | Office open (`-1030`), configuration mismatch (`-1034`), disk space |

## [Patching from a central distribution server](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#patching-from-a-central-distribution-server)

This works only with the full package.

1. On a reference machine with internet access and Office Click-to-Run installed, call `GetLatestInstaller` with `download: 1` and `background_patching: 0`. The reference machine must have the same Office setup as the targets.
2. The zip fits only devices whose Office setup matches the reference machine: same channel, architecture, languages and excluded apps. Build one package per distinct setup, or the targets fail with `-1034`.
3. Copy the zip to the targets and call `InstallFromFiles` with `background_patching: 0`. The zip is extracted before install.

Do not distribute a native-update package this way. It contains only `setup.exe` and `config.xml`, so the endpoint still downloads the update from Microsoft.

## [Result codes](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#result-codes)

| Code | Meaning | Likely cause and action |
| --- | --- | --- |
| `-1026` | Product not supported for this request | `GetLatestInstaller` was called with `download: 0`, or Office Click-to-Run was not detected. Use `download: 1` on a device with Office Click-to-Run installed. |
| `-28` | Not found | `InstallFromFiles`: (a) the package was downloaded with `background_patching: 1` but installed without it, (b) Office Click-to-Run is not installed, or (c) a native update finished but the version did not change and is still below the target version. |
| `-17` | No connection | Native update only. The endpoint cannot reach `microsoft.com`, `8.8.8.8` or `1.1.1.1` by ICMP ping. Check connectivity and firewall rules. A proxy alone does not satisfy this check. |
| `-1` | Click-to-Run service not running | Native update. Start the Click-to-Run service and retry. |
| `-1030` | Cannot close blocking processes | Full package with Office apps open and `force_close: 0`. Close Office, or set `force_close: 1` (unsaved work in Office apps is lost). |
| `-1034` | Installation failed | Full package: the package's `config.xml` does not match the device's channel, architecture, product ID, languages or excluded apps. Either method: `config.xml` is missing from the package, or Office reported a failure code not listed here (kept in the log as the native error). Native update: the Office update process did not start within 3 minutes. Check the script log. |
| `1003` | Restart needed | An Office update was already pending before the run, or the update is staged but not yet applied. Restart the device; retries return `1003` until then. |
| `-1064` | Installation could not complete | Office returned 17002. Possible causes: the installation was canceled, another installation is in progress, the disk is full, or a language ID is unknown. Fix the cause and retry. |
| `-1065` | Installation canceled by blocking apps | Office returned 17006: running applications blocked the update. Close them, wait a few seconds for background processes to exit, and retry. |

Other codes you may see: `-29` (a registry key or value is missing), `-32` (`CDNBaseUrl` is empty), `-47` (`setup.exe` signature not valid), `-42` (download script failed) and `-22` (access denied). Check `error_message` for details. Office's own failure codes are not returned as they are: 17002 becomes `-1064`, 17006 becomes `-1065`, and any other Office failure code becomes `-1034`, with the Office code kept in the log as the native error.

## [Recommendation](/docs/mdsdk/knowledge-base/how-the-sdk-patches-microsoft-office-365#recommendation)

**Use native update (background_patching: 1) wherever the endpoint can reach Microsoft's CDN.** Use the full package only when it cannot, such as air-gapped devices or a requirement to distribute from a central server.

- **Fewer ways to fail.** Microsoft's own updater does the work, so there is no device-specific `config.xml` that must match the target, and the `-1034` configuration-mismatch failures do not occur.
- **Less to manage.** There is no multi-GB package to build, copy and keep one per Office setup.
- **Simpler troubleshooting.** Common failures are limited to connectivity (`-17`), the Click-to-Run service (`-1`) and a pending restart (`1003`).
- **Does not block on open apps.** Native update proceeds while Office is open and returns `1003` if a restart is needed.
- **Smaller downloads.** Only the changes are downloaded.

**Trade-off:** native update moves the device to the latest build in its channel, not a pinned version. Use the full package when you need a specific version.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
