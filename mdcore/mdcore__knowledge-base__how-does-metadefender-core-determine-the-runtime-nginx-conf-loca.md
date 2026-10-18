<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-does-metadefender-core-determine-the-runtime-nginx-conf-loca -->

# How does MetaDefender Core determine the runtime nginx.conf location on Windows?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info:

**Check Your Version:**

This article applies to **all MetaDefender Core releases deployed on Windows**.

## [Issue:](/docs/mdcore/knowledge-base/how-does-metadefender-core-determine-the-runtime-nginx-conf-loca#issue)

After upgrading to MetaDefender Core 5.17.1 or later (see [**Windows Temporary Folder Path Changes for SYSTEM Account**](https://www.opswat.com/docs/mdcore/troubleshooting/windows-temporary-folder-path-changes-for-system-account) for details regarding the Local System account), or configuring the MetaDefender Core service to run under a different Windows account, users may be unable to locate the runtime `nginx.conf` file.

Historically, the runtime configuration was commonly found under:

C:\Windows\Temp\ometascan\nginx.conf

However, depending on the MetaDefender Core version and the account configured to run the service, the runtime configuration may be generated in a different location.

## [Main cause:](/docs/mdcore/knowledge-base/how-does-metadefender-core-determine-the-runtime-nginx-conf-loca#main-cause)

The runtime `nginx.conf` is generated automatically during MetaDefender Core service startup.

The location is determined by the temporary directory resolved for the account configured in the **Log On As** setting of the **OPSWAT MetaDefender Core** service.

For services running as **Local System**:

| MetaDefender Core Version | Runtime Location |
| --- | --- |
| Earlier than 5.17.1 | `C:\Windows\Temp\ometascan\` |
| 5.17.1 and later | `C:\Windows\SystemTemp\ometascan\` |

For services running under **any Windows user account**, the runtime configuration is generated under the temporary directory resolved for that account.

For example:

C:\Users\<username>\AppData\Local\Temp\ometascan\

The exact location depends on the value of the account's **TEMP** environment variable.

## [Resolution:](/docs/mdcore/knowledge-base/how-does-metadefender-core-determine-the-runtime-nginx-conf-loca#resolution)

#### [Step 1. Verify the account running the MetaDefender Core service](/docs/mdcore/knowledge-base/how-does-metadefender-core-determine-the-runtime-nginx-conf-loca#step-1-verify-the-account-running-the-metadefender-core-service)

Open:

services.msc

Locate:

OPSWAT MetaDefender Core

Open **Properties** → **Log On** and identify the account configured to run the service.

---

#### [Step 2. Locate the runtime configuration](/docs/mdcore/knowledge-base/how-does-metadefender-core-determine-the-runtime-nginx-conf-loca#step-2-locate-the-runtime-configuration)

If the service runs as **Local System**:

- MetaDefender Core earlier than **5.17.1**

C:\Windows\Temp\ometascan\

- MetaDefender Core **5.17.1 or later**

C:\Windows\SystemTemp\ometascan\

If the service runs under a **Windows user account**, navigate to that account's temporary directory.

Typical example:

%TEMP%\ometascan\

or

C:\Users\<username>\AppData\Local\Temp\ometascan\

The runtime directory contains files such as:

- `nginx.conf`
- `ometascan-nginx.pid`
- NGINX temporary directories

---

#### [Step 3. If the directory is missing](/docs/mdcore/knowledge-base/how-does-metadefender-core-determine-the-runtime-nginx-conf-loca#step-3-if-the-directory-is-missing)

Restart the **OPSWAT MetaDefender Core** service.

The runtime configuration is regenerated automatically during service startup.

---

### [Notes:](/docs/mdcore/knowledge-base/how-does-metadefender-core-determine-the-runtime-nginx-conf-loca#notes)

- The generated `nginx.conf` is the runtime configuration used by the embedded NGINX instance.
- The runtime `nginx.conf` should **not** be modified directly.
- If custom NGINX configuration is required, follow the supported method for loading additional NGINX configuration files.

---

If Further Assistance is required, please proceed to [log a support case or chat with our support engineer.](https://my.opswat.com/support)
