<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/can-i-upgrade-metadefender-core-from-an-very-old-version-such-as -->

# Can I upgrade MetaDefender Core from an very old version such as version 4.x.x to the latest version 5.x.x?

**TLDR:** Yes, we can basically run the latest installer to upgrade the MetaDefender Core from any older version to the latest. **However**, if the gap between the 2 versions is too far, it’s not recommended, and you should perform a clean/fresh installation.

**Recommended Path:**

If your Core release is more than *[time period]* old, In the vast majority of cases it will be a cleaner, easier, more reliable path to simply install the latest version of Core, including a clean database install.

The downside to this is that you will lose historical processing data. And you will need to rebuild your settings and workflows from scratch.

Specific recommendations documented below.

**If you absolutely MUST keep your historical data**

If you have absolutely no leeway about keeping your historical data, you can follow our incremental upgrade path below.

Caveats:

- The incremental upgrade process is very time intensive, and prone to unforeseen interactions between different Core versions, e.g. database structure mismatches, incompatible settings export files, etc.
- The process is not a science, but an art, that comes down to reading Release Notes at each stage to determine which Core version is the next safe landing point.
- Especially if the existing Core instance is very old, there is no guarantee that this path will be free of database errors. Meaning, you might end up with a corrupted database after several hours of effort, and need to drop back to a clean install anyway.

With all the above in mind, again this approach may turn out to require far more effort and time than the clean install approach, and with no guarantee of a clean result in the end.

**Incremental upgrade path:**

- Have a backup version (snapshot, recovery point,…)
- Divide the version gap into multiple stages to minimize the gap.
- Choosing the most stable versions to upgrade to. (Please review the Release note).
- Confirm that you have the proper [Recommended System Configuration](/docs/mdcore/v5.21.0/installation/recommended-system-configuration).

You can **attempt** to upgrade to MD Core version 5.6.1. However, the 5.X.X versions of Core come with a new Database. Since the current version is very old it may not be a smooth transition. After upgrading to 5.6.1 you can do incremental upgrades until you reach the latest version 5.13.2

**About the Installer:**

The latest installer is designed to work with both the old and new versions of the software. If you're currently using an older version, such as 4.16.3, it can detect the old database format (e.g., SQLite) and automatically convert it to the new format (e.g., PostgreSQL). It will also upgrade the database step-by-step through each version update. For example, if your current database is version v53 (from version 5.13.1) and you’re upgrading from v1 (from version 4.19.0), the installer will migrate the database to each version from 1-53. This process can take a long time and might lead to issues during migration.

That is why it’s not recommended to do the direct upgrade if the version gap is too far.

***Please note the following:**

- We do not have a formal recommended incremental upgrade path. So if you do decide to do incremental upgrade there is a good chance that you will run into a database error. In this situation you will most likely have to perform a clean/fresh installation.
- It is suggested that you take a Snapshot of your server before performing these upgrades.
- If you are on an older version of MD Core, such as v4.16.3 and upgrading to the latest version, you can attempt to export/import the configuration. However, you may not be able to successfully import the configuration. This is due to all the fixes and feature updates that have been made on latest version of MD Core.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
