<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-to-configure-smtp-server-with-authentication-under-metadefen -->

# How to configure SMTP server with authentication under MetaDefender ICAP Server to send notification to M365?

#### [**Solution**](/docs/mdicap/v5.14.1/knowledge-base/how-to-configure-smtp-server-with-authentication-under-metadefen#solution)

To be able to send notification to your M365 tenant from MetaDefender ICAP Server, the following fields should be configured properly under MetaDefender ICAP Server:

- Server: smtp.office365.com
- Port: 587
- Connection type: TLS
- Auth Method: Auth Login
- Email: Email address for sender of notification, it should be a real mailbox which is licensed on M365 side.
- Username: username of the mailbox provided under “email” field.
- Password: password of the mailbox provided under “Email” field.

More details about M365 URLs can be found checking following link: [Microsoft 365 URLs and IP address ranges - Microsoft 365 Enterprise | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges?view=o365-worldwide#exchange-online)

Example:

**IMPORTANT**: To complete the configuration, the following settings should be reviewed on the M365 mailbox account:

- Ensure that SMTP AUTH is enabled in your organization
- Verify that “Authenticated SMTP” is enabled per mailbox in scope

Please check the following article to see how this can be done: [Enable or disable SMTP AUTH in Exchange Online | Microsoft Learn](https://learn.microsoft.com/en-us/exchange/clients-and-mobile-in-exchange-online/authenticated-client-smtp-submission#disable-smtp-auth-in-your-organization)
