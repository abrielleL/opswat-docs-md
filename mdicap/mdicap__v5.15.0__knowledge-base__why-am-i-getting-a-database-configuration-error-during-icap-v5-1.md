<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/why-am-i-getting-a-database-configuration-error-during-icap-v5-1 -->

# Why am I getting a database configuration error during ICAP v5.11.0 installation?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to MetaDefender ICAP Server version 5.11.0 deployed on Windows Server with an unsupported locale.

**Issue:**

During the installation of ICAP v5.11.0, you may encounter the following error message:

**Database configuration**

**There's a problem when connecting to the database. Please contact your administrator.**

In the `mdicapsrv.log`, you will see an error similar to:

`[ERROR ] 2025.10.16 15:24:56.669: (icap.postgres) Postgres issue, error='Can not create database cluster, std-err: 'initdb: error: invalid locale name "en_US"`

**Resolution:**

This issue is already resolved in ICAP v5.12.0.

If you installed v5.11.0 on a system with unsupported locale settings, please upgrade to v5.12.0 following the [Upgrade documentation](https://www.opswat.com/docs/mdicap/installation/upgrade-to-version-5-7-0).

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
