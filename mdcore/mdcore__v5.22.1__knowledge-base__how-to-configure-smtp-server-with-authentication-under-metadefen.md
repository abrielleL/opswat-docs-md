<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-configure-smtp-server-with-authentication-under-metadefen -->

# How to configure SMTP server with authentication under MetaDefender Core to send notification to M365?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### Solution

To be able to send notification to your M365 tenant from MetaDefender Core, the following fields should be configured properly under MetaDefender Core:

- Server: smtp.office365.com
- Port: 587
- Connection type: TLS
- Auth Method: Auth Login
- Email: Email address for sender of notification, it should be a real mailbox which is licensed on M365 side.
- Username: username of the mailbox provided under “email” field.
- Password: password of the mailbox provided under “Email” field.

More details about M365 URLs can be found checking following link: [Microsoft 365 URLs and IP address ranges - Microsoft 365 Enterprise | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges?view=o365-worldwide#exchange-online)

Example:

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
