<!-- source: https://www.opswat.com/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage -->

# Add an SMB-Compatible unit in Linux deployments

> This article is applicable only for MetaDefender Storage Security deployed on Linux distributions. For Windows deployments, see [Add an SMB-Compatible unit in Windows deployments](https://www.opswat.com/docs/mdss/integrations/add-an-smb-compatible-unit-in-windows-deployments).

Starting with version 4.6.0, MetaDefender Storage Security (MDSS) connects to SMB shares on Linux through its **SMB service**, which mounts each share on demand using the SMB/CIFS client built into the Linux kernel. The share is added in MDSS as an **SMB Compatible** storage. No manual mount, `fstab` entry or `cifs-utils` package is needed on the MDSS machine.

> Before 4.6.0, SMB Compatible units on Linux were served by the previous SMB service, which connects to shares over the network without mounting them. That service is still shipped; see *Fallback: the legacy SMB service* below. Mounting the share on the MDSS machine and adding it as an NFS storage unit was the alternative recommended for production; see the last section of this article.

## Prerequisites

- A Linux machine with MetaDefender Storage Security 4.6.0 or later installed.
- An SMB share hosted on a Windows machine, a NAS, or a Linux machine running Samba, reachable from the MDSS machine on TCP port 445 or on the custom port the server uses.
- The `cifs` kernel module available on the MDSS machine (see Step 1).

> SMB over QUIC is not supported at this time - only traditional SMB over TCP connections are compatible.

## Step-by-Step Guide

### Step 1: Make sure the cifs kernel module is available

The SMB service mounts shares with the kernel's CIFS driver, so the module has to be available on the MDSS machine itself; a container cannot load kernel modules. On most distributions the module ships with the kernel and is loaded automatically the first time a share is mounted.

To check that the module is available, run:

```bash
grep cifs /proc/filesystems
```

If the command prints nothing, load the module:

```bash
sudo modprobe cifs
```

To keep it loaded across reboots on machines where automatic module loading is disabled:

```bash
echo cifs | sudo tee /etc/modules-load.d/cifs.conf
```

> `sudo mdss -c start` checks this prerequisite before it pulls the images and stops with instructions when the module is missing. If a storage is added while the module is missing, MDSS reports *The CIFS kernel module is not installed or not enabled on the machine running MetaDefender Storage Security. Install or enable the module, then try again.*

### Step 2: Container privileges

Mounting a filesystem requires the `SYS_ADMIN` capability, and Docker's default AppArmor profile denies mount operations. The `docker-compose.smb.yml` file shipped with MDSS therefore starts the SMB service container with:

```yaml
cap_add:
  - SYS_ADMIN
security_opt:
  - apparmor:unconfined
```

No change is needed for a standard installation. `sudo mdss -c start` verifies after the start that the SMB service container is running with these privileges and reports the exact problem when it is not.

Keep the following in mind if your organization applies a hardening policy to containers:

- `SYS_ADMIN` is granted to the SMB service container only. No other MDSS container receives it.
- `apparmor:unconfined` has no effect on machines without AppArmor. On machines with AppArmor, `sudo mdss -c start` accepts only `unconfined`: with any other profile it stops with the fallback instructions, unless `SKIP_SMB_CHECKS=yes` is set in `/etc/mdss/customer.env`.
- Shares are mounted inside the container's own mount namespace. They never appear on the MDSS machine's filesystem and are released when the container stops.
- Every share is mounted with the `nosuid`, `nodev` and `noexec` options, so nothing stored on the share can be executed inside the container. On Linux kernel 5.10 or later, shares are also mounted with `nosymfollow`, so symbolic links found on the share are not followed.

> If the container runtime cannot grant these privileges (a hardened Docker daemon, a policy engine, or a rootless runtime), the SMB service cannot mount shares. Use the legacy SMB service instead. See *Fallback: the legacy SMB service* below.

### Step 3: Add the SMB account in MDSS

1. Navigate to **Inventory** > **Add New** > **Account**, choose **SMB Compatible** and click **Next**.
2. Give your account a name so you can easily identify it later.
3. Enter the **Username** and **Password** of the account used to connect to the share.
4. Enter the **Host** (host name or IP address of the SMB server) and the **Port**. Leave the port at 445 unless the server listens on a different port.
5. Click **Next**. MDSS verifies the credentials against the server before the account is saved.

> To avoid authentication issues the Username should have one of the following formats: domain users should be `domain\username`, `domain/username` or `username@domain`; local users on the server should be the username alone. Passwords containing `,` `;` `=` or spaces are supported.

> A Samba file server needs to be enabled in order to connect to a Unix-based system share.

### Step 4: Add the SMB unit in MDSS

1. Navigate to **Inventory** > **Add New** > **Unit**, select the account created in Step 3 and click **Next**.
2. Give your unit a name and assign it to a group.
3. Enter the **Share path**: the name of the share, optionally followed by a folder inside it, for example `share` or `share/folder/subfolder`. When a folder is given, only that folder and its subfolders are discovered and scanned.
4. Click **Next** in order to finish the process. MDSS mounts the share once to verify that the path exists and that the account can access it.

> The share path must start with the share name. A path such as `folder/subfolder` without the share name is reported as *The object was not found on the server*. The same rule applies to the partition of a scan on an SMB unit: it replaces the share path, so it must include the share name as well.

## Custom configuration

The SMB service reads its settings from environment variables. To change one, add it to `/etc/mdss/customer.env` in the format `CONFIGURATION_PROPERTY_NAME=VALUE`, save the file and restart MetaDefender Storage Security with `sudo mdss -c restart`. See [Custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration). The defaults suit most deployments.

| Variable | Default | Description |
| ---- | ---- | ---- |
| `SMBSERVICE_MOUNT_DIRECTORY` | `/var/opswat/mdss/smb-mounts` | Directory inside the SMB service container where the shares are mounted. |
| `SMBSERVICE_MOUNT_IDLE_TTL_SECONDS` | `300` | A share that has not been used for this many seconds is unmounted. It is mounted again the next time it is needed. |
| `SMBSERVICE_MOUNT_TIMEOUT_SECONDS` | `60` | Maximum time to wait for a mount to complete. |
| `SMBSERVICE_SMB_SEAL` | `0` | Set to `1` to require SMB 3 encryption on every connection. Servers that do not support encryption then refuse the mount. |
| `SMBSERVICE_MOUNT_UID` / `SMBSERVICE_MOUNT_GID` | Not set | Owner reported for the files on the mount (the `uid` and `gid` mount options). The permissions configured on the server still decide what MDSS can read and write. |
| `SMBSERVICE_MOUNT_OPTIONS` | Not set | Additional CIFS mount options, comma-separated, for example `cache=strict,actimeo=30,echo_interval=30`. Options that the SMB service manages itself (credentials, server address, port, SMB version, security mode, `seal`, `uid`, `gid`) are not accepted here: the service does not start and logs the reason. |
| `SMBSERVICE_DISCOVERY_DEBOUNCE_TIME` | `5` | A file modified less than this many seconds ago is considered still being written and is skipped until the next discovery. Set it to `0` to process files as soon as they are found. On Linux, MDSS cannot reliably detect that another client still has a file open on the share, so this window is the main protection against scanning a partially copied file. Increase it when files are copied to the share by slow clients. |
| `SMBSERVICE_DOWNLOAD_CHUNK_TIMEOUT_SECONDS` | `60` | Maximum wait for each block of data read from the share (30 to 300). On Linux, a read the kernel is blocked on is not interrupted by this timeout: it ends when the kernel gives up on the session, about three minutes with the default settings (see the note below the table). |
| `SMBSERVICE_UPLOAD_CHUNK_TIMEOUT_SECONDS` | `60` | Maximum wait for each block of data written to the share (30 to 300). |

> When an SMB server stops responding in the middle of a transfer, the kernel keeps the session open for about three minutes before it reports the failure. The kernel reconnects on its own once the server answers again. Add `echo_interval=30` to `SMBSERVICE_MOUNT_OPTIONS` to shorten that window.

## Fallback: the legacy SMB service

The SMB service from earlier releases, which reads shares over the network without mounting them, is still shipped as the `smb_legacy` module. It needs no extra container privileges and no kernel CIFS support. The settings above do not apply to it by default: it skips a file that another client still holds open, and uses `SMBSERVICE_DISCOVERY_DEBOUNCE_TIME` only when `SMBSERVICE_FILE_READY_CHECK_MODE=0` is set.

1. Open `/etc/mdss/customer.env` and set `ENABLED_MODULES` to the complete list of modules you want enabled, keeping `smb` in the list and adding `smb_legacy` at the end:

```bash
ENABLED_MODULES=azureblob,amazonsdk,googlecloud,alibabacloud,azurefiles,smb,box,graph,sftp,nfs,mft,ftp,oraclesdk,smb_legacy
```

2. Restart MetaDefender Storage Security:

```bash
sudo mdss -c restart
```

> `smb` has to stay in the list: it is the module that enables the SMB integration in the product. `smb_legacy` only selects which service implements it. `customer.env` replaces the value from `.env`, so the line must list every module you want enabled.

> When `sudo mdss -c start` finds that the MDSS machine cannot run the SMB service (missing cifs module, rootless container runtime, privileges refused), it stops and prints this exact line to set. If a check reports a problem that does not apply to your machine, for example a custom AppArmor profile that you know permits `mount`, set `SKIP_SMB_CHECKS=yes` in `/etc/mdss/customer.env`.

## Troubleshooting

The message shown in MDSS when an account or unit is added identifies the cause. The SMB service log, in `services_logs/mdintegrations_smbservice` under the installation directory, carries the details: the server address, the share, the SMB version and the error code returned by the kernel.

When an account is added, every failure to reach the server (a name that cannot be resolved, an address with no server behind it, or a port with nothing listening on it) is currently reported as *Failed to connect to the server. The name could not be resolved.* The connection and timeout messages in the table below appear when a unit is added.

| Message shown in MDSS | Cause and what to do |
| ---- | ---- |
| The CIFS kernel module is not installed or not enabled on the machine running MetaDefender Storage Security. | The `cifs` module is not available on the MDSS machine. Follow Step 1. |
| Authentication failed. Please verify your credentials. | The server rejected the username or password, or the account has no access to the share. Check the credentials and the account's permissions on the share. Domain accounts may need the domain prefix. |
| The object was not found on the server. Please verify your path and permissions. | The share, or a folder in the share path, does not exist on the server. Make sure the share path starts with the share name and that every folder in it exists. |
| Failed to connect to the server. The name could not be resolved. Please verify that the path or hostname is correct and reachable. | The server name cannot be resolved, or nothing is listening on the configured port. Verify the server address and the port. |
| Connection to the unit share could not be established. | The kernel reported the server or its network as unreachable, or MDSS could not reach the SMB service container. Check the route and the firewalls between the MDSS machine and the server on the SMB port, and check that the `mdintegrations_smbservice` container is running. |
| IO timeout. Please verify your configuration and try again. | The kernel reported a timeout while connecting to the server. Check the route and the firewalls between the MDSS machine and the server on the SMB port. |
| Communication with the unit share failed. Please check that the username and password are correct. | The server did not answer (it is down, or a firewall drops the traffic), the mount did not complete within `SMBSERVICE_MOUNT_TIMEOUT_SECONDS`, the server rejected the mount options or the SMB version negotiation failed, the account can mount the share but cannot list the folder, or the SMB service container is running without the privileges described in Step 2. Check that the server is up, reachable on the SMB port and supports SMB 2.1 or later, and that the account can list the folder. Run `sudo mdss -c restart` and read its output, which reports missing container privileges, and check the kernel log below. |

For any mount failure, the kernel log on the MDSS machine shows the CIFS client's own diagnostics:

```bash
sudo dmesg | grep 'CIFS: VFS'
```

A mount that fails does not leave a session open on the server, so a corrected configuration can be retried immediately.

## Notes

- The SMB service negotiates SMB 3.1.1 first, then SMB 3.0, then SMB 2.1, and stops at the first version the server accepts. SMB 1 is never used.
- A share is mounted on first use and unmounted after 5 minutes without activity. A scan that starts later mounts it again.

## Units added as NFS storage in earlier releases

Before 4.6.0, the setup recommended for production was to mount the share on the MDSS machine with `cifs-utils` and add it in MDSS as an NFS storage unit pointing at the mount directory. Units configured that way keep working after the upgrade. To move a unit to the SMB service, add the share as an SMB Compatible storage as described above, then remove the NFS unit and the mount from the MDSS machine.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
