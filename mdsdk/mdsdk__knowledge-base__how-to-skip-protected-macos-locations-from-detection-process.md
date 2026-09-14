<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process -->

# How to skip protected macOS locations from detection process?

This article is applied to MetaDefender Endpoint Security SDK (OESIS) releases deployed on MacOS systems.

## [Overview](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#overview)

The **Restrict Bundle Search** feature allows you to **specify which protected macOS locations the WAAPI detection engine should skip** when scanning for installed application bundles.

This prevents macOS from displaying permission dialogs that require explicit user consent for accessing certain folders (e.g., Photos, Contacts, Reminders, Calendars). Using Restrict Bundle Search streamlines the end-user experience, especially in headless or automated deployments.

## [When to Use](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#when-to-use)

- You have a headless or automated deployment that needs to enumerate installed applications without triggering macOS permission dialogs.
- Your product only needs to detect bundles in "standard" locations (e.g., /Applications) and should skip user-protected data.

## [Configuration Steps](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#configuration-steps)

To enable Restrict Bundle Search, pass the `restrict_bundle_search` configuration key when invoking the `wa_api_setup` API.

### [1.1 Configuration Key](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#11-configuration-key)

CppCopy#define WAAPI_CONFIG_RESTRICT_BUNDLE_SEARCH L"restrict_bundle_search"

- **Type:** string
- **Default:** (empty / no restrictions)

### [1.2 Value Format](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#12-value-format)

The value for the `restrict_bundle_search` is a vertical-bar (|)-delimited list of folder tokens or absolute paths:

JsonCopy"restrict_bundle_search": "<entry1>|<entry2>|…|<entryN>"

- Entries can be:

  - **Tokens** (see 1.3)
  - **Absolute POSIX paths** (e.g., /Volumes/MyData).
- Order does not matter; duplicates are ignored.
- Invalid formats or tokens will return WAAPI_ERROR_INVALID_INPUT_ARGS.

### [1.3 Supported Tokens](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#13-supported-tokens)

| Token | Description |
| --- | --- |
| `all_predefined_values` | Expands to all built-in tokens in one go. |
| `all_predefined_values:except:<t1>,<t2>…` | Same as above, but excludes the comma-separated built-in tokens listed after `:except:` (e.g. `…:except:photos,user_home`). |
| `user_home` | The current user’s home directory (e.g. `/Users/<your_user>`). |
| `shared_folder` | The shared folder from the network. |
| `removable_media` | Any mounted removable volume (USB drives, SD cards, etc.). |
| `reminders` | `~/Library/Reminders` |
| `photos` | `~/Pictures` |
| `calendars` | `~/Library/Calendars` |
| `contacts` | `~/Library/Application Support/AddressBook`and`Library/PersonalizationPortrait/Contacts/` |
| `music` | `~/Music` |
| `desktop` | `~/Desktop` |
| `documents` | `~/Documents` |
| `downloads` | `~/Downloads` |
| `<absolute POSIX path>` | Any custom folder path to skip (e.g. `/Volumes/SecureData` or `/opt/custom/apps`). |

**Note:**

- When using all_predefined_values, **no other built-in tokens** may appear alongside it—only custom absolute paths may be appended.
- Malformed :except: clauses or mixing all_predefined_values with other tokens will result in WAAPI_ERROR_INVALID_INPUT_ARGS.

### [1.4 Examples](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#14-examples)

JsonCopy// 1) Basic: all built-in tokens
{ "restrict_bundle_search": "all_predefined_values" }
// 2) With custom path
{ "restrict_bundle_search": "all_predefined_values|/custom/path" }
// 3) Exclude a few built-ins
{ "restrict_bundle_search": "all_predefined_values:except:photos,user_home" }
// 4) Exclude + custom path
{ "restrict_bundle_search": "all_predefined_values:except:reminders|/temp/path" }
// 5) Invalid: unknown except token → WAAPI_ERROR_INVALID_INPUT_ARGS
{ "restrict_bundle_search": "all_predefined_values:except:invalid_token" }
// 6) Invalid: empty except list → WAAPI_ERROR_INVALID_INPUT_ARGS
{ "restrict_bundle_search": "all_predefined_values:except:" }
// 7) Individual tokens + custom path
{ "restrict_bundle_search": "desktop|downloads|user_home|/Volumes/MyData" }
### [1.5 Return Codes](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#15-return-codes)

