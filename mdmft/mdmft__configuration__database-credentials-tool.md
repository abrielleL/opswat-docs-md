<!-- source: https://www.opswat.com/docs/mdmft/configuration/database-credentials-tool -->

# Database Configuration Tool

Summarize Page    Connect to Cursor Connect to VS Code

MetaDefender Managed File Transfer systems integrated with a remote *Microsoft SQL Server* store the database connection in their service configuration. The **Database Configuration Tool** (`SftDatabaseConfigurationTool.exe`) lets an administrator change that connection after install — without re-running the installer.

Use it to:

- Update the SQL Server login credentials (username and password).
- Move the databases to a different *SQL Server* host or *Availability Group* listener, or change the port.
- Switch between *SQL Server authentication* and *Windows (Integrated) authentication*.
- Enable or disable connection encryption between the MFT services and *SQL Server*.

The tool applies the change consistently across all MFT services and the database, validates the new connection before committing, and automatically rolls everything back if anything goes wrong.

Important

The Database Configuration Tool is available for Managed File Transfer installations that use the recommended *Microsoft SQL Server* integration — with either *SQL Server authentication* or *Windows authentication*.

It is **not** available for installations that use *Microsoft SQL Server Express LocalDB*.

## [How it works](/docs/mdmft/configuration/database-credentials-tool#how-it-works)

When you run the tool it performs the change as a single, safe operation:

1. Reads and decrypts the current connection from the service configuration.
2. **Validates** the new connection — confirms the server is reachable, the `sft_conn` and `sft_data` databases exist, and the login has the required permissions. (With `--dry-run` the tool stops here and changes nothing.)
3. Backs up the configuration files, then stops the MFT services.
4. Writes the new connection to the three service config files and to the database, and — for *Windows authentication* — updates the service *Log On As* accounts.
5. Restarts the MFT services.

