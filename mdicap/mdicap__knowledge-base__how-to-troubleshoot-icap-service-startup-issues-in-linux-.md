<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-to-troubleshoot-icap-service-startup-issues-in-linux- -->

# How to troubleshoot ICAP Service Startup Issues in Linux?

## [**Issue:**](/docs/mdicap/knowledge-base/how-to-troubleshoot-icap-service-startup-issues-in-linux-#issue)

**Symptoms:**

- ICAP service fails to start or crashes immediately after starting.
- Error messages related to PostgreSQL or configuration files appear in system logs.
- Logs indicate permission errors or misconfigured parameters.
- The service remains in a stopped state after an attempted restart.

---

**Common Causes and Solutions:**

**1. Incorrect Permissions on PostgreSQL Configuration Files**

**Cause:** If the `postgresql.conf`or related files are modified using the root account, the ICAP server may not have the required permissions to read them.

**Solution:**

1. Check the ownership and permissions of the PostgreSQL configuration files:

BashCopyls -l /var/lib/mdicapsrv/pg_data/postgresql/conf

2. Ensure that the owner is the `mdicapsrv` user:

BashCopychown mdicapsrv:mdicapsrv /var/lib/mdicapsrv/pg_data/postgresql.conf
sudo chmod 644 /var/lib/mdicapsrv/pg_data/postgresql.conf

3. Restart the ICAP service:

BashCopysystemctl restart mdicapsrv-pg.service
### [2. Customizing PostgreSQL Configuration](/docs/mdicap/knowledge-base/how-to-troubleshoot-icap-service-startup-issues-in-linux-#2-customizing-postgresql-configuration)

**Cause:** If users need to customize the PostgreSQL configuration without modifying the default `postgresql.conf` file.

**Solution:**

1. Instead of modifying `/var/lib/mdicapsrv/pg_data/postgresql.conf`, create a new configuration file:

BashCopysudo touch /usr/lib/mdicapsrv/postgres/postgresql.conf

2. Add the required configuration settings to this file.
3. Ensure the correct ownership and permissions:

BashCopychown mdicapsrv:mdicapsrv /usr/lib/mdicapsrv/postres/postresql.conf
chmod 644 /usr/lib/mdicapsrv/postgres/postgresql.conf

4. Restart the ICAP service:

BashCopysystemctl restart mdicapsrv-pg.service
### [3. Invalid Parameter in ICAP Server Configuration File](/docs/mdicap/knowledge-base/how-to-troubleshoot-icap-service-startup-issues-in-linux-#3-invalid-parameter-in-icap-server-configuration-file)

**Cause:** If the customer adds an incorrect or unsupported parameter in the ICAP server configuration file (`/etc/mdicapsrv/mdicapsrv.conf`), the service may fail to start.

**Solution:**

1. Check the ICAP server logs for error messages related to invalid configuration parameters:

BashCopycat /var/log/mdicapsrv/mdicapsrv.log | grep error

2. Review the ICAP server configuration file and ensure all parameters are correctly set.

### [4. PostgreSQL Database Not Running or Corrupted](/docs/mdicap/knowledge-base/how-to-troubleshoot-icap-service-startup-issues-in-linux-#4-postgresql-database-not-running-or-corrupted)

**Cause:** The ICAP service may fail to start if the required PostgreSQL database is not running or is corrupted.

**Solution:**

1. Check the status of the PostgreSQL service:

BashCopysystemctl status mdicapsrv-pg.service

2. If PostgreSQL is not running, start it:

BashCopysystemctl start mdicapsrv-pg.service

3. If the database is corrupted, consider restoring from a backup:

BashCopypg_restore -U postgres -d icapdb /backup/icapdb.dump
### [5. ICAP Service Fails Due to Port Conflicts](/docs/mdicap/knowledge-base/how-to-troubleshoot-icap-service-startup-issues-in-linux-#5-icap-service-fails-due-to-port-conflicts)

**Cause:** If another application is using the same port as the ICAP service, the service will fail to bind to its configured port.

**Solution:**

1. Check for port conflicts:

BashCopynetstat -tulnp | grep <ICAP_PORT>

2. If another process is using the port, either stop the conflicting service or change the ICAP port in `icapserver.conf`.
3. Restate the ICAP service:

BashCopysystemctl restart mdicapsrv-pg.service

---

**Additional Troubleshooting Steps:**

- Check system logs for additional clues:

BashCopyjournalctl -xe | grep mdicapsrv-pg.service

- Ensure all dependencies are installed and up to date.
- Verify disk space availability using `df -h`.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
