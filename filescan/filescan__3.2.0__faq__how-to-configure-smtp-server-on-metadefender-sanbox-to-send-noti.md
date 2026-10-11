<!-- source: https://www.opswat.com/docs/filescan/3.2.0/faq/how-to-configure-smtp-server-on-metadefender-sanbox-to-send-noti -->

# How to configure SMTP server on MetaDefender Sanbox to send notification to Gmail mailbox?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

To be able to send notification to your Gmail mailbox from MetaDefender Sandbox the following fields should be configured properly under MetaDefender Sandbox:

- SMTP_PORT: smtp.gmail.com
- SMTP_PORT: 587
- SMTP_USER: username of the Gmail mailbox used for SMTP integration
- SMTP_PASS: App password created for Gmail mailbox provided under “Email” field.
- SMTP_SECURITY: starttls

In order to achieve that, the following configuration should be done on Gmail mailbox account:

1. Create App password for Gmail account

- Login to <https://myaccount.google.com/security>
- Under "Signing in to Google":

- Click on Two-Step Verification
- Scroll down to section “App passwords” and click arrow in front of “App passwords”

- In new page opened, write a name for your App password and click “Creates”
- Save the App password generated and click “Finished”. Further we will use the App password generated as password for mailbox used for MetaDefender Sandbox configuration as mentioned above and as in below example.

Example:

IMPORTANT: For field “Password” use App password created under Gmail account and not use the password which you use to login on Gmail mailbox.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
