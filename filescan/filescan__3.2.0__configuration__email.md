<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/email -->

# SMTP / Email

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This tab allows Admins to configure their STMP server which sends automatic emails to their users.

These configuration parameters are used in applications or scripts where sending emails programmatically is required, such as in web applications, automated notification systems, or email clients. By setting these parameters correctly, the application can connect to an SMTP server, authenticate, and send emails on behalf of a specified sender

### [Email tab](/docs/filescan/3.2.0/configuration/email#email-tab)

***Admin Panel > Settings > Configuration > Email***

The instances that are **sent automatically to user** via STMP emails can be due to:

- Sign-up confirmation email
- Resetting password

The [following tab](https://www.filescan.io/admin/settings/config) details the STMP server setup:

### [Configuration options](/docs/filescan/3.2.0/configuration/email#configuration-options)

| Field | Description |
| --- | --- |
| `EMAIL_SENDER_ADDRESS` | Email address that the automatic emails are being sent from to the users |
| `USE_SMTP` | Whether the organization or the admin is using SMTP server or not. Simple Mail Transfer Protocol (SMTP) should be used for sending emails. SMTP is the standard protocol for sending emails across the Internet and it is preferred by OPSWAT as well. ***Library used for sending emails if SMTP server is not configured:*** ***sendmail*** |
| `SMTP_HOST` | This specifies the hostname or IP address of the SMTP (outgoing mail) server that will be used to send the emails. |
| `SMTP_PORT` | This specifies the port number on the SMTP server to connect to for sending emails. Common ports used for SMTP are 25, 587, or 465 |
| `SMTP_USER` | This is the username or account name used to authenticate with the SMTP server if authentication is required. This could be an email address or a specific username provided by the SMTP server. |
| `SMTP_PASS` | This is the password associated with the SMTP_USER account. It is used for authentication when connecting to the SMTP server to send emails securely. |
| `SMTP_SECURITY` | This setting determines the type of security to use when connecting to the SMTP server. Possible values might include:   - `none`: No encryption or security. - `ssl`: Use SSL/TLS encryption on a dedicated SSL port (e.g., port 465). - `tls`: Use STARTTLS command to switch the connection to a TLS-encrypted one (usually on port 587). |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
