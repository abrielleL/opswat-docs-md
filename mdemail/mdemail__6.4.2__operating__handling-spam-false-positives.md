<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/handling-spam-false-positives -->

# Handling spam false positives

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#overview)

Email spam, also referred to as junk email, spam mail, or simply spam, is unsolicited messages sent in bulk by email. Email spam has steadily grown since the early 1990s, and by 2010s was estimated to account for around 90% of total email traffic. [[Wikipedia](https://en.wikipedia.org/wiki/Email_spam)]

Since the expense of the spam is borne mostly by the recipient, it is effectively postage due advertising. Thus, it is an example of a negative externality. [[Wikipedia](https://en.wikipedia.org/wiki/Email_spam)]

Emails classified as spam by OPSWAT are not harmful beyond the delivery cost and attention theft they cause to the receiving organization. Spam is discouraged and blocked at most of the organizations.

While organizations try to reduce the amount of spam delivered to their recipients, it is inevitable to detect some legitimate emails as spam and block these, ending up in false positives. This is a collateral damage, as the existence of spam (and the controls against it) cause normal emails to be blocked. Often normal emails are detected cause they bear the hallmarks of spam (e.g. sender IP blocklisted).

OPSWAT technologies -similarly to any other antispam technologies- cause false positive detections. In this article we give guidance how Email Gateway Security can be configured to detect less false positives and how already detected false positives can be handled.

## [Reducing false positives](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#reducing-false-positives)

In this section we discuss how to avoid spam false positives.

### [Detection threshold](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#detection-threshold)

Email Gateway Security gives a spam probability score to each email. The score value is as follows:

- 0: confident not spam
- 1 .. 8: possible spam (the higher the score, the more confident it is a spam)
- 9: confident spam

Emails with 0 probability score (not spam) are *always* handled according to the settings for non-spam emails.

Emails with 9 probability score (spam) are *always* handled according to the settings for spam emails (see the next section).

#### [Handling possible spam](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#handling-possible-spam)

Handling of emails with 1..8 probability score (the engine was uncertain if the email is spam or not) can be configured in the system to two ways: either handle as *Known Spam* or handle as *Potential Spam*.

The distinction between Known Spam and Potential Spam is set by the *Probability level*:

Emails that have the spam probability level set by the *Probability level* or higher (emails with spam probability level 5..9 using the example of the image above) are handled according to the *Known Spam* settings.

Emails that have the spam probability level below the *Probability level* (emails with spam probability level 1..4 using the example of the image above) are handled according to the *Potential Spam* settings.

Settings for each *Known Spam* (red) and *Potential Spam* (green) can be set for each *Security Rule* among on the *Anti-Spam* tab:

False positive reduction

Increasing the *Probability level* can reduce spam false positives handled as *Known Spam*.

As a negative side effect, this action may increase false negatives handled as *Potential Spam*.

For further details see [Anti-phishing and anti-spam](/docs/mdemail/6.4.2/configuration/policy#anti-phishing-and-anti-spam).

#### [Aggressiveness level](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#aggressiveness-level)

In **Settings > General** */ Anti-Spam / Aggressiveness level* Email Gateway Security’s anti-spam component can be configured how eager it should be when looking for (potential) spam.

False positive reduction

Lowering the *Aggressiveness level* can reduce spam false positives.

As a negative side effect, this action may increase false negatives

For further details see [Anti-spam](/docs/mdemail/6.4.2/configuration/settings#anti-spam).

### [Allowlisting](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#allowlisting)

#### [IP allowlist](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#ip-allowlist)

In **Settings > General** */ Anti-Spam /* *IP allowlist* a list of IPv4 addresses can be maintained for which anti-spam checks will be bypassed.

False positive reduction

Emails sent from the allowlisted IP addresses won't be detected as spam false positive as these messages skip anti-spam checks.

Difference to Trusted senders

Trusted senders makes IP allowlist redundant.

The main difference is that the

- *IP allowlist* is handled by the anti-spam engine after the email is forwarded to the engine for spam checking
- Emails matching the *Trusted senders* won't even be forwarded to the anti-spam engine, so this solution is a bit more resource efficient.
Limitations

The IP allowlist does not support subnets, only individua IP addresses.

For further details see [Anti-spam](/docs/mdemail/6.4.2/configuration/settings#anti-spam).

#### [Security rule](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#security-rule)

Using the filtering capability of security rules, a rule may be setup for allowlisting purposes.

First the filters of the rule must be set up to include the sender properties that are to be allowlisted (e.g. the IP address in the example below):

Relation among filter conditions

There are AND relations among filter condition blocks (i.e. *Sender IP address filter (PREVIOUS HOP)* **AND** *Sender domain or address filter (MAIL FROM)* **AND** *Recipient domain or address filter (RCPT TO)* **AND** *Active Directory filter*).

There are OR relations within a filter condition block (e.g. within the *Sender IP address filter (PREVIOUS HOP)* block there are OR relations between IP addresses).

Then the anti-spam capability needs to be disabled for the rule:

Depending on the filtering settings of the other rules, the allowlisting rule may need to be moved towards the top among the rules so that it can match the desired emails:

False positive reduction

Emails processed with an allowlisting rule created according to the steps above won't be detected as spam false positive as these messages skip anti-spam checks.

For further details see [Filtering](/docs/mdemail/6.4.2/configuration/policy#filtering).

#### [Trusted senders](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#trusted-senders)

Sender IP addresses, IP address ranges, domains or email addresses maintained in **Settings > Trusted senders** will bypass anti-spam checks.

False positive reduction

Emails sent from the trusted IP addresses, IP address ranges, domains or email addresses won't be detected as spam false positive as these messages skip anti-spam checks.

Difference to IP allowlist

Trusted senders makes IP allowlist redundant.

The main difference is that the

- *IP allowlist* is handled by the anti-spam engine after the email is forwarded to the engine for spam checking
- Emails matching the *Trusted senders* won't even be forwarded to the anti-spam engine, so this solution is a bit more resource efficient.

For further details see [Trusted senders](/docs/mdemail/6.4.2/configuration/trustedsenders).

## [Handling false positives](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#handling-false-positives)

In this section we discuss what are the different options to handle false positives after the system has already erroneously detected some legitimate emails as spam.

### [Controls to recipients](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#controls-to-recipients)

In this section we discuss workflows that administrators can set up so that recipients can control spam false positives for themselves.

#### [Spam notifications & actions](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#spam-notifications--actions)

When an email is detected as spam or possible spam, and get quarantined, Email Gateway Security supports the option to send an instant notification about the quarantined email (for details see [Alert, notification and quarantine report emails](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails)).

**Deliver original**

When the notification is configured with *Allow users the following actions* to include *Deliver original*, receivers of the notification will be permitted to deliver the original, unprocessed (no Multiscanning, no CDR, etc.) copy of the email.

False positive handling potential

With this procedure, whenever an email is erroneously detected as spam, the recipient gets notified about it, and the recipient will be able to get the email delivered directly.

Risk of outbreak

As with this method the recipient is entitled to release the original copy, there is a risk of malicious email outbreak.

**Anti-malware rescan**

When the notification is configured with *Allow users the following actions* to include *Anti-malware rescan*, receivers of the notification will be permitted to rescan the email with anti-malware controls (e.g. Multiscanning, CDR, OPSWAT Sandbox) but skipping anti-spam filtering. If the email turns out to be free of malware, it gets delivered at the end of the rescan.

False positive handling potential

With this procedure, whenever an email is erroneously detected as spam, the recipient gets notified about it, and the recipient will be able to initialize a rescan skipping anti-spam checks. If the email turns out to be clean (ignoring spam checks) then it gets delivered.

No risk of malware outbreak

With this method the email is checked for malware before it gets released.

#### [Quarantine reports & actions](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#quarantine-reports---actions)

When an email is detected as spam or possible spam, and get quarantined, Email Gateway Security supports the option to send *spam digest reports* about the quarantined emails detected as spam (for details see [Quarantine reports / User reports](/docs/mdemail/6.4.2/configuration/quarantine-reports#user-reports)).

**Limiting quarantine reports to spam emails only**

Administrators can reduce the risk of malicious email outbreak excluding emails from the spam digest report that have certain classifications (e.g. *Malware detected*, *Malicious behaviour,* etc.; red mark in the below example) besides the *Spam* (green mark in the below example) classification.

At the reporting frequency (top of the hour in the above example) each user that had a spam email detected since the last report, receives a digest email about their quarantined spam.

The users may be granted the same actions in the digest email as described in the *Spam notifications & actions* section above with the same false positive handling potential.

Delay

With this method the recipient does not get notified about spam immediately. When the spam false positive requires instant action (e.g. erroneously detected OTP token emails), this method may be not fast enough.

### [Controls to administrators](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#controls-to-administrators)

In this section we discuss workflows that administrators can set up for themselves to control spam false positives of the recipients.

Administrators can configure notifications or digest reports about spam similarly to how it was discussed in the *Controls to recipients* section above.

But when the administrators want to keep the right to themselves deciding what to deliver from the quarantine, and what not to, they grant the *Release request* action only to the recipients (instead of the *Deliver original* or the *Anti-malware rescan*).

This way recipients can request spam false positives to be released for them, but the recipients themselves can not actually release emails from the quarantine.

#### [Checking for spam requested to release](/docs/mdemail/6.4.2/operating/handling-spam-false-positives#checking-for-spam-requested-to-release)

Administrators can have several ways to check for spam emails that were requested to release. The two most convenient ways are discussed in this section.

**Quarantine subfolder**

Administrators may setup a quarantine subfolder using the *Save quarantine filter* function of the Quarantine.

With this method administrators can anytime check the Quarantine for spam emails that were requested for release.

Whenever a spam email gets requested for release, it shows up in this quarantine subfolder.

For details see [Saving filters](/docs/mdemail/6.4.2/operating/quarantine#saving-filters).

**Quarantine report**

Administrators may setup an administrator type quarantine report for themselves that report spam emails that were requested for release.

With this method administrators periodically receive a digest email about newly quarantined spam emails that were requested for release.

Administrator reports provide all supported functionality as actions to administrators, so administrators are entitled to release, rescan, etc. an email from the report.

For details see [Administrator reports](/docs/mdemail/6.4.2/configuration/quarantine-reports#administrator-reports) and [Supported functions](/docs/mdemail/6.4.2/operating/quarantine-reports#supported-functions).
