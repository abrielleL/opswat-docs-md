<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/why-upgrade-to-metadefender-icap-5-7-0-or-5-8-0-fails- -->

# Why does upgrading MetaDefender ICAP fail with a database connection error?

This article applies to upgrade attempts to MetaDefender ICAP Server from v5.6.0 or older to v5.7.0 or later (including current releases) on Windows, where the PostgreSQL database password or the underlying OS locale contains non-ASCII characters

## [**Issue**](/docs/mdicap/knowledge-base/why-upgrade-to-metadefender-icap-5-7-0-or-5-8-0-fails-#issue)

MetaDefender ICAP may fail during the upgrade process with the following error:

This kind of error typically means that the password being used to establish the database connection is incorrect.

## [**Cause**](/docs/mdicap/knowledge-base/why-upgrade-to-metadefender-icap-5-7-0-or-5-8-0-fails-#cause)

If the password has not been changed, the error is most likely due to the password containing non-ASCII characters (for example, Japanese, Turkish, or other non-Latin characters).

A related but distinct cause is a Windows OS locale that contains non-ASCII characters (for example, a Turkish-language Windows install). PostgreSQL 16 cannot initialize a database cluster under either condition, which blocks the PostgreSQL 12 → 16 migration that runs during upgrade.

Note:

A fix was introduced in v5.9.0 to handle non-ASCII passwords automatically during upgrade. However, this failure may recur in some cases, upgrading directly from v5.5.0/v5.6.0 on later releases, and the OS-locale variant is only resolved automatically for **fresh installs from v5.11.0 onward**.

In-place upgrades from older versions may still hit this issue on the current release and may require the manual remediation below or an OPSWAT Support-assisted session.

If your database password or OS locale contains non-ASCII characters, we recommend contacting Support before starting the upgrade.

## [**Remediation Steps**](/docs/mdicap/knowledge-base/why-upgrade-to-metadefender-icap-5-7-0-or-5-8-0-fails-#remediation-steps)

Depending on the status of your deployment, you can follow either of these two methods to remediate this issue:

### [**Method 1: MetaDefender ICAP is on a failed state after an upgrade failure**](/docs/mdicap/knowledge-base/why-upgrade-to-metadefender-icap-5-7-0-or-5-8-0-fails-#method-1-metadefender-icap-is-on-a-failed-state-after-an-upgrade-failure)

Info

This method assumes that MetaDefender ICAP has just failed the upgrade process with the error mentioned above. No other remediation actions taken.

Paths provided are a reference only. Please make sure to use the path where you have installed MetaDefender ICAP.

1. Uninstall ICAP version 5.7.0 or 5.8.0
2. Remove the following folders and files:

   - Folder `postgres` (`C:\<INSTALATION_PATH>\postgres`),
   - Folder `postgres-old`(`C:\<INSTALATION_PATH>\postgres-old`)
   - Folder `pg_data`(`C:\<INSTALATION_PATH>\data\pg_data`)
   - File `pg16.dat` (`C:\<INSTALATION_PATH>\pg16.dat`) if exists
   - File `ngx126.dat` (`C:\<INSTALATION_PATH>\ngx126.dat`) if exists
3. Rename folder `pg_data-old` (`C:\<INSTALATION_PATH>\data\pg_data-old`) -> `pg_data` (`C:\<INSTALATION_PATH>\data\pg_data`)
4. Install ICAP version 5.6.0(or the version of ICAP you had previously installed). Wait for ICAP to be ready ( when you can login to the Web Management Console)
5. Stop the ICAP Service. You can do this from the Windows Services window.
6. Open `cmd` with Admin privileges and cd to the ICAP installation folder (`cd C:\<INSTALATION_PATH>`)
7. Run `mdicapsrv-change-db-credentials.exe` and temporarily change the password to contain **ASCII characters ONLY**.

8. Start ICAP service again and test to make sure you can login to the Web Management Console
9. Upgrade to your target MetaDefender ICAP version

### [**Method 2: MetaDefender ICAP is in a working state and on version 5.6.0 or lower**](/docs/mdicap/knowledge-base/why-upgrade-to-metadefender-icap-5-7-0-or-5-8-0-fails-#method-2-metadefender-icap-is-in-a-working-state-and-on-version-560-or-lower)

Info:

This method assumes that you have a running MetaDefender ICAP version 5.6.0 or older and you know that the password set for the database contains non-ASCII characters.

Or, you have reverted back to an snapshot of the system.

Path provided are a reference only. Please make sure to use the path where you have installed MetaDefender ICAP.

1. Stop ICAP service. You can do this from the Windows Services window.
2. Make a backup of pg_data folder (`C:\<INSTALATION_PATH>\data\pg_data`).
3. Remove file `pg16.dat` (`C:\<INSTALATION_PATH>\pg16.dat`) if exists.
4. Remove file `ngx126.dat` (`C:\<INSTALATION_PATH>\ngx126.dat`) if exists.
5. Run `mdicapsrv-change-db-credentials.exe` and temporarily change the password to contain **ASCII characters ONLY**.

6. Start ICAP service and check the ICAP Server can connect to the database. Verify correct functioning.
7. Attempt the upgrade to your target version

Info:

If you wish to change your password again to the initial password you were using, before following Method 1 or Method 2 described above, please follow Method 2 steps.

After following any of the methods above, you can set a password with special characters.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
