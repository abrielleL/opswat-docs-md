<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-sdk-distinguishes-os-restart-and-application-restart -->

# How the OESIS SDK distinguishes OS restart and application restart when patching products

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Overview](/docs/mdsdk/knowledge-base/how-sdk-distinguishes-os-restart-and-application-restart#overview)

When a product is upgraded to a new version, the upgrade may need an OS restart (reboot), an application restart, or no restart at all to complete.

The SDK tells your agent or server which kind of restart is needed, both before and after installation.

### [Before installation](/docs/mdsdk/knowledge-base/how-sdk-distinguishes-os-restart-and-application-restart#before-installation)

On the endpoint, `GetLatestInstaller (50300)` reports the restart requirement with two fields:

- `reboot_required`: whether a restart is needed.
- `restart_type`: what kind of restart is needed. Values are `os_restart`, `application_restart`, `none` and `unspecified`.

On the server, read `restart_type` together with `requires_reboot` (in `patch_aggregation.json`) or `requires_restart` (in `patch_aggregation_v2.json`):

| `requires_reboot` (v1) / `requires_restart` (v2) | `restart_type` | Meaning |
| --- | --- | --- |
| `no` | `none` | No restart at all. These two values always go together. |
| `yes` | `os_restart` | OS reboot after a successful install. |
| `yes` | `application_restart` | Application restart after a successful install. |
| `maybe` / `runtime determined` | `os_restart` | OS reboot only when the installer reports a pending reboot. |
| `maybe` / `runtime determined` | `application_restart` | Application restart only when the installer reports a pending restart. |
| `yes` / `maybe` / `runtime determined` | `unspecified` | The kind of restart depends on endpoint conditions at install time. |

### [After installation](/docs/mdsdk/knowledge-base/how-sdk-distinguishes-os-restart-and-application-restart#after-installation)

On the endpoint, `InstallFromFiles (50301)` reports the restart requirement by:

- returning a success code: `WA_VMOD_INSTALLATION_NEED_RESTART (1003)` for an OS restart, `WA_VMOD_INSTALLATION_NEED_APPLICATION_RESTART (1005)` for an application restart, or `WAAPI_OK (0)` when no restart is needed.
- setting the `require_restart` flag to `0` or `1` in its output.

## [Workflow for checking restart requirements](/docs/mdsdk/knowledge-base/how-sdk-distinguishes-os-restart-and-application-restart#workflow-for-checking-restart-requirements)

1. Call `GetLatestInstaller (50300)` and read `restart_type`, or read it from the patch catalog files on your server.
2. Decide whether to deploy the patch:

   - `none` or `application_restart`: no OS reboot is expected.
   - `os_restart`: plan for an OS reboot.
   - `unspecified`: treat it as a possible OS reboot.
3. Close the application first if the patch requires it, then call `InstallFromFiles (50301)`.
4. Act on the return code: restart the OS for `WA_VMOD_INSTALLATION_NEED_RESTART (1003)`, or restart the application for `WA_VMOD_INSTALLATION_NEED_APPLICATION_RESTART (1005)`. The return code reflects what actually happened on the endpoint, so it is the final answer.

## [restart_type and requires_close_first](/docs/mdsdk/knowledge-base/how-sdk-distinguishes-os-restart-and-application-restart#restart_type-and-requires_close_first)

These two fields answer different questions and are read independently:

- `requires_close_first` (in `patch_aggregation_v2.json`) or `require_close_first` (in `InstallFromFiles (50301)`): running instances of the product must be closed **before** installation.
- `restart_type`: what must be restarted **after** installation to complete the upgrade.

## [Coverage and limitations](/docs/mdsdk/knowledge-base/how-sdk-distinguishes-os-restart-and-application-restart#coverage-and-limitations)

- **Operating system updates:** `restart_type` is determined for third-party patches only. For OS updates, the field is present but always returns `unspecified`. Rely on the `InstallFromFiles (50301)` return code for these updates.
- **Patch data changes:** the patch catalog is updated regularly, and a patch's restart requirement can change between updates. Read `restart_type` for each patch rather than keeping a fixed list of products.

## [Compatible SDK version](/docs/mdsdk/knowledge-base/how-sdk-distinguishes-os-restart-and-application-restart#compatible-sdk-version)

`restart_type` in `GetLatestInstaller`, `patch_aggregation.json` and `patch_aggregation_v2.json`:

- Windows: 4.3.6788.0 or later
- macOS: 4.3.6181.0 or later
- Linux: 4.3.5785.0 or later

Return code `WA_VMOD_INSTALLATION_NEED_APPLICATION_RESTART (1005)` in `InstallFromFiles`:

- Windows: 4.3.5434 or later
- Windows V3V4 Adapter: 4.3.3552 or later
- macOS: 4.3.4881 or later
- macOS V3V4 Adapter: 4.3.3473 or later
- Linux: 4.3.4481 or later
- Linux V3V4 Adapter: 4.3.3462 or later

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
