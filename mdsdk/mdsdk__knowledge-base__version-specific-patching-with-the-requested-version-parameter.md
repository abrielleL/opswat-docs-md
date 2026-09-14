<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/version-specific-patching-with-the-requested-version-parameter -->

# Version-Specific Patching with the requested_version Parameter

## [Background](/docs/mdsdk/knowledge-base/version-specific-patching-with-the-requested-version-parameter#background)

In many managed environments, organizations standardize on specific application versions that have been validated against their internal security policy. End users' policy configurations define which application version is approved, and the newest release is not always the approved one — it may not yet have passed the organization's change-control process.

## [Problem](/docs/mdsdk/knowledge-base/version-specific-patching-with-the-requested-version-parameter#problem)

Patching always to the latest available version can conflict with these policies: customers need to install or update an application to the exact version defined in the policy configuration from their users, rather than whatever version is newest.

## [Solution Overview](/docs/mdsdk/knowledge-base/version-specific-patching-with-the-requested-version-parameter#solution-overview)

The SDK supports **version-specific patching** through the `requested_version` parameter in both the `GetLatestInstaller (50300)` and `InstallFromFiles (50301)` methods, allowing customers to install or update an application to the exact version that matches the policy configuration from their users:

- In `GetLatestInstaller`, input a version in `requested_version` to download (or retrieve download information for) that specific application version.
- In `InstallFromFiles`, input a version in `requested_version` to install that specific version from local installer files, including older versions.

Version-specific patching with `GetLatestInstaller` requires the new patch database, **patchv2.dat**, which contains all application versions recognized by the SDK. Load it via `LoadPatchDatabase (50302)` by specifying `patchv2.dat` in the `dat_input_source_file` field. If the legacy database (`patch.dat`) is used and `requested_version` is specified, the SDK ignores the parameter. For details, see [Introduction to patchv2.dat](https://www.opswat.com/docs/mdsdk/knowledge-base/introduction-to-patchv2-dat).

When `requested_version` is not provided, both methods behave as before: the SDK targets the latest available version.

### [Behavior](/docs/mdsdk/knowledge-base/version-specific-patching-with-the-requested-version-parameter#behavior)

| **Method** | **Scenario** | **Behavior** |
| --- | --- | --- |
| `LoadPatchDatabase` | Input new database `patchv2.dat` to the `dat_input_source_file` parameter | The `patchv2.dat` is loaded and ready for use by the patching methods. |
| `GetLatestInstaller` | Input a version in `requested_version` | The SDK shows download info or downloads the patch if that version is verified and present in the database. |
| `InstallFromFiles` | Input a version in `requested_version` | The SDK allows installation only if the installer's file hash matches the database hash. |

### [Error Codes](/docs/mdsdk/knowledge-base/version-specific-patching-with-the-requested-version-parameter#error-codes)

| **Method** | **Scenario** | **Error Code** |
| --- | --- | --- |
| `GetLatestInstaller` | User inputs `patchv2.dat` and specifies online mode different from 0 | `WAAPI_ERROR_INVALID_INPUT_ARGS` |
| `GetLatestInstaller` | User requests a version not found in the database | `WA_VMOD_VERSION_LOCK_NOT_SUPPORTED` |
| `GetLatestInstaller` | User requests a version without a versioned URL in the database | `WA_VMOD_VERSION_LOCK_NOT_SUPPORTED` |
| `InstallFromFiles` | User inputs `patchv2.dat` and specifies online mode different from 0 | `WAAPI_ERROR_INVALID_INPUT_ARGS` |
| `InstallFromFiles` | User requests a version not found in the database | `WA_VMOD_VERSION_LOCK_NOT_SUPPORTED` |
| `InstallFromFiles` | User requests a version that does not match the input installer's version | `WAAPI_ERROR_VERSION_MISMATCH` |

## [SDK Version](/docs/mdsdk/knowledge-base/version-specific-patching-with-the-requested-version-parameter#sdk-version)

- Windows: 4.3.6110.0
- macOS: 4.3.5495.0
- Linux: 4.3.5226.0

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
