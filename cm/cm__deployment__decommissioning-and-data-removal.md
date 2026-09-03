<!-- source: https://www.opswat.com/docs/cm/deployment/decommissioning-and-data-removal -->

# Decommissioning and Data Removal

This page describes how to completely decommission a self-hosted My OPSWAT Central Management (MOCM) deployment and remove all of its data from the host. Use it when retiring a deployment, returning hardware, or otherwise ensuring no My OPSWAT Central Management data remains.

Applies to the standalone / appliance deployment: **MSI (Windows)**, **RPM (RHEL)**, and **OVA virtual appliance**.

> **Important:** Uninstalling My OPSWAT Central Management does **not** delete your data. The data directories and any backups remain on the host after a standard uninstall. To remove all data, complete the full procedure below.

## Before you begin

- **This procedure is irreversible.** Everything is permanently deleted, including your configuration, enrolled-endpoint records, and the web-console TLS certificate. If you may need any of it later — for example to rebuild the deployment elsewhere — create a backup and copy it off the host **before** you start. See [Backup and Restore](https://www.opswat.com/docs/cm/configurations/backup-and-restore).
- **You need administrative access:** a local Administrator account on Windows, or `root` / `sudo` on RHEL and the OVA appliance.
- **Set aside 15–30 minutes**, plus any additional time your organization's media-sanitization standard requires.
- **Scope:** this page covers only the data stored on the My OPSWAT Central Management host. It does not cover license deactivation or transfer, or removing the OPSWAT agent from your endpoints. Contact [OPSWAT Support](https://www.opswat.com/support) if you need to release a license or move it to a new deployment.

### Using the OVA virtual appliance? Take the short path

If you deployed the OVA and do not need to keep the virtual machine, you do not need to uninstall anything. Instead:

1. Complete **Step 1** below to locate any backups or support packages stored outside the appliance.
2. Power off the VM and delete it from your hypervisor, choosing the option that also deletes its virtual disks.
3. Complete **Step 6** to sanitize the datastore if your security policy requires it.

Deleting the VM removes all data, configuration, and files in one action. Follow the full procedure below only if you need to keep the VM running after removing My OPSWAT Central Management.

## Where My OPSWAT Central Management stores data

Find your deployment type below. These are the locations you remove in Step 3.

### Windows (MSI)

| What | Location |
| ---- | ---- |
| Application, data, configuration, and backups | `C:\Program Files\OPSWAT\MOCM` |
| Support packages | `mocm-support-package-<timestamp>.zip`, inside `C:\Program Files\OPSWAT\MOCM` |
| Logs | `C:\ProgramData\OPSWAT\MOCM\Logs` |
| Registry entries | `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MOCM` |

### RHEL (RPM)

| What | Location |
| ---- | ---- |
| Application | `/opt/mocm` |
| Data and backups | `/var/lib/mocm` |
| Support packages | `mocm-support-package-<timestamp>.tar.gz`, inside `/opt/mocm/lib` |
| Configuration | `/etc/opt/mocm` |
| Logs | `/var/log/mocm` |

### OVA virtual appliance

| What | Location |
| ---- | ---- |
| Application | `/var/opt/mocm` |
| Data and backups | `/var/lib/mocm` |
| Support packages | `mocm-support-package-<timestamp>.tar.gz`, inside the application folder |
| Configuration | `/etc/opt/mocm` |
| Logs | `/var/log/mocm` |

> > **Note:** Backups and support packages exist only if you created them. Copies you downloaded from the web console, sent to OPSWAT Support, or moved to another system are **not** stored in the locations above — Step 1 helps you find them.

## Decommissioning steps

### Step 1: Find backups and support packages

Do this **first**, while the folders still exist. Two kinds of file need attention:

- **Backups** (`.CMX`). Scheduled backup is off by default and runs only if it was enabled under **Settings → Servers → Backup**, but backups can also be created and downloaded manually at any time — so check even if you never set up a schedule.
- **Support packages**. If you ever generated one for OPSWAT Support, it bundles logs and configuration into a single archive. Those archives stay on the host until you delete them.

Search the host for both:

- **Windows (PowerShell as Administrator):**

  ```powershell
  Get-ChildItem -Path C:\ -Include *.CMX, mocm-support-package-*.zip -Recurse -ErrorAction SilentlyContinue | Select-Object FullName
  ```
- **RHEL / OVA:**

  ```bash
  sudo find / \( -name '*.CMX' -o -name 'mocm-support-package-*' \) 2>/dev/null
  ```

Note the results. Files inside the folders listed above are removed in Step 3, but **copies you downloaded or moved elsewhere are not** — for example on a file share, a backup server, a USB drive, an administrator's workstation, or in an email you sent to OPSWAT Support. Delete those separately.

### Step 2: Uninstall My OPSWAT Central Management

- **Windows:** go to *Control Panel → Programs and Features*, select **My OPSWAT Central Management**, and choose **Uninstall**. To uninstall silently instead, run `msiexec /x <path-to-installer>.msi /quiet`, replacing the path with the location of the installer file you originally used.
- **RHEL:** find the installed package name, then remove it:

  ```bash
  rpm -qa | grep -i mocm
  sudo dnf remove <package-name>
  ```
- **OVA virtual appliance:** there is no separate uninstall program for the appliance. You remove it by deleting the virtual machine — see **Using the OVA virtual appliance? Take the short path** above.

Uninstalling removes the software and stops its services, but leaves your data on disk. Continue with the remaining steps.

### Step 3: Delete all My OPSWAT Central Management directories

This is the step that removes your data: all stored records (including the web-console TLS certificate and private key), your configuration, your logs, and any backups or support packages kept in these folders.

Delete these folders and everything inside them:

- **Windows:** `C:\Program Files\OPSWAT\MOCM` and `C:\ProgramData\OPSWAT\MOCM`
- **RHEL:** `/opt/mocm`, `/var/lib/mocm`, `/etc/opt/mocm`, `/var/log/mocm`
- **OVA:** `/var/opt/mocm`, `/var/lib/mocm`, `/etc/opt/mocm`, `/var/log/mocm`

Also delete any backups or support packages stored outside these folders, using the list you gathered in Step 1.

### Step 4: Delete the Windows registry subtree (Windows only)

Open *Registry Editor* (`regedit`) and delete `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MOCM`.

To do the same from an elevated PowerShell prompt:

```powershell
Remove-Item -Path 'HKLM:\SOFTWARE\OPSWAT\MOCM' -Recurse -Force
```

### Step 5: Verify that nothing remains

Run the checks below. Every one should report that the item is gone.

- **Windows (PowerShell as Administrator):**

  ```powershell
  Test-Path 'C:\Program Files\OPSWAT\MOCM'        # expect: False
  Test-Path 'C:\ProgramData\OPSWAT\MOCM'          # expect: False
  Test-Path 'HKLM:\SOFTWARE\OPSWAT\MOCM'          # expect: False
  Get-ChildItem -Path C:\ -Include *.CMX, mocm-support-package-*.zip -Recurse -ErrorAction SilentlyContinue   # expect: no results
  Get-Service | Where-Object { $_.DisplayName -like '*OPSWAT*' }                                              # expect: no results
  ```
- **RHEL / OVA:**

  ```bash
  ls -d /opt/mocm /var/opt/mocm /var/lib/mocm /etc/opt/mocm /var/log/mocm 2>/dev/null   # expect: no output
  sudo find / \( -name '*.CMX' -o -name 'mocm-support-package-*' \) 2>/dev/null         # expect: no output
  systemctl list-units --all | grep -i mocm                                             # expect: no output
  ```

If your organization requires evidence of decommissioning, save the output of these checks along with the date and the name of the person who performed the procedure.

### Step 6: Sanitize the underlying storage

My OPSWAT Central Management does not provide an in-product secure-erase function — it does not perform multi-pass overwrite or cryptographic erase. Deleting the folders removes the data logically, which is enough for most cases. If your security policy requires media sanitization — for example, before returning or disposing of hardware — perform it at the operating-system, storage, or hypervisor layer:

- **OVA:** sanitize the virtual appliance's virtual disks, or the datastore holding them.
- **MSI / RPM:** sanitize the underlying disk or volume per your organization's media-sanitization standard.

## Notes

- **Certificates and keys:** the web-console TLS certificate and private key are stored internally by the product, not as separate files on disk. They are removed when you delete the data directories in Step 3, and no key material remains anywhere else on the host.
- **Configuration exports:** the `.CMX` backup is the only file-based export produced by My OPSWAT Central Management. There is no separate configuration-export format to track down and remove.
- **How deletion works:** when you delete data in My OPSWAT Central Management — an endpoint record, for example — the deletion is permanent. The product does not keep a hidden copy, a recycle bin, or a metadata record of what was removed.

## Related

- [Uninstall My OPSWAT Central Management](https://www.opswat.com/docs/cm/deployment/uninstall-my-opswat-central-management)
- [System Requirements](https://www.opswat.com/docs/cm/deployment/system-requirements)
- [Backup and Restore](https://www.opswat.com/docs/cm/configurations/backup-and-restore)
- [How to Generate a Support Package for My OPSWAT Central Management](https://www.opswat.com/docs/cm/knowledge-base/how-to-generate-a-support-package-for-my-opswat-central-manageme)
