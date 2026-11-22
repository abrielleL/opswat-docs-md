<!-- source: https://www.opswat.com/docs/supply-chain/installation/mdssc-command-line -->

# `mdssc` command line

The `mdssc` command controls MetaDefender Software Supply Chain on Linux. Run it as root. It works from any directory.

```bash
sudo mdssc <command> [options]
```

To see all commands, run `sudo mdssc help`. To see the details of one command, run `sudo mdssc <command> --help` or `sudo mdssc help <command>`.

> **Tab completion**
>
> Press **Tab** after `mdssc` to complete command names and options.

## Commands

| Command | What it does |
| ---- | ---- |
| `start` | Start all services. |
| `stop` | Stop all services. |
| `restart` | Stop, then start all services. |
| `update` | Pull newer images and restart. |
| `status` | Show the state of each container, its restarts and memory kills, and disk use. |
| `version` | Show the running image of each service and mark a service that differs from the expected image. |
| `logs` | Export all service logs to an archive. |
| `https on` / `https off` | Turn HTTPS for the web console on or off. See [Configuring HTTPS](https://www.opswat.com/docs/supply-chain/configuration/configuring-https). |
| `support` | Print a support report. See [Troubleshooting](https://www.opswat.com/docs/supply-chain/troubleshooting/troubleshooting#collecting-diagnostics). |
| `support logs` | Archive the recent logs and settings, with secrets masked. |
| `support full` | Build the full support package. |
| `debug <service>` | Turn on debug logs for one service for a limited time. |
| `debug off` | Turn off debug logs now. |
| `backup` | Save the database, settings and certificates to one file. |
| `restore <file>` | Restore a backup made with `mdssc backup`, then restart. |
| `help [command]` | Show the list of commands, or the details of one command. |

## Options

| Command | Option | Description |
| ---- | ---- | ---- |
| `support logs` | `--since TIME` | Archive logs newer than TIME, for example `30m`, `6h` or `2d`. Default: `24h`. |
| `support logs` | `--service NAME` | Archive only the logs of services whose name contains NAME. |
| `debug <service>` | `--for TIME` | Keep debug logs on for TIME, for example `30s`, `30m`, `2h` or `1d`. Default: `1h`. |
| `backup` | `--to DIR` | Write the backup file to DIR. Default: the current directory. |
| `backup` | `--passphrase-file FILE` | Read the passphrase from FILE instead of asking for it. |
| `backup` | `--no-encrypt` | Write a plain tar file. See the warning in [Backup and restore](#backup-and-restore). |
| `restore` | `--passphrase-file FILE` | Read the passphrase from FILE instead of asking for it. |

## Examples

```bash
sudo mdssc status
sudo mdssc version
sudo mdssc support logs --since 6h --service api
sudo mdssc debug api --for 30m
sudo mdssc backup --to /var/backups
sudo mdssc restore /var/backups/mdssc-backup_4.3.0_20261110-120000.tar
```

## Backup and restore

`mdssc backup` saves the database, `.env`, `customer.env`, the configuration files, the HTTPS certificates and the CA certificates to one file. By default it encrypts the file with a passphrase that you type.

```bash
sudo mdssc backup --to /var/backups
```

Keep the passphrase. You cannot restore the file without it.

> **Warning: --no-encrypt**
>
> `--no-encrypt` writes a plain tar file. The file holds the tenant encryption key next to the encrypted connection secrets. Anyone who can read the file can recover every stored integration credential. Keep the file as safe as the host.

`mdssc restore` asks you to type `RESTORE` before it starts. It replaces the database and the settings with the ones in the backup, then restarts the product. It keeps the database passwords, the database URL and the memory settings of the current host.

```bash
sudo mdssc restore /var/backups/mdssc-backup_4.3.0_20261110-120000.tar
```

You can restore a backup from the same version or from an older version. You cannot restore a backup from a newer version: upgrade first, then restore.

## Older commands

The `-c` and `-u` options still work. The new commands do the same work:

| New command | Older command |
| ---- | ---- |
| `mdssc start` / `stop` / `restart` | `mdssc -c start` / `-c stop` / `-c restart` |
| `mdssc update` | `mdssc -u update` |
| `mdssc logs` | `mdssc -u export_logs` |
| `mdssc https on` / `https off` | `mdssc -u enable_https` / `-u disable_https` |
| `mdssc support full` | `mdssc -u support_package` |

`mdssc -c status` still runs the full readiness check. `mdssc -u recreate <service>` recreates only the services that you name, with the current settings, and does not pull images.

`mdssc -u vacuum` and `mdssc -u export_settings` are removed in v4.3.0.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
