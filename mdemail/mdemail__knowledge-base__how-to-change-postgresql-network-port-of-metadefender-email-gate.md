<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/how-to-change-postgresql-network-port-of-metadefender-email-gate -->

# How to change PostgreSQL network port of MetaDefender Email Gateway Security?

This article applies to all MetaDefender Email Gateway Security versions 6.0.0 and above

**Step 1:** Open Registry Editor and navigate to

HtmlCopyComputer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\

**Step 2:** Modify the **db_port** value under the following Registry Keys:

- Metadefender Email Database\database (available only in case of a [Standalone database deployment](https://www.opswat.com/docs/mdemail/installation/standalone-deployment))
- Metadefender Email Security\database

As well as the **port** value in the **postgresql.conf** file:

- <EGS_Installation_Directory>/data/pg_data/postgresql.conf

**Step 3:** Open **Services** Application and restart both the **OPSWAT MetaDefender Email Gateway Security** and the **OPSWAT MetaDefender Email Gateway Security Database Server** services:

**Step 4:** Check that the **postgres** uses the new port using the following PowerShell Command:

HtmlCopyGet-Process -Id (Get-NetTCPConnection -LocalPort <port>).OwningProcess

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
