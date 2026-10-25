<!-- source: https://www.opswat.com/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta -->

# How to configure Offline Reputation Service allowlisting in MetaDefender Core Adaptive Sandbox.

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to MetaDefender Core with the embedded Adaptive Sandbox module, Adaptive Sandbox version **3.3.0** or later, deployed on Windows and Linux systems.

## [Overview](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#overview)

The Offline Reputation Service allows you to supply local reputation entries for MetaDefender Core’s Adaptive Sandbox. Use an allow list to trust selected indicators, such as a URL extracted from a document, when you have reviewed the detection and determined that an exception is appropriate.

Configure a permanent reputation folder in the Core interface and place the applicable reputation files in that folder.

## [Applies to](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#applies-to)

- MetaDefender Core with the embedded Adaptive Sandbox module on Windows or Linux.
- Adaptive Sandbox version **3.3.0** or later, with a Core build that exposes the **Offline Reputation Service folder** setting.

## [Configure URL allowlisting](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#configure-url-allowlisting)

### [1. Create a permanent reputation folder](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#1-create-a-permanent-reputation-folder)

On the server running Adaptive Sandbox, create a dedicated folder outside the MetaDefender Core installation and engine directories. For example:

| Platform | Example folder |
| --- | --- |
| Windows | `C:\Users\CoreAdmin\SandboxReputation` |
| Linux | `/home/coreadmin/SandboxReputation` |

These paths are examples; choose a path appropriate for your deployment. Avoid special characters in the path. A simple path without spaces is recommended. Ensure that the account running the module can read the folder and its files, including access through the parent directories.

**Important:** Do not store customer reputation files inside Core’s installation or engine directories. Files in those locations can be removed or replaced during updates or restarts.

### [2. Create the URL allow list](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#2-create-the-url-allow-list)

Inside the folder, create a plain-text file named exactly:

url_allowed.txt

Add one URL or domain per line. For example:

https://portal.example.com
downloads.example.org

The protocol is optional. The reputation service ignores the protocol when matching an entry, so using `http://`, `https://`, or no protocol does not change the allowlisting behavior.

You may add an optional description after a comma:

portal.example.com,Approved internal portal

URL matching is domain based. Review the scope of the exception before adding an entry; do not assume that a full URL limits the exception to a single page or path.

### [3. Configure the folder in MetaDefender Core](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#3-configure-the-folder-in-metadefender-core)

1. Sign in to the MetaDefender Core management console.
2. Go to **Inventory → Modules → Adaptive Sandbox**.
3. Locate **Offline Reputation Service folder**.
4. Enter the full path to the folder created in step 1. Enter the folder path, rather than the path to `url_allowed.txt`.
5. Save the module configuration.

You do not need to enable **Offline mode** for this feature. A **manual restart** of the MetaDefender Core service is **not required** and the engine will restart the **first** time this feature is enabled and the settings are saved; afterwards, the engine has to be **restarted** for any new changes to take effect.

## [Other supported reputation file names](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#other-supported-reputation-file-names)

The linked Offline Reputation Service reference defines the following allow-list files:

| Entry type | Allow-list file |
| --- | --- |
| MD5 hash | `md5_allowed.txt` |
| SHA-256 hash | `sha256_allowed.txt` |
| IP address | `ip_allowed.txt` |
| Domain | `domain_allowed.txt` |
| URL | `url_allowed.txt` |
| Digital certificate owner | `digicert_owner_allowed.txt` |

Certificate-owner entries have separate formatting requirements and do not support optional descriptions.

## [File formats](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#file-formats)

Each file - except `digicert_owner_allowed.txt` - can contain single-line entries as comma separated data and optional description pairs.

<data>,<optional description>

Examples: **md5_allowed.txt**

d41d8cd98f00b204e9800998ecf8427e,Known good from internal tool, empty file
d41d8cd98f00b204e9800998ecf8427d

Example:**digicert_owner_allowed.txt**

CN="Trusted .Inc", O="Trusted, Inc.", L=San Francisco, ST=California, C=US
## [Import Behavior](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#import-behavior)

- Data is **imported at application startup**, **if a file has changed**.
- If a file changes, **existing data for that type and list is replaced entirely**.
- All internal (system-managed) reputation data is updated after installation.
- External (customer) reputation data can be modified and re-imported at any time.

## [Frequently asked questions](/docs/mdcore/sandbox/how-to-configure-offline-reputation-service-allowlisting-in-meta#frequently-asked-questions)

**Q: Which file path should I use for the allowlist file?**

You can store the allowlist file in any suitable location, subject to the following restrictions:

- Do not store it in the MetaDefender Core installation folders, as files in these folders may be removed or replaced during updates or service restarts.
- Ensure the path contains no spaces or special characters.

A dedicated folder under your user profile is a suitable location.

**Q: Do I need to enable Offline mode?**

No. This feature works regardless of whether Offline mode is enabled.

**Q: Should I include the protocol, such as HTTP or HTTPS, when adding a URL allow/block?**

The protocol is optional. The reputation service ignores it, so allowlist and blocklist entries apply whether the protocol is included, omitted, or different from the protocol used in the request.

**Q: Do I need to restart the MetaDefender Core service after making these changes?**

No. A manual service restart is not required. The engine will restart the **first** time the settings are saved, and afterwards the engine has to be restarted for any new changes to take effect.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