If any step after the services are stopped fails, the tool **automatically rolls back** to the previous configuration and restarts the services, so a failed change does not leave MFT unable to start. The previous configuration files are also kept in a backup folder (see [Logs and backups](/docs/mdmft/configuration/database-credentials-tool#logs-and-backups)).

## [Before you begin](/docs/mdmft/configuration/database-credentials-tool#before-you-begin)

Warning

Before using the Database Configuration Tool, create a snapshot of your MFT virtual machine and a full backup of all MFT-related databases.

- **Run on the MFT server** in an **elevated** *Command Prompt* or *PowerShell* (Run as administrator).
- **Prepare the target SQL Server login.** The tool does **not** create databases, logins, or grant permissions — those must already exist. The login (for *Windows authentication*, the chosen Windows account) must have, on both the `sft_conn` and `sft_data` databases:
- the `db_owner` role (simplest), **or**
- at minimum `db_datareader` + `db_datawriter` **and** `EXECUTE` permission.
- **For** ***Windows authentication***, the chosen domain or machine account must also have the ***Log on as a service*** right on the MFT host (`secpol.msc` → *Local Policies* → *User Rights Assignment* → *Log on as a service*). The tool checks this up front and refuses to make any change if the right is missing.

Tip

There is no need to provide a different or intermediate login when only changing the password of the current account.

The tool validates the new connection before it commits anything and rolls back automatically on failure, so updating the same login with a new password is safe.

## [Running the tool](/docs/mdmft/configuration/database-credentials-tool#running-the-tool)

1. Open an **elevated** *Command Prompt* (cmd) or *PowerShell*.
2. Navigate to the `Tools` folder in the installation directory, for example:

   - `C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Tools`
3. Run `SftDatabaseConfigurationTool.exe` with the options you want to change:

SftDatabaseConfigurationTool.exe [--server <host>] [--port <number>]
[--username <user> --password <pwd>]
[--windows-auth] [--encrypt true|false]
[--trust-server-certificate true|false]
[--dry-run] [--service-start-timeout <seconds>]
### [Command-line options](/docs/mdmft/configuration/database-credentials-tool#command-line-options)

| Option | Description |
| --- | --- |
| `--server <host>` | *SQL Server* name or *Availability Group* listener address. |
| `--port <number>` | TCP port (0–65535). |
| `--username <user>` | *SQL Server* login (SQL auth), **or** — with `--windows-auth` — the Windows account to run the services as, in `DOMAIN\user` (or `MACHINE\user`) form. |
| `--password <pwd>` | Password for the login above. Always required together with `--username`. |
| `--windows-auth` | Switch the connection to *Windows (Integrated) authentication*. Requires `--password`. |
| `--encrypt true/false` | Enable or disable TLS encryption between the MFT services and *SQL Server*. |
| `--trust-server-certificate true/false` | Accept a self-signed/untrusted server certificate **for validation only** (see [Encryption and certificates](/docs/mdmft/configuration/database-credentials-tool#encryption-and-certificates)). |
| `--dry-run` | Validate the new settings and report what would change, without making any changes. |
| `--service-start-timeout <seconds>` | How long to wait for each service to start (default: 300). |

Info

Option rules:

1. Provide **at least one** option.
2. The tool applies **partial updates** — only the options you supply are changed; everything else is preserved from the current configuration. Options can be combined freely (for example, change the server and the port in one run).
3. `--username` and `--password` must always be provided together.
4. `--windows-auth` requires `--password`. `--username` is optional with `--windows-auth`; if omitted, the tool uses the account the `mftREST` service currently runs as.
5. Quote passwords that contain shell-special characters such as $, &, ^, %, !, or a backtick. In *PowerShell* prefer single quotes: `--password 'p@ss$word'`; in cmd.exe use double quotes.
## [Common tasks](/docs/mdmft/configuration/database-credentials-tool#common-tasks)

### [Change the SQL login credentials](/docs/mdmft/configuration/database-credentials-tool#change-the-sql-login-credentials)

SftDatabaseConfigurationTool.exe --username mftapp --password "S3cret!"
### [Move to a different SQL Server or port](/docs/mdmft/configuration/database-credentials-tool#move-to-a-different-sql-server-or-port)

SftDatabaseConfigurationTool.exe --server NEWSQL01 --port 1433

Only the server and port change; the existing credentials and other settings are preserved.

### [Switch to Windows authentication](/docs/mdmft/configuration/database-credentials-tool#switch-to-windows-authentication)

SftDatabaseConfigurationTool.exe --windows-auth --username DOMAIN\mftsvc --password "S3cret!"

The tool validates the connection as that account and then sets it as the *Log On As* account for the `mftNext`, `mftREST`, `mftProcessor`, `mftCache`, and `mftHelper` services. (`mftNodeManager` is intentionally left as `LocalSystem`.)

### [Change server or port while staying on Windows authentication](/docs/mdmft/configuration/database-credentials-tool#change-server-or-port-while-staying-on-windows-authentication)

SftDatabaseConfigurationTool.exe --server NEWSQL01 --port 1433

The tool detects that the current configuration uses *Windows authentication* and preserves it. Because validation must run as the service account, the tool prompts for that account's password if `--password` is not supplied (input is masked; press **Ctrl+C** to abort without making changes). Provide `--password` on the command line to skip the prompt.

### [Switch back to SQL authentication](/docs/mdmft/configuration/database-credentials-tool#switch-back-to-sql-authentication)

SftDatabaseConfigurationTool.exe --username sa --password "..."

The tool reverts the service *Log On As* accounts back to `LocalSystem` automatically.

### [Enable or disable encryption](/docs/mdmft/configuration/database-credentials-tool#enable-or-disable-encryption)

SftDatabaseConfigurationTool.exe --encrypt true
SftDatabaseConfigurationTool.exe --encrypt false
### [Validate without changing anything (dry run)](/docs/mdmft/configuration/database-credentials-tool#validate-without-changing-anything-dry-run)

SftDatabaseConfigurationTool.exe --server NEWSQL01 --port 1433 --dry-run
## [Encryption and certificates](/docs/mdmft/configuration/database-credentials-tool#encryption-and-certificates)

To use encryption (or simply to validate a connection) against a *SQL Server* that presents a **self-signed or otherwise untrusted** TLS certificate, the certificate must be **trusted by the MFT host**:

1. Install the *SQL Server* certificate into the **Local Computer → Trusted Root Certification Authorities** store on the MFT host, then run the tool normally. This is the recommended approach.
2. Alternatively, pass `--trust-server-certificate true` to accept the certificate **for the tool's own validation connection only**. This value is **not** written to the saved connection string — the MFT services do not support it — so it is a per-run option, not a permanent fix.

Self-signed certificates

The tool refuses to connect to a *SQL Server* whose certificate it cannot validate — even when encryption is disabled, because the login handshake still uses the certificate.

If your server uses a self-signed certificate, either install it into the host's *Trusted Root* store, or pass `--trust-server-certificate true` on each run until a trusted certificate is in place.

## [Troubleshooting](/docs/mdmft/configuration/database-credentials-tool#troubleshooting)

| Message | Cause | Fix |
| --- | --- | --- |
| `Login failed for user '...'` | Wrong username/password, the login lacks database access, or the shell mangled a password with special characters. | Verify the credentials and database permissions. Quote the password so the shell passes it through unchanged (PowerShell: single quotes; cmd.exe: double quotes). |
| `Login lacks required permissions on database 'sft_conn' / 'sft_data'` | The login is not in `db_owner` and is missing `db_datareader`, `db_datawriter`, or `EXECUTE`. | Add the login to `db_owner` on both databases, or grant `db_datareader` + `db_datawriter` + `EXECUTE`. |
| The server presented a TLS certificate that this machine does not trust | Self-signed/untrusted *SQL Server* certificate. | Install the certificate into the host's *Trusted Root* store, or pass `--trust-server-certificate true`. |
| `1069: The service did not start due to a logon failure` | The *Windows authentication* account lacks the *Log on as a service* right, or the password is wrong. | Grant the right (`secpol.msc`) and verify the password. |
| A service did not start within the timeout | The first start after a connection change can be slow (TLS handshake + database warm-up). | Re-run with a longer timeout, e.g. `--service-start-timeout 600`. |

If a change fails, the tool rolls back to the previous configuration and reports whether the rollback was clean. When the rollback succeeds, MFT continues running on its previous configuration and no further action is needed.

## [Logs and backups](/docs/mdmft/configuration/database-credentials-tool#logs-and-backups)

- **Tool log:** `DatabaseConfigurationTool.log`, located in the installation folder under `Services\Logs` (typically `C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Services\Logs`). It is collected automatically by the support-package generator.
- **Configuration backups:** the previous service configuration files are saved to `C:\ProgramData\OPSWAT\MetaDefender Managed File Transfer\backup\DatabaseConfigurationTool\` before each change.
