<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-to-persist-files-and-applications-across-metadefender-kiosk- -->

# How to persist files and applications across MetaDefender Kiosk Hardened Image upgrades and what persists by default?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to MetaDefender Kiosk Hardened Image deployments running:

- **Kiosk Hardened Image 25.07.1 or above** — required for the *Preserved folders* and *Post action* upgrade settings.
- **MD Kiosk 4.7.7 or above** — required to consume the above feature from the Kiosk Web Management Console.

For older Hardened Image versions, the *Preserved folders* and *Post action* fields are not exposed in the Console — the only option for custom applications is to re-install them manually after each Hardened Image upgrade.

## [**Summary**](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-persist-files-and-applications-across-metadefender-kiosk-#summary)

The MetaDefender Kiosk Hardened Image is a locked-down, customized Windows OS bundle. A Hardened Image upgrade is **not** an in-place Windows update — the OS partition is effectively replaced with the new image, and only a defined set of system and product settings is backed up and restored automatically.

As a result:

- **Applications installed by the customer on the Hardened Image (Windows-side custom apps) are not preserved across an image upgrade.** The Windows registry, services, scheduled tasks, system folders, and auxiliary files written by an installer are wiped together with the rest of the OS.
- However, MetaDefender Kiosk does support a **"Preserved folders"** option and a **"Post action"** batch script that run automatically after each Hardened Image upgrade. Used together, these two features let administrators **store installer payloads and re-install custom applications automatically** as part of every upgrade cycle.

This article explains what persists by default, what does not, and the recommended pattern for re-deploying custom applications cleanly after each upgrade.

---

## [**Background — what the Hardened Image upgrade actually does**](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-persist-files-and-applications-across-metadefender-kiosk-#background--what-the-hardened-image-upgrade-actually-does)

When the Hardened Image is upgraded (either automatically from My OPSWAT, or manually from a local/networked folder), Kiosk performs the following steps:

1. **Backup phase** — Kiosk backs up the configured system and product settings, plus any folders the administrator has listed under *Preserved folders*. A snapshot of the current state is also written to a separate partition.
2. **Image swap** — The Windows partition is replaced with the new Hardened Image bundle (new Windows build, new Kiosk and Core versions, refreshed drivers and BIOS).
3. **Restore phase** — The backed-up settings and preserved folders are restored onto the new image.
4. **Post action** — If a post-upgrade batch script is provided, Kiosk executes it after restoration completes.

Because the Windows partition itself is replaced, anything that lived only inside Windows (installed apps, registry keys, scheduled tasks, Windows services not tied to OPSWAT products) does not survive — unless it is recreated by the post-upgrade script.

---

## [**What persists automatically (no configuration required)**](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-persist-files-and-applications-across-metadefender-kiosk-#what-persists-automatically-no-configuration-required)

The following items are backed up and restored automatically by Kiosk during a Hardened Image upgrade:

**System settings**

- Computer host name
- Windows local administrator accounts (only when the corresponding password is provided in the *Windows account password* field of the upgrade settings)
- System hosts file (`C:\Windows\System32\drivers\etc\hosts`)
- Trusted Windows certificates from the Certificates MMC snap-in
- Network settings — DHCP/static, IP address, and Wi-Fi network (Wi-Fi networks that require user credentials are not supported)

**MetaDefender product configuration**

- Kiosk and Core licenses
- Kiosk and local Core configurations
- Kiosk session history
- Quarantined files from the locally-integrated MD Core
- Kiosk User Management settings
- HTTPS certificate and secure connection settings
- Kiosk branding and logo customization
- Instance management on My OPSWAT (if applicable)

> **Static IP** is included in the Network settings group above and will be preserved across Hardened Image upgrades without additional configuration.

---

## [**What does NOT persist automatically**](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-persist-files-and-applications-across-metadefender-kiosk-#what-does-not-persist-automatically)

- Custom Windows applications installed by the customer (Office, browsers, monitoring agents, productivity tools, third-party utilities, in-house tools, etc.)
- Registry keys and values written by those installers
- Windows services, scheduled tasks, and startup entries created outside the OPSWAT product set
- Files written to system folders (`C:\Program Files*`, `C:\Windows`, `C:\Users\...` outside the preserved Kiosk admin profile)
- Domain-join state — domain-joined system settings are explicitly not restored
- Standard (non-administrator) Windows user accounts
- BIOS rollback target — when reverting to a previous Hardened Image version, the BIOS is **not** rolled back

A "preserved folder" is a *file-level* preservation only. Placing a fully installed application's program folder inside a preserved folder will **not** result in a functional application after the upgrade, because the supporting registry entries, services, and auxiliary files outside that folder will be missing.

---