- `WAAPI_OK`**:** All specified tokens and paths were recognized and applied.
- `WAAPI_OK_OUTDATED_ENGINE`**:** One or more **unknown** tokens were skipped; the rest were applied.
- `WAAPI_ERROR_INVALID_INPUT_ARGS`**:** The format or tokens are invalid (e.g., malformed `:except:`, unknown token, or mixing tokens improperly).
- `WAAPI_ERROR_FAILED_TO_INIT_BUNDLE_RESTRICTION_SEARCH`**:** The SDK was unable to initialize the bundle restriction search.

## [Future Scenarios & Update Guidance](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#future-scenarios--update-guidance)

As macOS evolves, you may see two kinds of changes in the set of protected folders. We split tokens into:

| Token Type | Description | Tokens | To Add Support |
| --- | --- | --- | --- |
| **Static** | Folders that macOS designates as “protected” but whose paths never move. New static folders simply appear alongside existing ones. | `photos`, `reminders`, `calendars`, `contacts`, `music`, `desktop`, `documents`, `downloads` | **Data-only update**  `libwaresource.dylib` update required (e.g. on newer macOS version 1xxx protected against `movies` folder) |
| **Dynamic** | Locations that must be discovered at runtime (home directory, shared volumes, removable media). Their detection logic may change across macOS releases. | `user_home`, `shared_folder`, `removable_media` | **Engine update**  `libwaapi.dylib`, `libwautils.dylib` and another relevant `dylib` update required to include updated detection logic for the new OS. |

### [2.1 Static Token Example](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#21-static-token-example)

> **Scenario:** Apple introduces a new protected folder called “Movies”. **Action:**
>
> 1. Update **Data Only:** `libwaresource.dylib` to include the `movies` token.
> 2. No engine update is needed.

### [2.2 Dynamic Token Example](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#22-dynamic-token-example)

> **Scenario:** In macOS 16.x, Apple changes the location or mounting behavior for removable media. **Action:**
>
> 1. Update a new **Engine**: `libwaapi.dylib`, `libwautils.dylib` that contains updated logic to discover removable media under the new mount points.
> 2. Data JSON remains unchanged; the engine’s detection logic is enhanced.

### [2.3 Update Guidance](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#23-update-guidance)

Depending on how you’ve configured `restrict_bundle_search`, the update path differs slightly:

#### [2.3.1 Customers Using all_predefined_values](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#231-customers-using-all_predefined_values)

When you use `all_predefined_values`, this expands to all built-in tokens—both **static** (e.g. `photos`, `downloads`, `music`) and **dynamic** (e.g. `user_home`, `shared_folder`, `removeable_media`) values.

| Scenario | Action |
| --- | --- |
| **New static protected folder** e.g. Apple adds “Movies” | ✅ **Data-Only Update:** Update new `libwaresource.dylib` — `all_predefined_values` will then cover it automatically. |
| **macOS changes dynamic locations** e.g. removable media mounts differently | ✅ **Engine Update:** Update new `libwaapi.dylib`, `libwautils.dylib` (and all relevant engine libraries) to updated detection logic for the affected dynamic token. |

#### [2.3.2 Customers Using Individual Tokens](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#232-customers-using-individual-tokens)

When you list tokens one-by-one:

JsonCopy"restrict_bundle_search": "desktop|downloads|photos|user_home"

| Scenario | Action |
| --- | --- |
| **New static protected folder** e.g. Apple adds “Movies” | ✅ **Data-Only Update:** Add movies to your `restrict_bundle_search` and update `libwaresource.dylib`. |
| **macOS changes dynamic locations** e.g. shared volumes re-mount | ✅ **Engine Update:** Update new `libwaapi.dylib`, `libwautils.dylib` (and all relevant engine libraries) with updated discovery code. |

#### [2.3.3 Engine-Update Signal](/docs/mdsdk/knowledge-base/how-to-skip-protected-macos-locations-from-detection-process#233-engine-update-signal)

After calling `wa_api_setup`:

- `WAAPI_OK`: All listed tokens applied; **no** engine update needed.
- `WAAPI_OK_OUTDATED_ENGINE`: One or more **dynamic** tokens couldn’t be resolved by the current engine; plan a `libwaapi.dylib`, `libwautils.dylib` (and all relevant engine libraries) update.

This ensures you only update **data** for static-folder changes, and update the **engine** when runtime discovery logic must evolve.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
