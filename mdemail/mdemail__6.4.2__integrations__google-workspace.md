<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/integrations/google-workspace -->

# Google Workspace

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Hardening](/docs/mdemail/6.4.2/integrations/google-workspace#hardening)

Use TLS

Use TLS whenever it is supported by Google Workspace.

Email Gateway Security supports SMTP-over-TLS (SMTPS) or StartTLS for both inbound and outbound SMTP connections.

For details see the *SMTP servers* section in [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings) and [Configuration/Server profiles](/docs/mdemail/6.4.2/configuration/server-profiles).

Open relay

Under certain conditions - especially when integrated to Google Workspace as an outbound gateway - Email Gateway Security may be exploited as an open relay.

For details (risks and resolution) see [Configuration/Hardening](/docs/mdemail/6.4.2/configuration/hardening).

## [Inbound email gateway](/docs/mdemail/6.4.2/integrations/google-workspace#inbound-email-gateway)

### [Overview](/docs/mdemail/6.4.2/integrations/google-workspace#overview)

To configure Email Gateway Security with Google Workspace for inbound email, we will perform the following steps:

### [Google Workspace configuration](/docs/mdemail/6.4.2/integrations/google-workspace#google-workspace-configuration)

Unsecure configuration

The configuration described in this document focuses on a working connection only, and it may not result in a secure configuration.

Further reading

For detailed information about Google Workspace configuration see <https://support.google.com/a/answer/60730>.

Perform the following steps:

1. [Sign in](https://admin.google.com/) to your [Google Admin console](https://support.google.com/a/answer/182076).

Sign in using an *administrator account*.

2. From the Admin console Home page, go to **Apps > Google Workspace > Gmail > Advanced settings**.

**Tip:** To see *Advanced settings*, scroll to the bottom of the Gmail page.

3. In the **Organizations** section on the left, select the top-level organization (typically your primary domain).
4. Scroll to the **Inbound gateway** setting in the *Spam* section. Hover over the setting and click **Configure** to create a new setting or click **Edit** to edit an existing one.
5. Enter a description.
6. Under **Gateway IPs**, click **Add** and enter the IP address or range of addresses of Email Gateway Security server(s).

**Note:** Be sure to enter public IP addresses, as private IP addresses are not accepted.

7. Click **Save**.

### [Email Gateway Security configuration](/docs/mdemail/6.4.2/integrations/google-workspace#email-gateway-security-configuration)

Perform the following steps:

1. Install and configure MetaDefender Email Gateway Security. For details see [Installation/Prerequisites](/docs/mdemail/6.4.2/installation/prerequisites).
2. Configure SMTP server profiles according to the existing MX record setup (*SMTP server URL address* values to point to the addresses present in the MX records). This is the way for Email Gateway Security to forward incoming emails to Google. For details see [Configuration/Server profiles](/docs/mdemail/6.4.2/configuration/server-profiles) and [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).
3. Configure the appropriate security rules (the ones that will handle incoming email) as *Inbound* under **Security Rules / rule / GENERAL / Rule direction**. For details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).

   1. Set the server profiles created in the previous step as *SMTP relay server profile* for these rules.
4. Configure MetaDefender Email Gateway Security to listen on port 25. For details see the *SMTP servers* section in [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings).

Testing the configuration

Verify routing settings by sending an email to a Google Workspace recipient directly to the MetaDefender Email Gateway Security server and verify that it arrives correctly in the recipient’s inbox.

### [MX record redirection](/docs/mdemail/6.4.2/integrations/google-workspace#mx-record-redirection)

Refer to your Internet domain registrar for details how to change MX record to point to MetaDefender Email Gateway Security IP address.

Propagation delay

Make sure that the MX record changes have propagated and Time to Live (TTL) has expired before verifying email routing.

Testing the configuration

Verify email routing by sending an email to a Google Workspace recipient and verify that it arrives correctly in the recipient’s inbox.

## [Outbound email gateway](/docs/mdemail/6.4.2/integrations/google-workspace#outbound-email-gateway)

### [Overview](/docs/mdemail/6.4.2/integrations/google-workspace#overview)

To configure Email Gateway Security with Google Workspace for outbound email, we will perform the following steps:

An architecture like this is going to be created:

### [Google Workspace configuration](/docs/mdemail/6.4.2/integrations/google-workspace#google-workspace-configuration)

#### [Outbound forwarding configuration](/docs/mdemail/6.4.2/integrations/google-workspace#outbound-forwarding-configuration)

Unsecure configuration

The configuration described in this document focuses on a working connection only, and it may not result in a secure configuration.

Further reading

For detailed information about Google Workspace configuration see <https://support.google.com/a/answer/178333>.

Perform the following steps:

1. [Sign in](https://admin.google.com/) to your [Google Admin console](https://support.google.com/a/answer/182076).

Sign in using an *administrator account*.

2. From the Admin console Home page, go to **Apps > Google Workspace > Gmail > Advanced settings**.

**Tip:** To see *Advanced settings*, scroll to the bottom of the Gmail page.

3. In the **Organizations** section on the left, select the top-level organization (typically your primary domain).
4. Scroll to the **Outbound gateway** setting in the **Routing** section.
5. Enter the outbound gateway server address of the Email Gateway Security server.
6. At the bottom of the **Advanced settings** page, click **Save**.

#### [SMTP relay configuration](/docs/mdemail/6.4.2/integrations/google-workspace#smtp-relay-configuration)

Limits per user

The maximum number of messages a user can send in a 24-hour period is 10,000. However, this can vary, depending on the number of user licenses in your Google Workspace account.

A registered Google Workspace user can't relay messages to more than 10,000 unique recipients in a 24-hour period.

**Limits per customer**

The maximum number of *total__recipients* allowed per customer per 24-hour period is approximately 130 times the number of user licenses in your Google Workspace account, with an upper bound of 4,600,000 recipients per 24-hour period for large customers.

The maximum number of *total__recipients* allowed per customer *in a 10-minute window* is approximately 9 times the number of user licenses in your Google Workspace account, with an upper bound of 319,444 recipients per 10-minute window for large customers.

Unsecure configuration

The configuration described in this document focuses on a working connection only, and it may not result in a secure configuration.

Further reading

For detailed information about Google Workspace configuration see <https://support.google.com/a/answer/2956491>.

Perform the following steps:

1. [Sign in](https://admin.google.com/) to your [Google Admin console](https://support.google.com/a/answer/182076).

Sign in using an *administrator account*.

2. From the Admin console Home page, go to **Apps > Google Workspace > Gmail > Advanced settings**.

**Tip:** To see *Advanced settings*, scroll to the bottom of the Gmail page.

3. In the **Organizations** section on the left, select the top-level organization (typically your primary domain).

**Note**: You can configure the **SMTP relay service** setting for the top-level organization only.

4. Scroll to the **SMTP relay service** setting in the Routing section, hover over the setting, and click **Configure**. If the setting is already configured, hover over the setting and click **Edit** or **Add another**.
5. For a new setting, enter a unique description.
6. In the *Allowed senders* section, select **Only addresses in my domains.** This way the sender must be in one of your registered domains.
7. In the *Authentication* section, check **Only accept mail from the specified IP addresses**. This way the system only accepts email sent from Email Gateway Security.
8. Enter the IP address of Email Gateway Security:

   1. Click **Add IP RANGE**,
   2. Enter a description for the IP address,
   3. Enter the IP address of Email Gateway Security,
   4. Check the **Enabled** box to enable this IP address,
   5. Click **Save**.
9. Click **Add setting** or **Save**. Any new settings are added to the *Advanced* settings page.
10. At the bottom, click **Save**.

### [Email Gateway Security configuration](/docs/mdemail/6.4.2/integrations/google-workspace#email-gateway-security-configuration)

Perform the following steps:

1. Install and configure MetaDefender Email Gateway Security. For details see [Installation/Prerequisites](/docs/mdemail/6.4.2/installation/prerequisites).
2. Configure SMTP server profiles accordingly to route outgoing messages back to Google for delivery (*SMTP server URL address* values to point to Google SMTP-relay address *smtp-relay.gmail.com*). This is the way for Email Gateway Security to loop outbound emails back to Google after processing. For details see [Configuration/Server profiles](/docs/mdemail/6.4.2/configuration/server-profiles) and [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).
3. Configure the appropriate security rules (the ones that will handle outgoing email) as *Outbound* under **Security Rules / rule / GENERAL / Rule direction**. For details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).

   1. Set the server profiles created in the previous step as *SMTP relay server profile* for these rules.
4. Configure MetaDefender Email Gateway Security to listen on port 25. For details see the *SMTP servers* section in [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings).
