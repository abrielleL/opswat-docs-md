<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/how-to-move-central-management-database-to-another-drive- -->

# How to move Central Management database to another drive?

**Steps to Move OPSWAT Central Management Database to a New Drive:**

1. **Stop the** **OPSWAT Central Management** **Service:** Before making any changes, stop the OPSWAT Central Management service to ensure no operations are being performed on the database.
2. **Backup the Data Folder:** Create a backup of the `ProgramData\OPSWAT\Central\Data` folder to safeguard the existing data.
3. **Move the Data Folder:** Move the `Data` folder to the new location on the desired drive, e.g., `F:\OPSWAT\Data`.
4. **Edit the MongoDB Configuration File:** Open the file located at `ProgramData\OPSWAT\Central\mongod.conf` for editing.
5. **Update the Database Path:** In the configuration file, change the value of `dbPath` to the new location, e.g., `F:\OPSWAT\Data`.
6. **Restart the OCM Service:** Once the changes are made, restart the OPSWAT Central Management service.

Support:

If **Further Assistance** is required, please follow the instructions on [How To Create a Support Package](https://docs.opswat.com/mdcore/troubleshooting/how-to-create-support-package-), then proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
