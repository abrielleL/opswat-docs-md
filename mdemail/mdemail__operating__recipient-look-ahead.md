<!-- source: https://www.opswat.com/docs/mdemail/operating/recipient-look-ahead -->

# Recipient look-ahead

Email Gateway Security is a forward only SMTP server, it was designed to not store emails (except the quarantined ones).

To avoid the situation that emails stuck on Email Gateway Security due to forwarding failures, the product can be configured to check whether it will be able to forward the email based on the current recipient settings. If it will be able to forward, then the email gets accepted accepts. But if there is no SMTP relay that would accept the recipient, so Email Gateway Security would not be able to forward the email to the next hop, then the email gets rejected on the SMTP level.

In this case the message *No policy for recipient* is returned to the sender’s email client.

For details see [Configuration/Recipient verification](/docs/mdemail/configuration/recipient-verification).
