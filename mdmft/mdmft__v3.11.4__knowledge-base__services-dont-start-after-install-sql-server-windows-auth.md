<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/services-dont-start-after-install-sql-server-windows-auth -->

# Why don't the services start after installing MetaDefender Managed File Transfer with SQL Server using Windows authentication?

Summarize Page    Connect to Cursor Connect to VS Code

The services may fail to start if the service user account used to connect to the database lacks the *Log on as a service* permission. To resolve this issue:

- Open the "Local Security Policy" management console (`secpol.msc`).
- Navigate to "Local Policies" → "User Rights Assignment."
- Double-click on "Log on as a service."
- Click "Add User or Group," enter the service user account name, and click "OK."
- Restart the MetaDefender Managed File Transfer services in the Services management console (`services.msc`).
