<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-to-configure-smtp-server-on-metadefender-icap-server-to-send -->

# How to configure SMTP server on MetaDefender ICAP Server to send notification to Gmail mailbox?

#### [Solution](/docs/mdicap/v5.14.1/knowledge-base/how-to-configure-smtp-server-on-metadefender-icap-server-to-send#solution)

To be able to send notification to your Gmail mailbox from MetaDefender ICAP Server, the following fields should be configured properly under MetaDefender ICAP Server:

- Server: smtp.gmail.com
- Port: 587
- Connection type: TLS
- Auth Method: Auth Login
- Email: Email address for sender of notification, it should be a real Gmail mailbox.
- Username: username of the mailbox provided under “email” field.
- Password: App password created for Gmail mailbox provided under “Email” field.

To create an App password, the following configuration should be done on Gmail mailbox account:

1. **Create App password for Gmail account**

- Login to <https://myaccount.google.com/security>
- Under "**Signing in to Google**":
- Enable **2-Step Verification**
- Scroll down to section “**App passwords**” and click arrow in front of “App passwords”

In new page opened, write a name for your App password and click “**Creates**”

- Save the App password generated and click “Finished”. Further, we will use the App password generated as password for mailbox used for MetaDefender ICAP Server configuration as mentioned above and as in below example.

Example:

**IMPORTANT**: For field “Password” use App password created under Gmail account and not use the password which you use to login on Gmail mailbox.