## [**Recommended pattern — Preserved folder + Post-upgrade re-install script**](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-persist-files-and-applications-across-metadefender-kiosk-#recommended-pattern--preserved-folder--post-upgrade-re-install-script)

The supported way to keep custom applications available across Hardened Image upgrades is:

1. **Store the installer payloads** (MSI/EXE installers, configuration files, certificates, any static assets) inside a folder configured as a *Preserved folder*.
2. **Store an idempotent batch script** inside the same preserved folder that re-installs each application silently if it is not already present.
3. **Point the *Post action* field** at that batch script so Kiosk runs it automatically after each successful Hardened Image upgrade.

This design has two important properties:

- The installer payload itself is small relative to a full application install and survives the image swap intact.
- The script re-installs the applications fresh on top of the new Hardened Image, so registry entries, services, and any other supporting state are recreated cleanly — exactly as they would be on a brand-new install.

### [**Step-by-step configuration**](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-persist-files-and-applications-across-metadefender-kiosk-#step-by-step-configuration)

1. **Prepare the deployment payload on the Kiosk device**

Create a dedicated folder on a non-system drive or a stable path that the administrator controls — for example:

`C:\OPSWATCustom\Deploy\`

Inside that folder, place the application installers, any config files they need, and a re-install script (covered below). Keep the structure flat and predictable; nested paths are fine, but avoid spaces and special characters in folder names.

> **Note:** This folder is created and populated by the administrator outside the Kiosk Console — Kiosk does not create it for you. It can sit on the Hardened Image OS partition; what matters is that it is listed under *Preserved folders* before the next upgrade runs.

2. **Configure Preserved folders in the Kiosk Console**

1. Open the Kiosk Web Management Console.
2. Navigate to **Configuration > System Upgrade**.
3. Under **Preserved folders**, add the full path of the folder created in step 1 (e.g., `C:\OPSWATCustom\Deploy\`).
4. Save the configuration.

From this point on, every Hardened Image upgrade will back up the contents of that folder before the image swap and restore it onto the new image.

3. **Configure the Post action script**

1. In the same **Configuration > System Upgrade** page, locate the **Post action** field.
2. Provide the full path to the batch script stored inside the preserved folder (e.g., `C:\OPSWATCustom\Deploy\redeploy.bat`).
3. Save the configuration.

Kiosk will execute this script automatically after a successful Hardened Image upgrade. The script runs with the privileges granted to the post-upgrade execution context — verify that any silent install commands inside the script are compatible with that context.

The contents of the script are the customer's responsibility — Kiosk only invokes it. The script should be authored to run unattended, use the vendor-documented silent-install flags for each installer, and exit cleanly so the post-upgrade phase is not blocked.

---

## [**Limitations and caveats**](/docs/mdkiosk/v4.8.6/knowledge-base/how-to-persist-files-and-applications-across-metadefender-kiosk-#limitations-and-caveats)

Before relying on this pattern in production, confirm the following:

- **Hardened Image lockdown.** The Hardened Image enforces boot hardening, anti-tamper, hot-key restrictions, and similar protections. Some installers may behave differently — or refuse to run — on a hardened OS. Test each installer on a representative Kiosk device before adding it to the redeploy script.
- **No remote Core preservation.** Backup and restore covers only the locally-integrated MetaDefender Core. If the Kiosk is integrated with a remote Core (the value under *Configuration > Integration > MetaDefender Core* is anything other than `localhost`, `127.0.0.1`, or blank), the Core configuration is not part of the backup/restore set.
- **BitLocker is supported on the Hardened Image but must be temporarily disabled before an upgrade.** BitLocker can be enabled on Hardened Image devices for at-rest disk protection, however the Hardened Image upgrade workflow does not currently support upgrading while BitLocker is active — the upgrade will fail if BitLocker is enabled on the C: drive. The supported approach is to suspend or disable BitLocker before initiating the upgrade and re-enable it once the upgrade completes successfully. See KCM-1805 for the related failure signature.
- **Disk space.** At least 40% free space is required on the C: drive to accommodate the upgrade snapshot. The image download itself is approximately 10 GB. Preserved folders sit on top of that requirement.
- **Domain-joined machines.** Domain-join state is not restored after the upgrade. If custom applications depend on domain authentication, the device will need to be re-joined before the redeploy script can succeed.
- **Standard user accounts.** Only Windows administrator accounts are preserved (and only when the password is supplied in the *Windows account password* field). Standard user profiles and their per-user app installs will not return.
- **Post action execution context.** The post-upgrade script runs in the context the Kiosk upgrade workflow provides. Operations that require an interactive user session (e.g., installers that demand HKCU writes, GUI prompts, or per-user shortcuts) may not behave as they would during a manual install.
- **Rollback behavior.** When rolling back to a previous Hardened Image version using the *Upgrade History* rollback action, BIOS firmware is not rolled back.

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
