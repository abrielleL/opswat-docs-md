<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/can-metadefender-core-use-azure-sql-managed-instance-instead-of- -->

# Can MetaDefender Core use Azure SQL Managed Instance instead of PostgreSQL?

**Check your version:**

This article applies to MetaDefender Core and is applicable to all MetaDefender Core V5 releases deployed on Windows and Linux systems.

MetaDefender Core **requires** PostgreSQL as its database. Other database engines, including Microsoft Azure SQL Managed Instance, are not supported.

If you are planning a deployment, you will need to provision a PostgreSQL database for MetaDefender Core to function correctly. **Support for alternative database platforms is not currently available and is not on the product roadmap.**

For best results, follow the official deployment documentation and ensure your PostgreSQL instance meets the recommended configuration and performance guidelines.

If you have questions, concerns or issues regarding **MetaDefender** **Core**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
