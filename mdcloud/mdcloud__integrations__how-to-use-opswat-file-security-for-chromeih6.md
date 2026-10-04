<!-- source: https://www.opswat.com/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6 -->

# Deploy and Configure with Group Policy

OPSWAT File Security for Browser can be force-installed and centrally configured on managed devices using browser enterprise policies. This page covers Microsoft Edge, Google Chrome, and Chromium on Windows and Linux. Examples use Microsoft Edge; substitute the path for your browser where indicated.

### [Prerequisites](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#prerequisites)

- The device must be centrally managed: domain-joined, Microsoft Entra ID-joined, or enrolled in an MDM such as Intune. Browsers ignore force-install policies on unmanaged devices.
- The extension is distributed through the Chrome Web Store. Microsoft Edge installs Chrome Web Store extensions through the policies below; no Edge Add-ons listing is required.
- Extension ID: `fjampemfhdfmangifafmianhokmpjbcj`
- Update URL: `https://clients2.google.com/service/update2/crx`

### [Force-install the extension](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#force-install-the-extension)

Use either policy. `ExtensionSettings` is recommended, as it also lets you block user removal and manage other extensions from one policy.

#### [Option A — ExtensionInstallForcelist](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#option-a--extensioninstallforcelist)

| Browser | GPO path |
| --- | --- |
| Microsoft Edge | Computer Configuration › Administrative Templates › Microsoft Edge › Extensions › Control which extensions are installed silently |
| Google Chrome | Computer Configuration › Administrative Templates › Google › Google Chrome › Extensions › Configure the list of force-installed apps and extensions |

Value:

fjampemfhdfmangifafmianhokmpjbcj;https://clients2.google.com/service/update2/crx
#### [Option B — ExtensionSettings](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#option-b--extensionsettings)

| Browser | GPO path |
| --- | --- |
| Microsoft Edge | Computer Configuration › Administrative Templates › Microsoft Edge › Extensions › Configure extension management settings |
| Google Chrome | Computer Configuration › Administrative Templates › Google › Google Chrome › Extensions › Extension management settings |

Value:

json

{"fjampemfhdfmangifafmianhokmpjbcj":{"installation_mode":"force_installed","update_url":"https://clients2.google.com/service/update2/crx"}}
#### [Linux](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#linux)

Place a JSON file in the managed policies directory for your browser:

| Browser | Directory |
| --- | --- |
| Microsoft Edge | `/etc/opt/edge/policies/managed/` |
| Google Chrome | `/etc/opt/chrome/policies/managed/` |
| Chromium | `/etc/chromium/policies/managed/` |

json

{
"ExtensionSettings": {
"fjampemfhdfmangifafmianhokmpjbcj": {
"installation_mode": "force_installed",
"update_url": "https://clients2.google.com/service/update2/crx"
}
}
}
### [Configure managed settings](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#configure-managed-settings)

The extension reads its configuration from the browser's managed storage. All settings are supplied as a **single JSON string** under a key named `settings`. Do not supply a nested JSON object.

#### [Settings template](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#settings-template)

json

{
"scan_downloads": true,
"sanitize_downloads": true,
"sandbox_analysis": false,
"selected_workflow": "",
"reputation_lookup": false,
"share_results": false,
"show_notifications": true,
"show_status_page": true,
"save_clean_files": false,
"storage_file_size": "",
"safe_url": true,
"file_size_limit": "",
"file_size_limit_one_time": "",
"custom_apikey": "",
"core_url": "",
"core_apikey": "",
"core_rule": "",
"domain_allowlist": ["opswat.com", "metadefender.com"]
}
#### [Windows](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#windows)

Create a `REG_SZ` value named `settings` under the key for your browser, containing the JSON template above as a single-line string.

| Browser | Registry key |
| --- | --- |
| Microsoft Edge | `HKLM\SOFTWARE\Policies\Microsoft\Edge\3rdparty\extensions\fjampemfhdfmangifafmianhokmpjbcj\policy` |
| Google Chrome | `HKLM\SOFTWARE\Policies\Google\Chrome\3rdparty\extensions\fjampemfhdfmangifafmianhokmpjbcj\policy` |
| Chromium | `HKLM\SOFTWARE\Policies\Chromium\3rdparty\extensions\fjampemfhdfmangifafmianhokmpjbcj\policy` |

Example (Edge):

Key: HKLM\SOFTWARE\Policies\Microsoft\Edge\3rdparty\extensions\fjampemfhdfmangifafmianhokmpjbcj\policy
Name: settings
Type: REG_SZ
Data: {"scan_downloads":true,"sanitize_downloads":true,"sandbox_analysis":false,"selected_workflow":"","reputation_lookup":false,"share_results":false,"show_notifications":true,"show_status_page":true,"save_clean_files":false,"storage_file_size":"","safe_url":true,"file_size_limit":"","file_size_limit_one_time":"","custom_apikey":"","core_url":"","core_apikey":"","core_rule":"","domain_allowlist":["opswat.com","metadefender.com"]}
#### [Linux](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#linux)

Add a file (for example `opswat-file-security.json`) to the managed policies directory listed above. Note the escaped inner quotes: `settings` is a string, not an object.

