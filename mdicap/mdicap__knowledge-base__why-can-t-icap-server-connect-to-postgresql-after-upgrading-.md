<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/why-can-t-icap-server-connect-to-postgresql-after-upgrading- -->

# Why can't ICAP Server connect to PostgreSQL after upgrading?

This article is applied to ICAP Server releases deployed on Windows and Linux systems.

**Issue:** ICAP Server cannot connect to PostgreSQL after upgrading ICAP Server.

**Possible Cause:** The PostgreSQL password contains special characters that are not handled correctly during the upgrade process.

**Resolution:** There are two possible solutions:

- **Option 1: Change the PostgreSQL Password Before Upgrade**

  - For:

    - Windows: Use the built-in tool `mdicapsrv-change-db-credentials.exe` located in the ICAP Server installation folder to change the PostgreSQL password to one that does not contain special characters.
    - Linux: Run `mdicapsrv-change-db-credentials` under `/usr/sbin` with root privilege to change the PostgreSQL password to one that does not contain special characters.
  - Then, proceed with the ICAP Server upgrade.
- **Option 2: Upgrade to a Newer Version**

  - Upgrade ICAP Server to version 5.9.0 or later, which addresses this issue.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
