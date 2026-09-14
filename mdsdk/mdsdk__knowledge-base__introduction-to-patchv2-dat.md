<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/introduction-to-patchv2-dat -->

# Introduction to patchv2.dat

## [Background](/docs/mdsdk/knowledge-base/introduction-to-patchv2-dat#background)

The OESIS Framework Patch Management module relies on a patch database to identify, download, and install application patches. The database `patch.dat` is designed to include the **latest version** of each supported application.

## [Problem](/docs/mdsdk/knowledge-base/introduction-to-patchv2-dat#problem)

Many customers need to patch applications to a specific version — for example, a version validated against their organization's internal security policy — rather than the newest release. Supporting this use case requires a patch database that covers more than the latest version of each application.

## [Solution Overview](/docs/mdsdk/knowledge-base/introduction-to-patchv2-dat#solution-overview)

A new database, **patchv2.dat**, is introduced as an improvement over `patch.dat`. It includes **all application versions recognized by the SDK** — not only the latest release of each application.

This enables version-specific patching via the `requested_version` parameter in both `GetLatestInstaller` and `InstallFromFiles`. See [Version-Specific Patching with the requested_version Parameter](https://www.opswat.com/docs/mdsdk/knowledge-base/version-specific-patching-with-the-requested-version-parameter).

### [Differences between patch.dat and patchv2.dat](/docs/mdsdk/knowledge-base/introduction-to-patchv2-dat#differences-between-patchdat-and-patchv2dat)

|  | **patch.dat (legacy)** | **patchv2.dat (new)** |
| --- | --- | --- |
| Version coverage | Latest version of each application only | All application versions recognized by the SDK |
| Version-specific patching (`requested_version`) | Limited to the latest version; `requested_version` is ignored in `GetLatestInstaller` | Supported in both `GetLatestInstaller` and `InstallFromFiles`, including older versions |

### [Usage](/docs/mdsdk/knowledge-base/introduction-to-patchv2-dat#usage)

Load `patchv2.dat` with `LoadPatchDatabase (50302)` by specifying it in the `dat_input_source_file` field instead of the legacy database.

Notes:

- `patchv2.dat` is supported in offline mode only. If online mode is set to a value different from 0, `GetLatestInstaller` and `InstallFromFiles` return `WAAPI_ERROR_INVALID_INPUT_ARGS`.
- If `patchv2.dat` is absent or fails to load, `LoadPatchDatabase` returns the appropriate error. The SDK does not fall back to `patch.dat`.

## [SDK Version](/docs/mdsdk/knowledge-base/introduction-to-patchv2-dat#sdk-version)

- Windows: 4.3.6110.0
- Mac: 4.3.5495.0

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
