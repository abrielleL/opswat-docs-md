<!-- source: https://www.opswat.com/docs/mdmft/troubleshooting/local-database -->

# Local Database

Summarize Page    Connect to Cursor Connect to VS Code Info

This page is relevant for MetaDefender Managed File Transfer™ versions prior to 3.9.2

### [Insufficient RAM for LocalDB Creation](/docs/mdmft/troubleshooting/local-database#insufficient-ram-for-localdb-creation)

An error such as "Failed to create a tenant" in the log file may indicate insufficient RAM for creating a LocalDB.

#### [Resolution](/docs/mdmft/troubleshooting/local-database#resolution)

To resolve this issue:

1. Examine the installed log file for entries indicating "Failed to create a tenant."
2. Identify and terminate non-essential processes consuming system memory.
3. Attempt to create the LocalDB instance again after freeing up sufficient memory.

---

### [Conflict in LocalDB Preventing Creation of a New Instance](/docs/mdmft/troubleshooting/local-database#conflict-in-localdb-preventing-creation-of-a-new-instance)

Conflicts in LocalDB that prevent the creation of a new instance can arise due to several factors, such as database corruption, ongoing processes, or other environmental issues. These conflicts can hinder the successful creation of a new LocalDB instance. Following the steps below will help resolve the conflict by stopping and deleting the conflicting LocalDB instance, allowing for the creation of a new one without disruptions.

#### [Resolution](/docs/mdmft/troubleshooting/local-database#resolution)

To resolve this issue:

1. Open the "PSTool" folder using an Administrator command prompt.
2. Run the following command to initiate SQL PSExec:

BatchCopyPSExec -i -s -d cmd

3. Display SQL LocalDB information using the command:

BashCopysqllocaldb i

4. Stop the conflicting LocalDB instance with:

BashCopysqllocaldb stop <instance-name>

5. Delete the conflicting LocalDB instance using:

BashCopysqllocaldb delete <instance-name>

After completing this step, try to install LocalDB again.
