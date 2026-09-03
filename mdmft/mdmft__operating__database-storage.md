<!-- source: https://www.opswat.com/docs/mdmft/operating/database-storage -->

# Database Storage Monitoring

Summarize Page    Connect to Cursor Connect to VS Code

The Database Storage Monitoring widget provides a visual representation of how much storage space the application's database is using. This allows administrators to monitor database growth and ensure sufficient storage is available for operations.

## [Displayed Information](/docs/mdmft/operating/database-storage#displayed-information)

The chart presents three key metrics:

- Maximum Size: The hard drive's storage capacity, the database is installed on.
- Allocated Size: The total space currently allocated for the database file. This space may be larger than the actual data usage.
- Used Space: The actual amount of space occupied by data within the allocated size.

The data is fetched upon loading the page and can be reloaded on demand, and it is displayed in a graphical format, making it easy to understand trends and identify potential storage concerns.

Info

If the allocated space approaches the maximum size or the used space nears the allocated limit, administrators should consider optimizing storage or increasing capacity.

## [Required database permission](/docs/mdmft/operating/database-storage#required-database-permission)

To retrieve database storage metrics, the database login must have the **VIEW SERVER STATE** permission.

For SQL Azure Managed Instance, the required permission is **VIEW SERVER PERFORMANCE STATE.**

These permissions ensure that the necessary system views and dynamic management objects can be accessed to gather storage usage details.

Info

For information about how to migrate from SQL Server Express LocalDB, refer to our [documentation](/docs/mdmft/knowledge-base/sql-server-express-localdb-migration).

Info

For information about how to migrate from SQL Server Express LocalDB, refer to our [documentation](/docs/mdmft/knowledge-base/sql-server-express-localdb-migration).
