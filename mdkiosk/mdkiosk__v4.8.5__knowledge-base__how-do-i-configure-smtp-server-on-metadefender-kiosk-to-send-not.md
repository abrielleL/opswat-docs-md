<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-configure-smtp-server-on-metadefender-kiosk-to-send-not -->

# How do I configure SMTP server on MetaDefender Kiosk to send notification to M365 tenant?

**Solution**

To be able to send notification to your M365 tenant from MetaDefender Kiosk, the following fields should be configured properly:

- Email settings: **SMTP**
- Host: **smtp.office365.com**
- Port: **587**
- Authentication: **StartTLS**
- Username: Email address for sender of notification, it should be a real mailbox which is licensed on M365 side. Normally in M365 is called UPN and it’s the same one as Primary SMTP Address.
- Password: password of the mailbox provided under “Username” field

Section “**Test settings**” provide the option to test SMTP configuration, but there should be provided real email addresses in order to be able to receive the email by recipient set.

More details about M365 URLs can be found checking following link: [Microsoft 365 URLs and IP address ranges - Microsoft 365 Enterprise | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/enterprise/urls-and-ip-address-ranges?view=o365-worldwide#exchange-online)

Example:

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
