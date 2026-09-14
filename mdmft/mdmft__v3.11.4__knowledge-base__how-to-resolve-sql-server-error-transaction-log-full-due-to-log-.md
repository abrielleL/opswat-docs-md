<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-to-resolve-sql-server-error-transaction-log-full-due-to-log- -->

# How to resolve SQL Server Error Transaction Log Full due to LOG_BACKUP?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article is applied to MetaDefender MFT releases deployed in a Windows environment using a full SQL database.

**Description**

There are situations when the SQL log is full which can lead to high disk usage, insufficient disk space on the drive or for the log in the archive which ultimately lead to MFT not functioning properly.

**Prerequisites**

For this activity, you will require the SQL Server Management Studio installed on the MFT server or the SQL database server.

**Configuration**

First step is to stop the MFT services

To do so please go to the services.msc, locate the OPSWAT MetaDefender Managed File Transfer Helper and stop it. This will trigger the stop of the other MFT services as shown below.

Please confirm that all the MFT services are stopped.

The next step is to Open the SSMS application and connect to the SQL database

1. First task is to backup the database log. - In Object Explorer, expand Databases.

   - Right click the sft_data -> tasks -> Backup -> Set Backup type to 'Transaction Log' and select a destination (e.g., .trn file).
   - Click OK to perform the log backup.
2. Change Recovery Model to SIMPLE - In Object Explorer, expand Databases.

   - Right-click sft_data → Properties
   - Go to the Options page.
   - Change Recovery Model from 'FULL' to 'SIMPLE' and click OK.
3. Shrink the Transaction Log File in SSMS - Right-click the 'sft_data' database > Tasks > Shrink > Files.

   - Set File type to 'Log', confirm the file name (e.g., sft_data_log).
   - Choose 'Release unused space' and click OK.
4. The MFT services can be started. - Please go to the services.msc, locate the OPSWAT MetaDefender Managed File Transfer services.

   - Start them in the following order:

     - OPSWAT MetaDefender Managed File Transfer Helper
     - OPSWAT MetaDefender Managed File Transfer Next
     - OPSWAT MetaDefender Managed File Transfer Processor
     - OPSWAT MetaDefender Managed File Transfer Rest
   - Once all the services are started, the MFT application is ready to be used.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
