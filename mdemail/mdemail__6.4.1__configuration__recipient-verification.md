<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/configuration/recipient-verification -->

# Recipient verification

## [Overview](/docs/mdemail/6.4.1/configuration/recipient-verification#overview)

Email Gateway Security can be configured to apply a rule only if the recipient of the email is accepted by any of the SMTP servers of the SMTP server profile configured for the rule.

## [The problem](/docs/mdemail/6.4.1/configuration/recipient-verification#the-problem)

This option can help avoiding situations when Email Gateway Security accepts emails even if it is known to be unable to forward it, cause no SMTP server will accept the recipient.

In such cases the email ends up in *Failed* status and pollutes the Email History with email junk that can not be delivered with a message in *Processing history* like *SMTP send failed to (Response: Unknown user (550, MailboxUnavailable)) smtp://localhost:25*.

Bulk emails to random (non-existing) recipients at an organization are usually sent as directory harvest attack (DHA) attempts so that attackers can discover valid recipients at the organization.

## [The solution](/docs/mdemail/6.4.1/configuration/recipient-verification#the-solution)

When this option is enabled, then before accepting the email, Email Gateway Security checks whether it will be able to forward it based on the current settings. If it will be able to forward, then accepts it. But if it knows that it will not be able to forward the email, then the email gets rejected on the SMTP level.

In this case the message *No policy for recipient* is returned to the sender’s email client.

Combining recipient verification with throttling or tarpitting requests to invalid email addresses, directory harvest attacks (DHA) can be made very ineffective (the attack will suffer a huge delay making it uneconomical).

## [How it works](/docs/mdemail/6.4.1/configuration/recipient-verification#how-it-works)

When *SMTP relay recipient verification* is enabled for the rule, then Email Gateway Security will attempt to initiate sending an email to the recipient via the SMTP servers of the SMTP server profile configured for the rule (GENERAL / SMTP relay server profile).

If the recipient (RCPT TO) is accepted by the remote SMTP server, then Email Gateway Security aborts the connection, and accepts the emails as it will be possible to be delivered.

## [Auto rule selection](/docs/mdemail/6.4.1/configuration/recipient-verification#auto-rule-selection)

Enabling *SMTP relay recipient verification* for all the rules, Email Gateway Security will apply the first rule for an email that will be able to deliver it to an SMTP destination.

## [SMTP server(s) unreachable](/docs/mdemail/6.4.1/configuration/recipient-verification#smtp-servers-unreachable)

If there are some SMTP servers in the server profile, that are not reachable, Email Gateway Security will accept the email, cause it can not ensure, whether the email can later be delivered or not.

## [Caching](/docs/mdemail/6.4.1/configuration/recipient-verification#caching)

On successful initiation recipient addresses are cached for 10 minutes. It means that within this timeframe Email Gateway Security won’t check whether the recipient will be accepted by the servers of the configured server profile, it assumes success.
