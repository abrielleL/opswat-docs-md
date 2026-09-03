<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/sql-authentication-server-setup -->

# SQL Authentication Server Setup

To configure a new database authentication server contact OPSWAT Support at [opswat-support@opswat.com](mailto:opswat-support@opswat.com)

For Active Directory and LDAP Authentication Setup click [here](/docs/manac/nac-v8.1.1/configuration/active-directory-and-ldap-authentication-sources-setup).

To configure Chained Authentication Sources click [here](/docs/manac/nac-v8.1.1/configuration/chained-authentication-servers).

## [Database table requirements:](/docs/manac/nac-v8.1.1/configuration/sql-authentication-server-setup#database-table-requirements)

| **Field** | **Field Type** | **Field Description** |
| --- | --- | --- |
| **username** | varchar | Column that contains a username. Column name is configurable. |
| **password** | varchar | Column that contains the password. Column name is configurable. |
| **groups** | varchar | Column that contains group names. Group names must be comma separated. Column name is configurable. |
| **expires** | timestamp | Column that contains the guest account expiration date and time. Column name is configurable. |
| **state** | int | Column that determines whether the guest account is active. Value must be set to ‘1’ for authentication to succeed. All other values will cause authentication to fail. Column name is NOT configurable. |

## [Related articles](/docs/manac/nac-v8.1.1/configuration/sql-authentication-server-setup#related-articles)
