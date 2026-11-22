<!-- source: https://www.opswat.com/docs/mdmft/installation/updating-metadefender-managed-file-transfer -->

# Backup MetaDefender Managed File Transfer

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This page applies to a **standalone** MetaDefender Managed File Transfer™ (MetaDefender® MFT) v3 installation. It explains what to back up, how to restore MetaDefender® MFT on the same server or at a disaster recovery (DR) site, and how to test the procedure safely. For an HA cluster, see [High Availability](https://www.opswat.com/docs/mdmft/high-availability/high-availability); HA protects against the failure of one node, not against losing a whole site (see [HA is not disaster recovery](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#ha-is-not-disaster-recovery)).

MetaDefender® MFT does not back itself up on a schedule. The installer and an encryption key change take database backups of their own, but only to roll back that operation if it fails; they are not recovery points. You need your own backups of every component below, and you need to be able to restore all of them **to the same point in time**.

## [What makes up an MetaDefender® MFT installation](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#what-makes-up-an-product_name_short-installation)

| Component | Where it is | What it holds |
| --- | --- | --- |
| Encryption secret | `C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Services\secret.bin` (default install folder) | The secret that protects the database connection strings and the other secrets MetaDefender® MFT stores (storage credentials, directory and email passwords, SSO and MFT-to-MFT keys). A database backup cannot be used without the matching `secret.bin`. It is replaced every time the encryption key is changed or rotated. |
| Rotated encryption keys | The folder set as **Path to save rotated keys** under **Settings → Security → Encryption**, if encryption key rotation is enabled | A copy of each file encryption key that a scheduled rotation creates. A restore does not need them when `secret.bin` and the databases match, but they are as sensitive as `secret.bin`. |
| Service configuration | In the install folder: the `Services` folder (`*.exe.config`, `appsettings.json`, `cache.appsettings.json`, `node-manager.appsettings.json`, `config_meta_data.json`) and the `WebServer` folder (`nginx.conf`, `conf\dynamic.conf`) | Encrypted database connection strings, service and web server settings. |
| Web server certificate | The certificate, key and password files that `WebServer\conf\dynamic.conf` points to, wherever you stored them | The TLS certificate of the MetaDefender® MFT web interface. MetaDefender® MFT does not copy these files into its install folder. |
| Customized texts and images | `WebClient\assets\i18n` and `WebClient\assets\img` in the install folder, if you changed them | Your branding and wording changes. |
| Databases | Microsoft SQL Server: `sft_conn` and `sft_data` | Users, settings, file and share records, workflows, audit log, license record. |
| File storage | The storage configured under **Settings → File Storage**: a local folder, a network share (SMB), an Amazon S3 bucket or an S3-compatible bucket | The uploaded files. Files are not stored in the database. |
| License | Activated against the server's deployment ID | See [Licensing on restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#licensing-on-restore). |

### [Keep the backup set consistent](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#keep-the-backup-set-consistent)

The databases and the file storage describe each other: every file in storage has a record in `sft_data`, and the encryption secret must match the databases. Restore all components from the same point in time:

- If the databases are older than the storage, storage holds files that MetaDefender® MFT does not know about.
- If the storage is older than the databases, MetaDefender® MFT lists files that no longer exist, and downloads fail.
- If `secret.bin` and the databases come from either side of an encryption key change, MetaDefender® MFT cannot decrypt its connection strings and stored credentials.
- Never combine an MetaDefender® MFT server or installer of one version with databases from another version. See [What goes undetected](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#what-goes-undetected).

Take the database and storage backups as close together as possible, ideally in a quiet period, and keep a record of the exact MetaDefender® MFT version (as shown in Windows **Apps** or **Programs and Features**) with each backup set.

## [Backing up](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#backing-up)

### [Encryption secret and configuration](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#encryption-secret-and-configuration)

1. Copy `secret.bin`, the configuration files, the web server certificate files and any customized texts and images (see the table above) to a secured location that is **separate** from the MetaDefender® MFT server. The `Services` folder's `Logs` and `JobLogs` subfolders are not needed.
2. Copy them **every time you back up the databases**, for example with a scheduled task on the MetaDefender® MFT server that runs right after the database backup. Every encryption key change, whether manual (**Change encryption key**) or a scheduled rotation, replaces `secret.bin` and re-encrypts the secrets in the database. A `secret.bin` from before a key change cannot be used with a database backup from after it, and the other way round.
3. If encryption key rotation is enabled, also back up the **Path to save rotated keys** folder.
4. Protect these copies like a password: `secret.bin` together with a database backup gives access to every secret stored in MetaDefender® MFT. Keep them apart from the database backups.

The encryption key you can download under **Settings → Security → Encryption** is not `secret.bin` and cannot replace it in a restore. The settings export holds settings only, without users, files or the encryption secret, so it does not replace a database backup either.

Also record, for each backup set: the MetaDefender® MFT version, the server's hostname and IP address, the SQL Server name, the storage paths or bucket names, and the license key.

### [Databases](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#databases)

Back up `sft_conn` and `sft_data` with SQL Server native backups (`BACKUP DATABASE`), on the same schedule.

| Where SQL Server runs | How to schedule the backups |
| --- | --- |
| A separate SQL Server (Standard or Enterprise) | A SQL Server Agent job or maintenance plan. |
| SQL Server Express (on the MetaDefender® MFT server or elsewhere) | SQL Server Express has no SQL Server Agent. Use Windows Task Scheduler to run `sqlcmd`, as in the example below. |
| SQL Server Express LocalDB (older installations only) | MetaDefender® MFT does not include a database server, and current versions do not support LocalDB: from 3.11.5 the installer refuses to install or upgrade on it. If an older installation still runs on LocalDB, migrate it to SQL Server first: see [SQL Server Express LocalDB migration](https://www.opswat.com/docs/mdmft/knowledge-base/sql-server-express-localdb-migration). |

Example, run as an account with backup rights on both databases:

sqlcmd -S <sql-server> -E -Q "BACKUP DATABASE [sft_conn] TO DISK = N'D:\MftBackup\sft_conn.bak' WITH INIT, CHECKSUM; BACKUP DATABASE [sft_data] TO DISK = N'D:\MftBackup\sft_data.bak' WITH INIT, CHECKSUM"

Copy the `.bak` files off the server after each run. Adjust authentication (`-E` for Windows authentication, `-U`/`-P` for a SQL login) and encryption options to your environment.

MetaDefender® MFT creates its databases with the simple recovery model, so you can restore to the time of a full or differential backup. If you need finer recovery points, your database administrator can switch the databases to the full recovery model and schedule transaction log backups.

Do not rely on a VM snapshot for the databases

If SQL Server runs on the MetaDefender® MFT server, a hypervisor snapshot is safe for the databases only if it is application-consistent (taken through VSS with the SQL Server VSS Writer). Even then, keep native backups: they are the only copy you can restore to a different SQL Server and verify on their own.

### [File storage](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#file-storage)

| Storage type | How to back it up |
| --- | --- |
| Local folder | Back up the folder or the volume it is on. Keep it on a separate drive from the operating system. A full backup of the MetaDefender® MFT server includes it. |
| Network share (SMB) | Snapshots or backups on the file server or NAS. A backup of the MetaDefender® MFT server does **not** include it. |
| Amazon S3 | S3 Versioning, plus Cross-Region Replication or AWS Backup if you need a copy outside the region. |
| S3-compatible | The equivalent versioning or replication feature of your storage vendor. |

Schedule the storage backup to match the database backup.

### [MetaDefender® MFT server](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#product_name_short-server)

Back up the whole server (VM backup or full OS backup) so that you can restore it as it was. If you cannot, you can rebuild the server instead: see [Option B](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#option-b-rebuild-the-server). Rebuilding needs the encryption secret, the configuration files and the exact MetaDefender® MFT version recorded with the backup set.

## [Restoring](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#restoring)

There are two ways to bring MetaDefender® MFT back:

- **Option A: restore the MetaDefender® MFT server** from its VM or OS backup. Use it when the server backup is available. The restored server keeps its hostname and its MetaDefender® MFT identity, and, if it also keeps its MAC address, its license.
- **Option B: rebuild the MetaDefender® MFT server.** Install the same MetaDefender® MFT version on a new server and attach it to the restored databases. Use it when there is no server backup, or when you move to new hardware. The new server gets a new MetaDefender® MFT identity, so expect to activate the license again.

### [Before you start](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#before-you-start)

1. **Make sure the original MetaDefender® MFT server is off and stays off**, or that the restored server cannot reach the original's databases and storage. MetaDefender® MFT does not detect a second copy of itself. See [What goes undetected](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#what-goes-undetected).
2. Restore `sft_conn` and `sft_data` to SQL Server, from the same backup set as the storage. If you restore to a different SQL Server and MetaDefender® MFT uses a SQL login, map the database users to the login on the new server (`ALTER USER ... WITH LOGIN = ...`); the login needs `db_owner` on both databases.
3. Restore the file storage **to the same path or bucket** it had before. MetaDefender® MFT finds each file from the storage settings in the database (share path or bucket, plus the file's name in it), and it uses the credentials stored there, so those credentials must work at the DR site too. If the share path or bucket has to change, use a DNS alias for the file server, or contact OPSWAT Support before you start MetaDefender® MFT.

### [Option A: restore the server](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#option-a-restore-the-server)

1. Restore the server from its backup, with its original MAC address. Start it with the network adapter disconnected in the hypervisor (not removed; see [Licensing on restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#licensing-on-restore)).
2. Stop the MetaDefender® MFT services and set their startup type to **Manual** until you have finished the steps below. The services are `mftHelper` (which also runs the web server), `mftREST`, `mftNext`, `mftProcessor`, `mftCache` and `mftNodeManager`; all of them depend on `mftHelper`. In an elevated PowerShell prompt:

   Get-Service mft* | Set-Service -StartupType Manual
   Stop-Service mftHelper -Force # also stops the services that depend on it
3. Connect the server to the network. Check its IP address, DNS records and the names on its TLS certificate.
4. If the server is joined to a domain, repair its trust relationship before anything uses Windows authentication (SQL Server, AD synchronization, SSO). A server restored from an older backup can have an out-of-date computer account password. In an elevated PowerShell prompt:

   Test-ComputerSecureChannel -Repair -Credential (Get-Credential)
5. If the SQL Server name or port is different from before, repoint MetaDefender® MFT with the [Database Configuration Tool](https://www.opswat.com/docs/mdmft/configuration/database-credentials-tool), from an elevated prompt in the `Tools` folder of the install folder:

   .\SftDatabaseConfigurationTool.exe --server <new-sql-server>

   The tool checks the new connection, stops the services, updates the connection string in every place MetaDefender® MFT stores it, and starts the services again. If anything fails, it rolls back. Do not edit the configuration files by hand: the connection string is also stored, encrypted, in the `sft_conn` database. The tool decrypts the current connection string with `secret.bin`, so it fails if `secret.bin` does not match the restored databases. It is not available for LocalDB installations. As an alternative, keep the old SQL Server name and point it at the new server with a DNS alias.
6. Set the MetaDefender® MFT services back to **Automatic** and start them:

   Get-Service mft* | Set-Service -StartupType Automatic
   Start-Service mft*
7. Check the license (see [Licensing on restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#licensing-on-restore)), then run the [checks after a restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#checks-after-a-restore).

### [Option B: rebuild the server](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#option-b-rebuild-the-server)

1. Prepare a Windows Server that meets the [system requirements](https://www.opswat.com/docs/mdmft/installation/system-requirements). Give it the original hostname if you can: the hostname is part of the license's deployment ID, and URLs, certificates and partner systems refer to it.
2. Copy the backed-up `secret.bin` to the new server.
3. Install **the same MetaDefender® MFT version** that the backup set was taken with, and attach it to the restored databases. In the installer, choose to use the existing databases and the existing encryption secret; from the command line, use `DbInstallMode=CreateToExisting` with `PathToSecret=<path to secret.bin>` and the database server options. See [Installing from the command line](https://www.opswat.com/docs/mdmft/installation/installing-from-command-line). An older installer refuses databases from a newer version. A newer installer upgrades the databases during installation, which adds an upgrade to your recovery, so prefer the same version.
4. Re-apply what is set up on the server itself rather than in the database: the web server certificate files, customized texts and images, firewall rules, and any changes you had made to the configuration files (compare them with the backed-up copies).
5. Sign in as an administrator and activate the license (see [Licensing on restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#licensing-on-restore)).
6. Run the [checks after a restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#checks-after-a-restore).

### [Checks after a restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#checks-after-a-restore)

Before you let users and partner systems back in:

1. Sign in as an administrator. Check that **Settings → Security → License** shows a valid license.
2. In **Settings → File Storage**, check that the active storage is reachable. Download a file that was uploaded before the backup point.
3. Upload a new file and download it again. Check that it is scanned by MetaDefender Core.
4. Check the connections to your directory service (AD/LDAP), the email server and your SSO provider. If the server's address changed at the DR site, also update it wherever other systems point to MetaDefender® MFT: DNS, the SSO provider's redirect URLs and MFT-to-MFT peers.
5. Review workflows, scheduled jobs and MFT-to-MFT connections before you reconnect them to their destinations. Jobs that ran after the backup point will run again (see [Known limitations](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#known-limitations)).

## [Licensing on restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#licensing-on-restore)

MetaDefender® MFT's license is activated against the server's **deployment ID**, shown under **Settings → Security → License**. The deployment ID is calculated from the server's **hostname** and the **MAC addresses of its network adapters**. If it changes, the license is no longer valid on that server and has to be activated again. Until then, MetaDefender® MFT keeps running and administrators can sign in, but other users cannot sign in and nobody can upload files.

### [Keep the deployment ID unchanged](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#keep-the-deployment-id-unchanged)

| Change on the restored server | Deployment ID |
| --- | --- |
| Same hostname, same network adapter with the same MAC address | Unchanged: the license stays valid |
| Different hostname | Changes |
| Different MAC address: a new or replaced network adapter, a VM restored or cloned as a new VM with a newly generated MAC address, or a MAC address that the hypervisor assigns dynamically (for example in Hyper-V, when the VM starts on another host) | Changes |
| A network adapter added, removed or disabled in Windows | Can change |
| Rebuilt server ([Option B](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#option-b-rebuild-the-server)) | Changes, and the license record belongs to the original server, so activate again |
| A different VM UUID or different CPU, memory or disks | Not part of the deployment ID |

To restore without activating again:

- **Give the MetaDefender® MFT server's network adapter a static MAC address** in the hypervisor, and restore the VM with that MAC address. This is the most common reason a restored or migrated MetaDefender® MFT server loses its license. Because the restored server has the original's MAC address, never run it on the same network as the original.
- **Keep the hostname** and the same number of network adapters.
- If the server uses **NIC teaming**, give the team a static MAC address as well: a team's MAC address can change between restarts.
- When you start a restored server without network access, **disconnect** its network adapter in the hypervisor. Do not remove the adapter or disable it in Windows: that changes the deployment ID.

### [When you have to activate again](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#when-you-have-to-activate-again)

1. **If the license was activated online** and the server has internet access, click **Deactivate License** first. This releases the activation of the original deployment ID on the OPSWAT activation server. Then click **Activate License**.
2. **If the license was activated offline**, if the restored server has no internet access, or if deactivation fails: activate with the new deployment ID (**Offline Activation** through My OPSWAT works from any machine with internet access), and ask OPSWAT Support to release the old deployment ID. Deactivating an offline-activated license in MetaDefender® MFT only removes it from MetaDefender® MFT; the activation stays in use until Support releases it.
3. If your activation key has no free activation left, the new deployment ID cannot be activated until Support releases the old one. For an air-gapped DR site, or if you cannot wait for Support during a disaster, agree the procedure with OPSWAT, or ask your account team about an extra activation for DR, before you need it.

See [License Activation](https://www.opswat.com/docs/mdmft/configuration/license-activation) for the activation steps.

A standby MetaDefender® MFT server that runs permanently at the DR site is a separate installation and needs its own license. Check your entitlement with your OPSWAT account team.

## [Testing your disaster recovery procedure](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#testing-your-disaster-recovery-procedure)

Test the restore regularly, and never in a way that lets the restored copy reach production. A restored MetaDefender® MFT server is configured to talk to your production SQL Server (if it is remote), your production file storage, MetaDefender Core, the email server, your directory service, MFT-to-MFT peers and every workflow destination. MetaDefender® MFT has no maintenance mode: as soon as its services start, scheduled workflows run, queued emails are sent and MFT-to-MFT requests are forwarded. The isolated network is what keeps the test away from production.

1. Build an isolated test network with no route to production and **no outbound internet access** (otherwise a restored server can still reach an S3 bucket).
2. Restore copies of `sft_conn`, `sft_data` and the file storage into the isolated network.
3. Restore the MetaDefender® MFT server into the isolated network with its network adapter disconnected in the hypervisor, stop the MetaDefender® MFT services and set them to **Manual**.
4. Connect the adapter to the isolated network and point MetaDefender® MFT at the database copies with `SftDatabaseConfigurationTool.exe --server <test-sql-server>`. If the server is domain-joined, the isolated network needs a domain controller too, or Windows authentication fails.
5. Make the storage copy available under the same path (for a network share, a test file server with the same name in the isolated DNS).
6. Start the services and run the [checks after a restore](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#checks-after-a-restore).

### [What goes undetected](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#what-goes-undetected)

- **Version mismatch.** The MetaDefender® MFT services do not check the database version when they start; only the installer does. A server restored from an older backup starts against newer databases, then fails on individual operations. Always restore the server and the databases from the same backup set.
- **A second copy of the same server.** A restored server is the same MetaDefender® MFT node as the original. If both run against the same databases, MetaDefender® MFT does not warn you: both run workflows, retention, MFT-to-MFT forwarding and notifications on the same data and storage.

### [Cloning the MetaDefender® MFT server](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#cloning-the-product_name_short-server)

A clone of the MetaDefender® MFT server is a copy of the same MetaDefender® MFT node. That is what you want when the clone **replaces** the original, and for an isolated DR test. Do not clone the MetaDefender® MFT server to create a **second, independent** MetaDefender® MFT server, such as a test or standby server: the clone keeps the original's MetaDefender® MFT identity, and this identity survives uninstalling MetaDefender® MFT from the clone. Install an independent server on a clean Windows installation instead, or contact OPSWAT Support before installing MetaDefender® MFT on a clone.

## [Known limitations](/docs/mdmft/installation/updating-metadefender-managed-file-transfer#known-limitations)

- **Data loss window.** Everything after the last consistent backup set is lost: uploads, shares, settings changes and audit entries. Links that users received after that point stop working.
- **Repeated work.** The restored databases do not know what happened after the backup point. Workflows that run on a frequency start as soon as the services start. A transfer workflow checks each destination file and, depending on its settings, skips it, overwrites it or keeps a second copy. MFT-to-MFT requests that were forwarded after the backup point are forwarded again (the target reports files it already has), and emails that were still queued at the backup point are sent again.
- **Encryption key changes.** Each key change or scheduled rotation replaces `secret.bin`. A `secret.bin` and a database backup from either side of a key change cannot be used together, so back them up together.
- **No built-in backup or DR.** MetaDefender® MFT has no scheduled backup and no automated failover to another site. The database backups that the installer and encryption key changes take exist to roll back that operation, not to recover from a disaster.
