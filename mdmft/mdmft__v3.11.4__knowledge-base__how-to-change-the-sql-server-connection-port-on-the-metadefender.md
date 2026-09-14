<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-to-change-the-sql-server-connection-port-on-the-metadefender -->

# How to change the SQL Server connection port on the MetaDefender Managed File Transfer side?

Summarize Page    Connect to Cursor Connect to VS Code

1. Locate the *SftDatabaseConfigurationTool.exe* in the "<Metadefender Managed File Transfer installation folder>/tools" directory.
2. Run the *SftDatabaseConfigurationTool.exe* with the `--port=<portnumber>` parameter, ensuring that `<portnumber>` matches the current setting on the SQL Server side.
3. If all conditions are met, MetaDefender Managed File Transfer™ will connect to the SQL Server using the new connection port.
