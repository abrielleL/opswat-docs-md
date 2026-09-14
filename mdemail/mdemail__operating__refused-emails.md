<!-- source: https://www.opswat.com/docs/mdemail/operating/refused-emails -->

# Refused Emails

**Audit > Refused Emails** is the list of emails which were refused to be processed by Email Gateway Security on the inbound SMTP interface.

## [List verbosity](/docs/mdemail/operating/refused-emails#list-verbosity)

For details see [Operating/Email History](/docs/mdemail/operating/email-history).

## [Conditions of refusal](/docs/mdemail/operating/refused-emails#conditions-of-refusal)

An email gets refused if any of the following conditions occur:

| Condition | Result | Notes |
| --- | --- | --- |
| There is no security rule matching this email | No security rule | For details see [Policy/Fitering](/docs/mdemail/configuration/policy#fitering). |
| The sender email address is invalid | Invalid sender |  |
| The recipient email address is invalid | Invalid recipient |  |
| The sender IP address is blocked by anti-spam | Rejected by Anti-Spam policies | The email was scored as known or potential spam, and the *Known spam action* or *Potential spam action* property of the matching rule was set to *Reject.* For details see [Policy/Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| The sender IP address is blocked by anti-phishing | Rejected by Anti-Phishing policies | The email was scored as known or potential phishing, and the _Known phishing action_or *Potential phishing action* property of the matching rule was set to _Reject. _For details see [Policy/Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| The sender IP address or email address/domain is refused by the Blocklist | Blocklisted | The IP address and/or email address/domain is listed in the Blocklist. For details see [Settings/Blocklist](https://docs.opswat.com/mdemail/configuration/blocklist) |
