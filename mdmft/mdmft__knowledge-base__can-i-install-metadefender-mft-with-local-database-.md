<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/can-i-install-metadefender-mft-with-local-database- -->

# Can I install MetaDefender MFT with Local Database?

Summarize Page    Connect to Cursor Connect to VS Code
#### [Overview](/docs/mdmft/knowledge-base/can-i-install-metadefender-mft-with-local-database-#overview)

Can I install Metadefender MFT with Local Database?

Solution: This is possible for MFT versions prior to 3.9.2, but starting version 3.9.2 MFT no longer offers LocalDB as an installation option. For new installations, administrators must set up and connect to a compatible external database before proceeding.

Existing installations using LocalDB can still be upgraded without interruption.

#### [Warning](/docs/mdmft/knowledge-base/can-i-install-metadefender-mft-with-local-database-#warning)

Microsoft SQL Server 2019 Express LocalDb is primarily designed for testing and development purposes and is not recommended for production environments.

Using this database in a production setting can result in data loss and significant performance issues, especially under high load.

For reliable and secure operation, we recommend using a more robust database solution. We strongly advise against deploying this backend in live production systems.

#### [References](/docs/mdmft/knowledge-base/can-i-install-metadefender-mft-with-local-database-#references)

- [Database System Requirements](https://www.opswat.com/docs/mdmft/installation/system-requirements#database)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
