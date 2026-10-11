<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-to-enable-tls-between-metadefender-vault-and-sql-server -->

# How to enable TLS between Metadefender Managed File Transfer and SQL Server for enhanced security?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

To enable TLS between MetaDefender Managed File Transfer and SQL Server, follow these steps:

1. Configure SQL Server to Support TLS:

- **Enable TLS Protocol:** Enable the "Force Encryption" option in SQL Server Configuration Manager.
- **Certificate Installation:** Install a valid SSL/TLS certificate on the SQL Server. Obtain a certificate from a trusted Certificate Authority (CA) or generate one internally using tools like OpenSSL.
- **Binding Certificate:** Bind the certificate to the SQL Server instance in SQL Server Configuration Manager. Specify the certificate in the "Certificate" tab under the "Protocols for SQL Server" properties.

2. Enable encrytion on the Metadefender Managed File Transfer side:

- Run *SftDatabaseConfigurationTool.exe* with the *--encrypt* parameter in the "<Metadefender Managed File Transfer installation folder>/tools" directory.
- Use *--encrypt false* to disable the encryption.

Warning

The "Encryption" option does not support self-signed certificates, and Microsoft SQL Server Express LocalDB is not supported.