json

{
"3rdparty": {
"extensions": {
"fjampemfhdfmangifafmianhokmpjbcj": {
"settings": "{\"scan_downloads\":true,\"sanitize_downloads\":true,\"sandbox_analysis\":false,\"selected_workflow\":\"\",\"reputation_lookup\":false,\"share_results\":false,\"show_notifications\":true,\"show_status_page\":true,\"save_clean_files\":false,\"storage_file_size\":\"\",\"safe_url\":true,\"file_size_limit\":\"\",\"file_size_limit_one_time\":\"\",\"custom_apikey\":\"\",\"core_url\":\"\",\"core_apikey\":\"\",\"core_rule\":\"\",\"domain_allowlist\":[\"opswat.com\",\"metadefender.com\"]}"
}
}
}
}
### [Settings reference](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#settings-reference)

| Key | Type | Default `[CONFIRM all]` | Description |
| --- | --- | --- | --- |
| `scan_downloads` | boolean | `true` | Scan every downloaded file. |
| `sanitize_downloads` | boolean | `true` | Produce a Deep CDR-sanitized copy of supported file types. Ignored when `selected_workflow` is set. |
| `sandbox_analysis` | boolean | `false` | Submit suspicious files for dynamic analysis. Ignored when `selected_workflow` is set. |
| `selected_workflow` | string | `""` | MetaDefender Cloud Workflow ID. When set, the workflow's configuration replaces `sanitize_downloads` and `sandbox_analysis`. Empty string disables. |
| `reputation_lookup` | boolean | `false` | Check download URLs, IPs, and domains against MetaDefender Cloud reputation data. |
| `share_results` | boolean | `false` | Share scan results with the MetaDefender Cloud community. |
| `show_notifications` | boolean | `true` | Show browser notifications for scan verdicts. |
| `show_status_page` | boolean | `true` | Open the scan status page during analysis. |
| `save_clean_files` | boolean | `false` | Keep only files with a clean verdict; discard the rest. |
| `storage_file_size` | integer or string | `""` | Maximum size in MB of a download held in browser memory while scanning. Larger files are not held. `0` or `""` disables. |
| `safe_url` | boolean | `true` | Check the download URL before the file is fetched. |
| `file_size_limit` | integer or string | `""` | Skip scanning files from regular links larger than this size in MB. `0` or `""` disables. |
| `file_size_limit_one_time` | integer or string | `""` | Skip scanning files from one-time links larger than this size in MB. `0` or `""` disables. |
| `custom_apikey` | string | `""` | MetaDefender Cloud API key used for all scans. Overrides the user's own key and any Core configuration. Empty string disables. |
| `core_url` | string | `""` | URL of a private MetaDefender Core server. Requires `core_apikey`. Empty string disables Core scanning. |
| `core_apikey` | string | `""` | API key for the MetaDefender Core server. Requires `core_url`. |
| `core_rule` | string | `""` | Name of a workflow rule on the Core server (for example `multiscan`), sent as the `rule` header. Empty or omitted lets Core apply its default rule. If the name is not found, Core applies its default rule. |
| `domain_allowlist` | array of strings | `["opswat.com","metadefender.com"]` | Domains for which downloads are not scanned. Empty array disables. |

### [Precedence and interactions](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#precedence-and-interactions)

| Situation | Behaviour |
| --- | --- |
| `custom_apikey` set | Used for all scans. Core settings and the user's own key are ignored. |
| `core_url` + `core_apikey` set, `custom_apikey` empty | Files are scanned by the Core server. `core_rule` applies if set. |
| Neither set | Files are scanned by MetaDefender Cloud using the signed-in user's key. |
| `selected_workflow` set | Workflow configuration overrides `sanitize_downloads` and `sandbox_analysis`. |
| File exceeds `file_size_limit` but not `file_size_limit_one_time`, from a one-time link | File is still scanned. |
| File exceeds both limits | Scan is skipped. |
| `scan_downloads: true`, `show_notifications: false` | Scanning does not run. |

### [Security considerations](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#security-considerations)

- Managed-storage values, including `custom_apikey` and `core_apikey`, are stored in plaintext in the Windows registry under `HKLM` and in `/etc` on Linux. Both locations are readable by local users.
- Use a dedicated API key for browser deployments. Scope it to the minimum required permissions and rotate it on your normal credential schedule.
- Do not use an administrator or organization-owner API key in a browser policy.

### [Verify the deployment](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#verify-the-deployment)

1. Open `edge://policy` (or `chrome://policy`). Confirm `ExtensionSettings` or `ExtensionInstallForcelist` appears with no errors, and that the `settings` value appears under the extension's ID.
2. Open `edge://extensions` (or `chrome://extensions`). The extension should show as installed by your administrator and cannot be removed by the user.
3. Restart the browser after applying policy if the extension does not appear.

### [Limitations](/docs/mdcloud/integrations/how-to-use-opswat-file-security-for-chromeih6#limitations)

- **Allow access to file URLs** cannot be set by policy on Chrome or Edge. Each user must enable it manually in `edge://extensions` or `chrome://extensions`, per device and per profile, if scanning of local `file://` downloads is required.
