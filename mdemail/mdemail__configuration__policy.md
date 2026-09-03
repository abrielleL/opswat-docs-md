<!-- source: https://www.opswat.com/docs/mdemail/configuration/policy -->

# Policy

The policy how emails are handled in Email Gateway Security can be configured by the rules under the **Security Rules** page.

### Enable/Disable Security Rules

If you temporarily want to disable one or more Security Rules in MetaDefender Email Gateway Security, select the rule(s) to disable in the list and click the icon. To enable the rule again, select the rule(s) to enable and click the icon.

Risk of emails rejected

Disabling a Security rule can potentially cause emails to be rejected (if no other applicable Security rule can be located).

Disabled rules still do rescan

A disabled rule will still apply when attempting to perform a Rescan of the email.

### Open relay

MetaDefender Email Gateway Security displays warnings in case of Security Rules that have no filters set and as so have the potential to cause [open relay](https://en.wikipedia.org/wiki/Open_mail_relay).

Not necessary open relay

When Email Gateway Security warns for possible open relay, it does not necessarily mean that the email system as a whole behaves as an open relay. It warns for the potential.

Disabled rules

The warnings are shown for disabled Security Rules, too. Disabled rules, however, can not cause the system to be an open relay.

Open relay configuration still possible

Email Gateway Security can still be configured in a way to end up in open relay. Ineffective filters (a filter is set but does not effectively filter for anything, e.g. `.*` as the *Sender domain or address filter*) can cause such situations.

#### Intended open relay

Email Gateway Security may be configured as an open relay deliberately e.g. when there are other controls in the email processing pipeline that compensate for this, or when open relay is desired.

Suppress warning messages

To suppress warning messages for potential open relay, configure the problematic security rules with filters -that may even be ineffective.

### Direction

In traditional configurations MetaDefender Email Gateway Security is wedged between the organization's *email gateway* and *mail server* (see the image below). In case of *inbound* email directions the email is received from the email gateway and sent towards the mail server. In case of *outbound* directions the email is received from the mail server and sent towards the email gateway.

The direction of the email flow can be mapped to security rules in Email Gateway Security with defining:

1. Where emails are coming from, and
2. Where emails should be sent next after processing.

To configure direction for a certain security rule:

1. Apply appropriate filter settings for the **Security rules >*rule*/ FILTER / Sender IP address filter (PREVIOUS HOP)** to define where emails matching this rule are coming from.

SMTP relay recipient verification

This option makes Email Gateway Security to ensure that it will be able to forward the accepted emails upon completed processing.

When this option is not enabled, and the recipient of the email is not accepted by any SMTP servers of the server profile, then the email will end up in a retry loop, and finally in permanent failure.

When this option is enabled with no further filtering, then for each email the first rule will match, that will be able to forward that email.

2. Select the appropriate SMTP destination in **Security rules >*rule*/ GENERAL / SMTP relay server profile** to define where emails matching this rule should be sent next after processing. For further details about server profiles see [Configuration/Server profiles](/configuration/server-profiles).

When the filter and the SMTP relay are set appropriately to match emails coming from or going to a certain direction, then the **Security rules >*rule*/ GENERAL / Rule direction** can be set accordingly to *Inbound* or *Outbound* depending on the direction of the email flow.

#### DKIM signing

These options enables signing of emails with DKIM (DomainKeys Identified Mail), both for inbound email (ARC) and outbound (DKIM)

Configure DKIM certificates

As a prerequisite DKIM certificates need to be configured under **Settings > Security >** **Certificates**.

**Inbound direction: Authenticated Received Chain (ARC)**

In most of the cases Email Gateway Security acts as an intermediate email processing server between the original sender and the intended recipient. As Email Gateway Security is not the original sender the SPF check will fail on the recipients side. Email Gateway Security usually modifies emails (adds custom headers, and with Deep CDR and Proactive DLP it often modifies the email bodies and attachments) and as a result the DKIM verification will fail at the recipient.

[Authenticated Received Chain](https://en.wikipedia.org/wiki/Authenticated_Received_Chain) is an email authentication system designed to allow an intermediate mail server to sign an email's original SPF and DKIM authentication results. This allows a receiving service to validate an email when the email's SPF and DKIM records are rendered invalid by an intermediate server's processing.

With ARC, an intermediate processing server can digitally sign the SPF/DKIM results of the preceding server and its own modifications to the email with DKIM-like signatures.

1. Certificate: Certificate in **Settings > Security >** **Certificates** to be used to create the DKIM/ARC signatures.
2. Signer Domain: The domain for which to create the DKIM-like ARC signature. The next email processing server will look up the public keys in the DNS records of this domain to verify Email Gateway Security's ARC signature.
3. DNS Selector: Specifies the DNS location of the public key. Receiving servers use this selector to find the public key.

**Outbound direction: DKIM signing**

If your mail server does not attach a DKIM signature to your email, or if you make modifications to the email in MetaDefender Email Gateway Security you can opt to sign it here.

1. Certificate: Certificate in **Settings > Security >** **Certificates** to be used to create the DKIM/ARC signatures.
2. Signer Domain: The domain for which to create the DKIM signature. The next email processing server will look up the public keys in the DNS records of this domain to verify Email Gateway Security's DKIM signature.
3. DNS Selector: Specifies the DNS location of the public key. Receiving servers use this selector to find the public key.
4. Optionally, if your previous mail server did add a DKIM signature, then you can remove that, before adding the new one by checking *Remove existing DKIM signature before signing*.

Use sender's domain

With the *Use sender's domain* option enabled, Email Gateway Security will automatically take the domain part from the SMTP sender email address (`MAIL FROM`) and use it as the *signer domain* in DKIM or ARC signatures.

## Priority

Email Gateway Security supports the following three priority queues when processing emails:

1. High,
2. Normal and
3. Low.

The system will always give priority to emails with higher security rule priority.

Example

Processing of *Low* priority emails will start or continue only if there are no *High* and/or *Normal* priority emails waiting for processing.

Default

The default priority for each rule is *Normal*.

### Email History

The priority of the email is displayed in [Operating/Email History](/operating/email-history). The following icons represent each priority:

1. High: **↑**
2. Low: **↓**

Normal priority

For Normal priority there is no icon in the Email History.

## Rule order

Several security rules can be created that may target different messages from different sources going to different recipients. However, care must be taken how these rules are set up and ordered, as there is a *first match* and a *no match* policy (see the next two sections).

Specific rules should come first while generic rules should go at last.

Reordering Security Rules

The order of the rules can be set by drag and drop using the ⋮⋮⋮ icon in front of the rule entry (when the drag and drop is active, the mouse pointer changes to , see the image below).

### First match policy

If there are more matching rules in the system, then the email message will be accepted/rejected and processed according to the security policy of the first matching rule in the list.

### No match policy

If there is no matching rule in the system (or no rule at all), then the email message will be rejected.

Risk of blocking email flow

Deleting all security rules from the system results all email messages being blocked.

## Security rule configuration

### Filtering

#### Recipient verification

When *SMTP relay recipient verification* is enabled for the rule, then Email Gateway Security will attempt to initiate sending an email to the recipient via the SMTP servers of the SMTP server profile configured for the rule (GENERAL / SMTP relay server profile).

The rule is applied to the email only, if the connection initiation succeeds.

For details see [Configuration/Recipient verification](/configuration/recipient-verification).

#### Sender IP address conditions

Sender IP addresses are the addresses of infrastructure elements in the deployment, from which MetaDefender Email Gateway Security is allowed to receive emails according to this rule.

Example

In case of a traditional setup, for example, sender is the email gateway for inbound messages and the mail server for outbound messages.

| **Type** |  | IP address or subnet |
| --- | --- | --- |
| **Match type** |  | EQUALS |
| **Examples** | **IP** | 10.0.0.1 |
| **Examples** | **IP range** | 10.0.0.0/24 |

Relation

There is **OR** relation among entries in sender IP address conditions.

#### Sender domain or address conditions

Sender filter makes possible to apply security rule based on from what email address the email was sent. The value is taken from the SMTP communication’s *MAIL FROM* command that holds an email address.

Risk of spoofing

When using this filter please be aware of the fact that spoofing the sender of the email is a very easy task. A more secure way to use this filter would be for OUTBOUND emails only along with filtering to the sender IP.

**Field details**

| **Value type** | email address |
| --- | --- |
| **Field type** | [.NET Regex](https://learn.microsoft.com/en-us/dotnet/api/system.text.regularexpressions.regex) |
| **Match type** | regular expression match |
| **Examples** | - [.+@opswat.com](mailto:.+@opswat.com) - [somespecificuser@opswat.com](mailto:somespecificuser@opswat.com) - opswat.com (treated as [.+@opswat.com](mailto:.+@opswat.com)) |

Explicit filters

To avoid unexpected matching, special regular expression characters must be taken into consideration.

For example:

- The `.` (dot) in a regular expression matches any character. This means that `.+@opswat.com` can match `test@opswat1com`. If you want to match explicitly for a dot you should escape it like this: `.+@opswat\.com`
- The `^` (hat) and `$` (dollar) characters match the beginning and end of the string respectively. The regular expression `test@opswat\.com` may unexpectedly match `this_is_test@opswat.com` besides `test@opswat.com`. To match `test@opswat.com` explicitely, use the regular expression `^test@opswat\.com$`.

For more details see [.NET Regular Expressions](https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference).

Relation

There is **OR** relation among the sender domain or email address conditions.

#### Recipient domain or address conditions

Recipient conditions can help to restrict emails matched by the rule to specific recipients. The value is taken from the SMTP communication’s *RCPT TO* command that holds an email address.

Benefits of recipient filtering

Recipient domain or email address conditions can also help to counter emails sent to invalid recipients; that do not even exist at an organization or among the partners, for example.

This kind of defense may protect against unnecessary overloads or even against malicious attacks.

**Field details**

The field details are identical to the field details of the sender domain or address conditions (for details see the *Sender domain or address conditions* section).

#### Email header conditions

Email header conditions help to define email processing based on the email headers rather than SMTP properties (for example as email and SMTP properties are sometimes not in-line, e.g. email *From* and SMTP *MAIL FROM* may be different).

Accepted recipients may not match

Header filters might cause already accepted recipients to finally match no rule. When there is no matching rule, the email (for the recipients that have no matching rule) can not be processed and delivered. Such messages are retained in Email Gateway Security's Email History with the classification *Forbidden*.

For details see the *Forbidden* subsection in [Permanent failure statuses](/operating/email-history#permanent-failure-statuses) and [Failed and Forbidden emails](/operating/email-history#failed-and-forbidden-emails).

**Field details**

Relation

There is **OR** relation among the email header conditions.

***Header name***

| **Value type** | [RFC 5322 field name](https://datatracker.ietf.org/doc/html/rfc5322#section-3.6.8) |
| --- | --- |
| **Field type** | text |
| **Case sensitivity** | case insensitive |
| **Match type** | EQUALS |
| **Examples** | - Subject - from - X-Metadefender-EmailSecurity-OriginalCopy |

***Header value***

| **Value type** | [RFC 5322 unstructured](https://datatracker.ietf.org/doc/html/rfc5322#section-2.2.1) |
| --- | --- |
| **Field type** | [.NET Regex](https://learn.microsoft.com/en-us/dotnet/api/system.text.regularexpressions.regex) |
| **Case sensitivity** | case insensitive |
| **Match type** | regular expression match |
| **Examples** | - [.+@opswat.com](mailto:.+@opswat.com) |

Explicit filters

To avoid unexpected matching, special regular expression characters must be taken into consideration.

For example:

- The `.` (dot) in a regular expression matches any character. This means that `.+@opswat.com` can match `test@opswat1com`. If you want to match explicitly for a dot you should escape it like this: `.+@opswat\.com`
- The `^` (hat) and `$` (dollar) characters match the beginning and end of the string respectively. The regular expression `test@opswat\.com` may unexpectedly match `this_is_test@opswat.com` besides `test@opswat.com`. To match `test@opswat.com` explicitly, use the regular expression `^test@opswat\.com$`.

For more details see [.NET Regular Expressions](https://learn.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference).

Case insensitive regular expressions

Regular expressions for the header value are always treated with case insensitive.

For example *hello* as the header value pattern will match both *hello* and *Hello* even when case insensitive option is not applied.

#### Importing from CSV

Entries for the `Sender IP address filter (PREVIOUS HOP)`, `Sender domain or address filter (MAIL FROM)`, `Recipient domain or address filter (RCPT TO)` and `Email header filter` filters can be imported from comma separated value (CSV) files. The values imported from a file are added only on the GUI, ignoring values that already have an entry.

Valid syntax

For **Sender IP address filter (PREVIOUS HOP)**, **Sender domain or address filter (MAIL FROM)** and **Recipient domain or address filter (RCPT TO)** one IP address or email address or domain respectively for each line.

`"<IP address>"`

**Email header filter**

`"<email header name>","<email header value>"`

example:

`"From","mdemailsecurity@opswat.com"`

#### Exporting to CSV

Visible values are exported

The values exported to a CSV file export only what is visible on the GUI. The export ignores what values are actually present in the database in case the modifications have not been saved yet.

#### Bulk delete filter conditions

Administrators can select and delete multiple entries at once across all security rule filter categories, including Sender IP address, sender domain or address, recipient domain or address, and email header filters.

### SMTP relay

After processing, emails must be forwarded by Email Gateway Security to an SMTP destination so that recipients can receive them.

For each security rule the SMTP destination can be set in **Security rules >*rule*/ GENERAL / SMTP relay server profile** to define where emails matching this rule should be sent next after processing.

There are two ways of SMTP delivery:

1. Normal delivery: when an `SMTP server` type server profile is selected for the **SMTP relay server profile**, the email gets delivered to exactly one SMTP server. The destination SMTP server is selected according to the server preference settings in the `SMTP server` type server profile.

2. Multi-delivery: when an `SMTP multi-delivery` type server profile is selected for the **SMTP relay server profile**, the email is intended to get delivered to multiple SMTP servers. For each member `SMTP server` type server profile of the `SMTP multi-delivery` type server profile the destination SMTP server is selected according to the server preference settings in the `SMTP server` type server profile.

For further details about server profiles see [Configuration/Server profiles](/configuration/server-profiles).

### Rule actions

It is possible to add disclaimers and/or tags to all emails processed by a specific security rule.

#### **Rule disclaimer**

To add a disclaimer to all emails processed by this specific rule, enable the option **Security rules >*rule*/ GENERAL /** **Rule disclaimer** and configure the disclaimer content using the disclaimer editor.

#### **Rule email headers**

To add one or more custom email headers to all emails processed by this specific rule, click on the option **Security rules >*rule*/ GENERAL /** **Rule email headers** and complete the configuration in the header editor.

#### **Rule tags**

To add one or more tags to all emails processed by this specific rule, click on the option **Security rules >*rule*/ GENERAL /** **Rule tags** and complete the configuration in the tag editor.

### Security policy

The security policy of a certain rule is defined by the settings on the SCAN, ADVANCED THREAT PREVENTION, ZERO-DAY MALWARE PREVENTION, ANTI-PHISHING, UPLOAD ATTACHMENTS and ADVANCED tabs.

#### Scan

On the *Scan* tab of a certain rule it can be defined if emails matching this rule must be scanned at all, or not.

**MetaDefender Core server profile**

A *MetaDefender Core* server profile to which emails are sent for malware scanning and zero-day malware prevention. For further details see [Configuration/Server profiles](/configuration/server-profiles).

**MetaDefender Core Workflow**

The Workflow defined on the MetaDefender Core specified by the *MetaDefender Core server profile* field. This Workflow specifies how the email gets processed by Core.

Moved from Server Profile

This configuration option was moved here from the Settings > Server Profiles in Email Gateway Security 6.1.1.

Email Gateway Security supports different Core _Workflow_s for different email parts (headers, bodies and attachments). For details see the *Scan email headers, body and attachments* subsection below.

**Scan email headers, body and attachments**

Email Gateway Security is capable to process email headers, body and attachments, thus find malicious or sensitive content not only in attachments, but even in the body or headers.

*Scan email body* will scan the body (both the HTML and the plain text body) including all the inline, embedded attachments (inline attachments are the non-text elements embedded into the HTML email body, e.g. inline images).

If *Enable MetaDefender Cloud Safe URL redirect* is turned on, all links in the email body will be redirected through [MetaDefender.com](https://metadefender.opswat.com/) [Safe URL redirect](https://onlinehelp.opswat.com/mdcloud/1._Safe_URL_redirect.html) service for URL reputation check.

MetaDefender Cloud license required

For the *MetaDefender Cloud Safe URL redirect* feature to work properly, MetaDefender Cloud’s Reputation API must be licensed.

For demonstration purposes, however, a limited number of Reputation API calls are available for free of charge.

*Scan attachments* can toggle scanning the regular (non-inline) attachments.

Examples

An email with an embedded (inline) image attachment:

An email with a regular attachment (in Thunderbird):

Email Gateway Security supports different Core _Workflow_s for different email parts (headers, bodies and attachments).

To turn on this feature for the Security Rule, enable the Rule's *Advanced / Override settings / Allow specific MetaDefender workflow for email parts* option.

When this option is enabled, for each email part a different Core *Workflow* of the selected Core *Server Profile* can be specified.

**Scan email as a whole**

This option can help better utilizing certain OPSWAT technologies -like [MetaDefender Aether](https://www.opswat.com/products/metadefender/aether)- that work better on whole emails than on parts of the email. When Aether is enabled in the Core side rule it can be benefical to enable sending emails as a whole, too.

**Attaching scan results**

For certain use-cases it may be beneficial to attach the MetaDefender Core scan results to the email. This is supported by enabling the *Attach scan results* option.

Scan results attached to blocked notifications

This option will also attach the scan results to the notification emails sent when the email gets blocked.

**Hash lookup**

To shorten email processing time Email Gateway Security can be configured to perform hash lookups to MetaDefender Core and MetaDefender Cloud (whatever is set as the MetaDefender Core type server profile for the rule).

If the email header, body, attachment or the whole email is found by the hash, then it won't be sent to MetaDefender Core / Cloud for scanning or processing. This way the scanning and processing time can be saved.

MetaDefender Core / Cloud will return the cached scan results and the cached processed version of the header, body or attachment.

Email headers are always different, but bodies and attachments can be the same among separate emails (for example in case of a newsletter that is sent to hundreds of recipients within an organization). Email Gateway Security comes with reasonable defaults to do hash lookup on attachments (both inline and non-inline attachments).

Performance penalty

Hash lookups give a benefit only when parts of the email were previously scanned and exist in the cache.

If the email part does not exist in the cache, then the time of the hash lookup adds to the time of the processing and as so for such a case the total processing time will be longer than without the hash lookup.

Enabling *Force scan on mismatch* the hash lookup will be omitted when the actual file name and the cached file name do not match. In this case the header, body or attachment will be forcibly scanned, even if the result already exists in the cache based on the hash of the file. For further details see [Configuration/Email History/Malware scan details](/operating/email-history#malware-scan-details).

#### Advanced Threat Prevention

Using [multiscanning](https://www.opswat.com/technologies/multiscanning), Email Gateway Security can utilize even 20 anti-malware engines to prevent advanced, unknown threats.

On this tab it can be configured what Email Gateway Security should do if its Advanced Threat Prevention feature found malware in one or more components of the email.

If *Quarantine original email* is enabled, then the original copy of the email is put into the [Operating/Quarantine](/operating/quarantine) regardless of how *Handling of the email* is set.

*Handling of the email* may be:

- Block email: the email is blocked. If *Notify recipients if email is blocked* is enabled, then a notification will be sent to the recipients. For further details see [Configuration/Alert, notification and quarantine report emails](/configuration/alert--notification-and-quarantine-report-emails).

- Delete blocked contents: the blocked contents (e.g. infected attachments) are removed from the email. The remaining is delivered.
- Deliver blocked contents: the email is delivered containing the potentially malicious (infected) contents.

Attachment removal

For *Delete blocked contents* or *Deliver blocked contents* options Email Gateway Security provides customization to remove attachments.

Risk of outbreak

Selecting *Deliver blocked contents* will deliver potentially malicious contents to recipients.

If Email Gateway Security is set to *Notify recipients if email is blocked* then notifications may be limited to the case of emails with password protected attachments. To do so set *Send notifications for* to *Only emails with password protected attachments*.

**Blocked notifications**

It is possible to send the recipient a blocked notification when an email is blocked and put in quarantine. The options available for the notifications are:

***Subject***

Allows customization of the notification subject.

***Send notifications for***

Whether to send the notification for all emails that were blocked by MetaDefender Core, or only for those that were detected with password protected attachments.

***Notification template***

By default, each rule uses the built-in (`default`) notification template.

Selecting a custom variant overrides the default for notifications triggered by this rule, allowing different recipient groups to receive customized notifications.

For details see [Alert, notification and quarantine report emails](/configuration/user-interface-customization#alert-notification-and-quarantine-report-emails).

***Send notification for original sender***

Send the notification to the original email sender (recommended for outbound emails).

***Send notification for original recipient(s)***

Send the notification to the original email recipients (recommended for inbound emails).

***Additional recipients***

Allows sending the notification to a set to fixed recipients, such as an administrator etc.

***User permissions***

When sending a blocked notification it is possible to permit the recipient to perform actions on the quarantined email.

The following permissions are supported:

1. Rescan emails: Allows the recipient to initiate a rescan of the content. This is useful, for example, when an email contains password protected attachments. The use can specify the password(s) and allow MetaDefender Email Gateway Security to scan the decrypted content
2. Anti-malware rescan: Similar to Rescan emails except that anti-spam and anti-phishing checks are skipped. This way false positive spam or phishing emails can be delivered while anti-malware measures (Multiscanning, Deep CDR, Sandbox, etc.) still apply.
3. Delete emails: Allows the recipient to permanently delete the email from the Quarantine. This could be allowed for, for example, spam emails that the recipient does not wish to receive or keep.
4. Deliver original emails: Allows the recipient to deliver the quarantined (unscanned) email. This permission is not recommended since it could potentially deliver malicious content to the recipient.
5. Release request: Allows the recipient to request the release of an email. An email that has been requested for release will obtain the 'Release request' classification which informs the administrator that a recipient wants his email released.
6. Add to Trusted senders (global): Allows recipients to trust the sender system wide for any recipient.
7. Add to Trusted senders (user): Allows recipients to trust emails exchanged exclusively between themselves and the sender.

Release requests

In order for an administrator to be informed of release requested emails an administrator Quarantine Report can be created, filtering on the Release Request classification. For more information, see [Configuration/Quarantine reports](https://docs.opswat.com/mdemail/configuration/quarantine-reports).

***Notification email headers***

Add the custom headers (X-headers) defined here to the notification email.

**Forward blocked emails**

The original copy of each blocked email can be forwarded to dedicated recipients (e.g. to a SoC email address for further analysis).

**Encrypted attachments**

Email Gateway Security supports functionality to automatically attempt to decrypt attachments by analyzing the email body for possible password(s). To enable this functionality, select the option *Decrypt password protected attachments*.

Password formulas

Email Gateway Security use regular expressions to find the password in the email body. These regular expressions can be configured under **Settings > General** */ Attachment password patterns*.

For details see [Attachment password patterns](/configuration/settings#attachment-password-patterns).

In case password(s) cannot be located in the email body, a notification email can be sent (*Handling of the email* is set to *Block email*) or disclaimer can be added (*Handling of the email* is set to *Delete blocked contents*) to the email, allowing the recipient to provide the password and rescan the email.

Sometimes it is the email body that contains the instructions how the password needs to be formulated. For this use-case Email Gateway Security can display the email body in the rescan page. To use this feature, enable the *Display email body on the rescan page* option.

Use the *Encrypted disclaimer* to customize the message added to the email requesting a rescan (not applicable when *Block Email* is selected as *Handling of the email* action)

***Password storage***

From MetaDefender Core version 5.12.0, password storage is supported in Core workflows. When Email Gateway Security is integrated to Core using a workflow where password storage is configured, then Core will attempt to decrypt encrypted attachments using the passwords configured in the Core workflow. This way encrypted attachments may be processed automatically without the need to extract the password from the email body or to request the password from the recipient.

Password storage requires two steps to work with MetaDefender Core workflows:

1. Define one or more password storage(s) under **Inventory > Password Storage** in Core

2. Link the password storage(s) to the workflow under **Workflow Management > Workflows** */ [Workflow] / Archive / Password storage*

For details see the *Password storage for handling encrypted file* section in [MetaDefender Core 5.12.0 Release notes](https://docs.opswat.com/mdcore/release-notes/release-notes#new-features-improvements-and-enhancements).

**Tombstone files**

For the use-cases where Email Gateway Security might remove attachments:

1. *Handling of the email* is set to *Delete blocked contents* or
2. *Remove attachments* is enabled

it is supported to replace the removed attachment (both inline and regular attachments) with a tombstone file.

Tombstone file

A tombstone file is a small plain text placeholder file to replace the original, blocked attachment.

File name format: `<original attachment file name>.tombstone.txt`

Contents:

JsonCopy{
"data_id":"<data id of original file scan result processed by MetaDefender Core>",
"file_info": {
"sha256": "<SHA256 hash of original file>"
},
"process_info": {
"blocked_reason": "<blocked reason to indicate why original file was blocked>"
}
}

#### Zero-Day Malware Prevention

Using [content disarm and reconstruction](https://www.opswat.com/technologies/data-sanitization), Email Gateway Security can prevent zero-day malware in [over 100 common file types](http://onlinehelp.opswat.com/cdr/).

The content disarm and reconstruction capabilities can be configured for each MetaDefender Core server. For further details see [Configuration/Server profiles](/configuration/server-profiles).

On this tab it can be configured what Email Gateway Security should do if its Zero-Day Malware Prevention feature applied disarm and reconstruction to one or more components of the email.

If *Quarantine original email* is enabled, then the original copy of the email is put into the [Operating/Quarantine](/operating/quarantine).

**Overriding sanitization behavior**

Sanitization can fail for two reasons in Email Gateway Security:

1. The Deep CDR engine fails to sanitize the file (the file type version is not supported or the engine has other trouble)
2. The email body is converted by the Deep CDR engine to a file type that is not supported as email body (e.g. the plain text body is converted to pdf).

Supported email body file type conversions

Only the following email body file type conversions are allowed in Email Gateway Security:

1. txt  txt
2. html  html
3. html  txt

Any other email body file type conversion set in the Deep CDR engine will cause a sanitization failure.

Default to remove failed

By default Email Gateway Security removes all the bodies and attachments for which the sanitization failed from the email to be delivered.

The default behavior can be customized enabling the *Override sanitization behavior* option and selecting the cases for which Email Gateway Security should deliver the original copy of the body or attachments in case of a sanitization failure.

Risk of outbreak

Selecting attachment or email body categories in *Send original file, if sanitization failed for* increases the risk of delivering malicious emails.

Especially when the MetaDefender Core side workflow—that handled the file for which the sanitization failed—has no other control (Multiscanning, Proactive DLP, Adaptive Sandbox, etc.) enabled that could detect the malicious email component.

#### Data loss prevention

When Proactive Data Loss Prevention is licensed (see [Installation/Licensing](/installation/licensing)), certain behavior of the technology can be modified on this tab.

Enabling *Send sanitized version of blocked files only if redacted* can influence the setting under *Zero-Day Malware Prevention / Override sanitization behavior / Send sanitized version of blocked files*. A sanitized version is sent only, if it could have been successfully redacted, too.

Example

As of today, Proactive DLP can detect sensitive data in PowerPoint presentations (.ppt), but can not redact.

If both *Send sanitized version of blocked files* and *Send sanitized version of blocked files only if redacted* then the sanitized version won’t be sent for .ppt files as they can not be redacted.

How to enable?

The *Send sanitized version of blocked files only if redacted* option can be enabled only when for the Security Rule

1. on the *Advanced Threat Prevention* tab the *Handling of the email* option is set to *Delete blocked contents* AND
2. on the *Zero-Day Malware Prevention* tab the *Override sanitization behavior* option is enabled.

Enabling *Send redacted version of blocked files* will deliver redacted email contents - when redaction is available for the file type - if they were blocked due to sensitive data only.

Infected contents

Malware infected contents won’t be delivered even when this option is enabled.

How to enable?

The *Send redacted version of blocked files* option can be enabled only when for the Security Rule

1. on the *Advanced Threat Prevention* tab the *Handling of the email* option is set to *Delete blocked contents* AND
2. on the *Zero-Day Malware Prevention* tab the *Override sanitization behavior* option is disabled.

#### Anti-phishing and anti-spam

Email Gateway Security provides cutting edge anti-spam and anti-phishing protection. Spam and phishing are handled by the same component so the settings are quite similar. For specific settings see the two subsections at the end of this section.

**Probability level**

The anti-spam and anti-phishing component use the *Probability level* setting to tell the component what it should treat as *Possible spam* or *Possible phishing* (for details see [Operating/Email classifications](/operating/email-classifications)) and what is known *Spam* or *Phishing* (for details see [Operating/Email classifications](/operating/email-classifications)).

Probability levels

Email Gateway Security can assign the following probability levels to spam and phishing emails:

- 0: not a spam or phishing,
- 1-8: possible spam or phishing (the higher the number, the higher the probability),
- 9: known spam or phishing.

The levels 0 and 10 are not configurable.

Example 1

In the example below Email Gateway Security assigned the spam probability level 9 to the email.

Example 2

In the example below the *Probability level* is set to 4.

It means, that

- all email that’s probability level is higher or equal than 4, will be treated as known *Phishing*, while
- all email that’s probability level is lower than 4 will be treated as *Possible phishing*
- (all email that’s probability level is 0 will be treated as not phishing)

Example 3

If the *Probability level* is set to 9, then only emails with probability level 9 will be treated as known *Spam* or *Phishing*. Emails with levels 1-8 will be treated as *Possible spam* or *Possible phishing*.

**Actions for known or potential phishing and spam**

Based on the probability level, Email Gateway Security can be configured to handle known and potential spam or phishing in different ways.

The following actions are available:

| **Action** | **Description** |
| --- | --- |
| Reject | Perform an IP reputation check and if turns out to be a (potential) spam or phishing sender, then reject the email on the SMTP level. The email will show up in **Audit > Refused Emails**. |
| Delete | Receive the email, perform an IP reputation and/or content check, and if turns out to be a (potential) spam or phishing, then delete it. The email will show up in **Audit > Email History** with some additional details as if it was rejected and with the appropriate classifications added (for details see [Operating/Email History](/operating/email-history) and [Operating/Email classifications](/operating/email-classifications)). |
| Quarantine | Receive the email, perform an IP reputation and/or content check, and if turns out to be a (potential) spam or phishing, then quarantine it (just like infected emails). The email will show up in **Quarantine** with the appropriate classifications added (for details see [Operating/Quarantine](/operating/quarantine) and [Operating/Email classifications](/operating/email-classifications)). |
| Deliver | Receive the email, perform an IP reputation and/or content check, but even if it turns out to be a (potential) spam or phishing, deliver it (just like clean emails). The email will show up in **Audit > Email History** with the appropriate classifications added (for details see [Operating/Email History](/operating/email-history) and [Operating/Email classifications](/operating/email-classifications)). |
| Add headers | If the known or potential *action* is set to *Deliver*, then headers can be added to the email for each case. These headers can indicate for example to the receiving side that a (potential) phishing has just been received. |

**Blocked notifications**

It is possible to send the recipient a blocked notification when a spam and/or phishing email is put in quarantine. The options available for the notifications are identical as for Advanced Threat prevention (see above).

**Disclaimers**

It is supported to amend an email detected as known spam or - phishing or potential spam or - phishing with a disclaimer if the *processed version* of the email finally gets delivered. Such an email may get finally delivered if the *action* is set to *Deliver*; or the *action* is set to *Quarantine* and the email gets delivered after a *Full rescan* or an *Anti-malware rescan*. The idea behind this behavior is that this way recipients can be alerted about the potential risks in spam and phishing emails even after being delivered by a rescan.

Disclaimers won't be appended to the email when the email is *released*, *forwarded* or *downloaded* from the Quarantine.

For details see the *Full rescan email* and *Anti-malware rescan email* sections in [Supported functions](/operating/quarantine-reports#supported-functions); and [Disclaimers](/configuration/disclaimers).

**Anti-spam specific settings**

Email Gateway Security’s ant-spam component can detect some kind of graymail, too. Enabling *Classify marketing/bulk email as spam* will instruct Email Gateway Security to treat email detected as marketing and bulk as spam and handle it according to the anti-spam settings.

**Anti-phishing specific settings**

***SPF lookup***

It is possible to enable/disable the Sender Policy Framework (SPF) verification as a part of the Anti-Phishing feature. For more information on SPF, see [Sender Policy Framework](https://en.wikipedia.org/wiki/Sender_Policy_Framework).

Internal/Private IP addresses

SPF lookup will never be attempted if an email originates from an internal/private IP address, regardless if the option is enabled or not.

SPF on email From header

Email Gateway Security extends checking SPF records not only by the `MAIL FROM` domain, but by the email's `From` header domain, too. This strict checking can be reverted to the standard when disabling *Check FROM header address*.

***DKIM signature validation***

DKIM signature validation can be enabled/disabled depending on preference and infrastructure.

3rd party software

If the mail flow includes any 3rd party software modifying the email content in any way before reaching MetaDefender Email Gateway Security, this might break the email's DKIM signature and produce a validation failure. In this case, simple omit the DKIM validation by disabling this option.

***Enforce DMARC policy when available***

When this option is enabled, Email Gateway Security enforces the DMARC policy according to the sender domain settings (if DMARC is available in the domain records of the sender domain). The potential outcomes:

1. Pass: the email continues processing normally; `DMARC Pass` classifcation added
2. Fail: if the DMARC policy is `Reject` or `Quarantine` then the email gets handled as known phishing with `Phishing` classification by default; `DMARC Fail` classifcation added

   1. When the outcoume is Fail but the policy set by the sender domain is `None` then the email continues processing as non-phishing; `DMARC Fail` classification added
3. Error: the email continues processing; `DMARC Error` classifcation added
4. Disabled (no DMARC records in the DNS or email not checked due to DMARC sampling): the email continues processing

Tune handling policy

It is supported to tune what DMARC policies to handle as `Phishing` or `Possible Phishing`.

By default, `Reject` and `Quarantine` are handled as known phishing and classified and as `Phishing`.

For details see the *Actions for known or potential phishing and spam* section above and [Registry configuration](/configuration/registry-configuration).

DMARC reporting is not yet supported

DMARC reporting is planned to be addressed in a later release.

SPF and DKIM required

As DMARC uses the outcome of the SPF and DKIM verification, the *Enforce DMARC policy when available* option is available only when *Enable SPF lookup* and *Enable DKIM signature validation* are on.

Standard SPF only

For the DMARC verification only the *standard SPF* check result (the domain in the `MAIL FOM` SMTP command) is used, the *From header SPF* result (the domain in the `From` email header) is not.

For details see the *SPF lookup* subsection above.

***URL reputation lookup***

With this option enabled Email Gateway Security checks the reputation of the URLs extracted from the email body. If any URL is found malicious then the email gets classified as *Phishing* and treated according to the settings for *known phishing* emails.

MetaDefender Cloud subscription needed

The URL reputation lookup uses the URL reputation services of MetaDefender Cloud. An appropriate MetaDefender Cloud subscription is needed for this capability to work.

The MetaDefender Cloud subscription is connected to the URL reputation lookup capability through a *MetaDefender Core* type server profile that has one of its servers configured as *MetaDefender Cloud*.

The MetaDefender Cloud subscription is connected to the URL reputation lookup capability through a *MetaDefender Core* type server profile.

This server profile has to have its type as *MetaDefender Core*. At least one of its servers must be *MetaDefender Cloud.*

At least one of the servers of this server profile must be *MetaDefender Cloud.*

***Authenticated Received Chain*** ***(****ARC****)***

In most of the cases Email Gateway Security acts as an intermediate email processing server between the original sender and the intended recipient. As Email Gateway Security is not the original sender the SPF check will fail on the recipients side. Email Gateway Security usually modifies emails (adds custom headers, and with Deep CDR and Proactive DLP it often modifies the email bodies and attachments) and as a result the DKIM verification will fail at the recipient.

[Authenticated Received Chain](https://en.wikipedia.org/wiki/Authenticated_Received_Chain) is an email authentication system designed to allow an intermediate mail server to sign an email's original SPF and DKIM authentication results. This allows a receiving service to validate an email when the email's SPF and DKIM records are rendered invalid by an intermediate server's processing.

With ARC, an intermediate processing server can digitally sign the SPF/DKIM results of the preceding server and its own modifications to the email with DKIM-like signatures.

To enable ARC, go to **Security Rules >** ***rule*** **/** **General** and enable the *Sign with DKIM (ARC)* option.

Configure DKIM certificates

As a prerequisite DKIM certificates need to be configured under **Settings > Security >** **Certificates**.

1. Certificate: Certificate in **Settings > Security >** **Certificates** to be used to create the ARC signatures.
2. Signer Domain: The domain for which to create the DKIM-like ARC signatures. The next email processing server will look up the public keys in the DNS records of this domain to verify Email Gateway Security's ARC signatures.
3. DNS Selector: Specifies the DNS location of the public key. Receiving servers use this selector to find the public key.

#### Upload attachments

**Prerequisites**

Configuring the *Upload attachments* capability requires some technical understanding of MetaDefender Managed File Transfer.

For details about MetaDefender Managed File Transfer see [https://onlinehelp.opswat.com/mdmft/](https://onlinehelp.opswat.com/vault/).

For details about integrating Email Gateway Security and Managed File Transfer see [Integrations/Integration with MetaDefender Managed File Transfer](/integrations/integration-with-metadefender-mft).

The *Upload attachments* capability requires a MetaDefender Managed File Transfer server profile to be configured and set for the *MetaDefender Managed File Transfer* *server profile* value. For details see [Configuration/Server profiles](/configuration/server-profiles).

**Attachment notice**

Setting the *Attachment notice* a custom notification text can be configured to be appended to emails notifying recipients about where they can access their files in MetaDefender Managed File Transfer.

The *Attachment notice* works the same way as other disclaimers do. For details see [Configuration/Disclaimers](/configuration/disclaimers).

Required disclaimer variable

You should not remove **%[]mft_list[]%** from the notification texts as it would lead to missing URLs. For details see [Configuration/Disclaimers](/configuration/disclaimers).

**Upload blocked attachments**

By selecting this option, the original copy of every attachment which was blocked will be uploaded to MetaDefender Managed File Transfer.

**Upload sanitized attachments**

By selecting this option, the sanitized copy of every attachment which was [sanitized](https://onlinehelp.opswat.com/cdr/) will be uploaded to MetaDefender Managed File Transfer.

To upload the original copy of the sanitized attachments see [Configuration/Policy](/configuration/policy).

**Upload partially sanitized attachments**

By selecting this option, the original copy of every attachment which was partially [sanitized](https://onlinehelp.opswat.com/cdr/) will be uploaded to MetaDefender Managed File Transfer.

Requires MetaDefender Core setting

This requires the 'Distinguish partial archive sanitization result' option checked in the MetaDefender Core rule used to scan content with. See [MetaDefender Core > 3.6.2. Workflow template configuration](https://onlinehelp.opswat.com/corev4/3.6.2._Workflow_template_configuration.html) for more information.

**Upload original of sanitized attachments**

By selecting this option, the original copy of every attachment which was [sanitized](https://onlinehelp.opswat.com/cdr/) will be uploaded to MetaDefender Managed File Transfer.

Upload only once

If both *Upload original of sanitized attachments* and *Upload attachments that failed sanitization* are enabled –and the sanitization fails– then the original file will be uploaded only once.

**Upload attachments that failed sanitization**

By selecting this option every attachment where the [sanitization](https://onlinehelp.opswat.com/cdr/) failed will be uploaded to MetaDefender Managed File Transfer.

Upload only once

If both *Upload original of sanitized attachments* and *Upload attachments that failed sanitization* are enabled –and the sanitization fails– then the original file will be uploaded only once.

**Upload bypassed attachments**

By selecting this option every attachment that was bypassed (for details see [Operating/Bypassing](/operating/bypassing)) by Email Gateway Security will be uploaded to MetaDefender Managed File Transfer.

**Upload allowed attachments**

By selecting this option every attachment which was allowed will be uploaded to MetaDefender Managed File Transfer.

Allowed but sanitized won't upload

Please note that if an attachment is allowed but gets sanitized then it won't be uploaded if only the *Upload allowed attachments* option is set.

If you want to upload these kind of attachments you should have *Upload original of sanitized attachments* enabled.

**Options**

***Skip supervisor approval***

Enable this option to skip supervisor approval of attachments that were uploaded to MetaDefender Managed File Transfer (MFT). Supervisor approval adds an extra layer of security by requiring a supervisor or designated authority to approve file availability file transfers or data sharing activities in MFT before they proceed.

Supporting MFT versions

Skip supervision capability is available in MetaDefender Managed File Transfer 3.9.1 and newer.

For this functionality to work, Email Gateway Security must be integrated to MFT using a *System Level API Key* that has set *Allow Skip Supervision* enabled.

This is how such an API key is defined on the MFT side (for details see For details see <https://www.opswat.com/docs/mdmft/end-user-guide/supervisor-approval> and <https://www.opswat.com/docs/mdmft/configuration/api-keys>):

This is how such an API key is used with a *MetaDefender Managed File Transfer* type server profile (for details see [Server profiles](/configuration/server-profiles)):

***Remove uploaded attachments from email***

By enabling this option every attachment which was successfully uploaded to MetaDefender Managed File Transfer will be removed from the email. If uploading an attachment fails the removal will be skipped.

Blocked files

Blocked files will be removed regardless this setting if the action for blocked contents is to *Delete blocked contents*.

***Include scan result***

By enabling this option, Email Gateway Security will upload the scan results to Managed File Transfer besides the attachment as metadata. As a result Managed File Transfer will know the verdict of the scan and can make the file available immediately.

***Create subfolders in MetaDefender Managed File Transfer***

When this option is enabled, a subdirectory is created for each attachment category (e.g. password protected attachments, sanitized attachments, original copy of sanitized attachments, etc.) in MetaDefender Managed File Transfer.

The attachment categories are the same as the upload options under the Upload attachments tab in the security rule.

***Account impersonation options***

Impersonation

Based on the email addresses, the files will be uploaded to the recipients' own MFT accounts (when the account exists on the MetaDefender Managed File Transfer at all). This feature requires appropriate permissions (impersonation) on MetaDefender Managed File Transfer.

Default account

The account on MetaDefender Managed File Transfer that is assigned to the API key specified in the MetaDefender Managed File Transfer server profile (see [Configuration/Server profiles](/configuration/server-profiles)) set for the Email Gateway Security rule that matched the email.

Upload to default account for each email address for each email

When there are multiple recipient email addresses for an email that do not have the corresponding account on MetaDefender Managed File Transfer, or *Always upload to default account* is set; then the files will be uploaded to the default account for each email address for each email.

A separate subdirectory is created for subsequent email addresses named as counter values (1, 2, ...).

Guest account

A temporary account created on MetaDefender Managed File Transfer. These accounts can be accessed using a PIN.

The PIN length and the account expiry window can be configured in the Upload attachments tab or the security rule.

The PIN can be made available to the recipients using the `mft_name` or `mft_user` disclaimer variables. For details see [Disclaimer variables](/configuration/disclaimers#disclaimer-variables).

This PIN then needs to be used on the MetaDefender Managed File Transfer login page for Guest accounts. When the upload might end up in creating a guest account, then the recipients' attention needs to be called to this fact and the way how they can authenticate on MetaDefender Managed File Transfer.

Separate guest account for each email address for each email

For each email and for each recipient email addresses a dedicated guest account will be created on MetaDefender Managed File Transfer.

This might result a huge number of guest accounts created on MetaDefender Managed File Transfer.

[Disclaimer variables](/configuration/disclaimers#disclaimer-variables)

| Option | Details |
| --- | --- |
| Impersonate when possible, otherwise upload to default account | For accounts existing on the MetaDefender Managed File Transfer with the recipients' email addresses, the attachments will be uploaded to the appropriate MetaDefender Managed File Transfer accounts. In other cases the attachments will be uploaded to the default account. |
| Impersonate when possible, otherwise upload to guest account | For accounts existing on the MetaDefender Managed File Transfer with the recipients' email addresses, the attachments will be uploaded to the appropriate MetaDefender Managed File Transfer accounts.  In other cases the attachments will be uploaded to a dedicated guest account for each email address. |
| Impersonate when possible, otherwise skip upload | For accounts existing on the MetaDefender Managed File Transfer with the recipients' email addresses, the attachments will be uploaded to the appropriate MetaDefender Managed File Transfer accounts.  In other cases the attachments won't be uploaded, but delivered with the email normally. |
| Always upload to guest account | Attachments will be uploaded to a separate guest account for each email address. |
| Always upload to default account | Attachments will be uploaded to the default account. |

Example: Impersonate when possible, otherwise upload to default account

Impersonation works for the email address `one@local` but the address `two@local` will fall back to the default account `admin`.

#### Advanced

**Signed email settings**

These settings allow you to override the default behavior when handling signed and/or encrypted emails (S/MIME, PGP). By default, Email Gateway Security will not modify (add disclaimers, sanitize etc.) signed email to ensure that the email signature remains intact. By disabling the option *Do not modify S/MIME and PGP signed emails*, any signed emails will be modified and potentially render the signature invalid.

**Additional recipients**

This feature allows you to add additional recipients to every email processed by this security rule. Any recipients added in the list will receive a BCC copy of all emails processed.

**Rescan notifications**

When this feature is enabled the configured notifications are sent again if the email is kept quarantined after a _[_*full rescan*](%5Bhttps://www.opswat.com/docs/mdemail/operating/quarantine-reports#full-rescan-email) or](https://www.opswat.com/docs/mdemail/operating/quarantine-reports#full-rescan-email)or) [*anti-malware rescan*](https://www.opswat.com/docs/mdemail/operating/quarantine-reports#anti-malware-rescan-email).

**SMTP sender or recipient rewriting**

With this configuration it is supported to replace the *domain part* of the email addresses in the *MAIL FROM* and/or the *RCPT TO* SMTP commands to the configured value(s) during the SMTP submission to the SMTP relay configured for the rule.

Email addresses in email headers

To rewrite the email headers in the `From`, `To`, `Cc`, etc. email headers accordingly, enable the *Rewrite email headers option*.

When this option is off, email headers are kept unchanged. This means that the final recipient will see the original values of these headers.

SMTP rewriting logs

SMTP rewriting events are logged to the product log on INFO level.

Also, the *Processing history* of the *Email details* show an entry for the SMTP rewriting. For details see [Email details](/operating/email-history#email-details).

**Group disclaimer settings**

This options allows grouping of any disclaimers into a section (above or below email body content). This provides a less intrusive way of displaying information in multiple disclaimers for the recipient. An additional footer disclaimer can also be added to each email processed by the security rule.

**Override settings**

The override settings policy define certain exceptions from the default behavior for SMTP relays & MetaDefender Core scanning.

Retry

Email Gateway Security can be configured to retry to process emails. If an option is set to *Retry*, *Bypass if all retry fail* or *Quarantine if all retry fail*, then the retry mechanism under **Settings > General / Email** is applied.

For details see [Configuration/Settings](/configuration/settings).

The decision tree for the retry mechanism under *Override SMTP results*:

The decision tree for the retry mechanism under *Override error handling behavior*:

Risk of potentially harmful content

If *Bypass on first failure* or *Bypass if all retry fail* is configured for certain settings, and the email gets bypassed finally, then the original, potentially harmful email is delivered.

The recipient may be notified about the fact of bypassing. To do so set the *Bypass email disclaimer*. For details see [Configuration/Disclaimers](/configuration/disclaimers).

Risk of reverse NDR attack

When *Retry and send NDR on failure* or *Fail immediately and send NDR* is configured for *Override SMTP results / SMTP permanent failure* and a non-delivery report email (NDR) is sent finally, there is a risk that Email Gateway Security will become the sender of [backscatters](https://en.wikipedia.org/wiki/Backscatter_(email)) or will be abused for reverse NDR attacks (when attackers intentionally cause huge amounts of backscatters to the victim to overload the victim's infrastructure). Victims of backscatters and reverse NDR attacks may have the sender server's IP listed by blocklisting services.

***Anti-Spam processing failed***

Email Gateway Security has a special option in case when the Anti-Spam processing fails. Setting the option to *Ignore* the anti-spam result is ignored and the email is processed as if the anti-spam check would have found the email clean.
