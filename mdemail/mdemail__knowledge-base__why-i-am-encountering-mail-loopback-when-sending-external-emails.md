<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/why-i-am-encountering-mail-loopback-when-sending-external-emails -->

# Why I am Encountering Mail Loopback When Sending External Emails?

When sending emails, an infinite email loop appears in the processing history of MetaDefender Email Gateway Security (EGS).

## [Cause](/docs/mdemail/knowledge-base/why-i-am-encountering-mail-loopback-when-sending-external-emails#cause)

The issue occurs when the SMTP relay server configured in EGS is the same as the mail server (MTA). This misconfiguration causes emails to be continuously relayed back to EGS, creating a loop.

## [Resolution](/docs/mdemail/knowledge-base/why-i-am-encountering-mail-loopback-when-sending-external-emails#resolution)

To fix this issue, please update the SMTP relay server profile in EGS to use a dedicated relay server.

If you do not set a dedicated SMTP relay server and continue using the same MTA for relaying, while sending an external email, the email flow will be as follows:

**Mail Client (e.g., Outlook, Thunderbird) ⇄ Mail Server (MTA) ⇄ EGS ↔ Mail Server (As an SMTP Relay) ⇄ EGS** *(Loop occurs here)*

This results in emails being stuck in an infinite loop.

### [**Steps to Resolve:**](/docs/mdemail/knowledge-base/why-i-am-encountering-mail-loopback-when-sending-external-emails#steps-to-resolve)

1. Check the EGS security rule settings and verify if the relay server is set as the same MTA.
2. Modify the SMTP relay server profile in EGS to use a separate, dedicated relay server instead of the MTA. On EGS > go to **Settings** > **Server Profiles** > **SMTP server profile**

3. Test email flow to confirm that the loop no longer occurs.

By ensuring a dedicated relay server is used, emails will be processed correctly without looping.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
