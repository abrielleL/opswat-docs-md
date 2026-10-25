<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/email-tags -->

# Email tags

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdemail/6.4.2/operating/email-tags#overview)

Email Gateway Security supports adding markers called ***tags*** to emails, to provide a user-defined notation for emails based on different processing properties of a specific email.

Per rule tags

Tags can be configured differently for each security rule.

## [Enable tagging](/docs/mdemail/6.4.2/operating/email-tags#enable-tagging)

Tagging can be enabled for several actions or statuses in security rules. For example here the *clean* tag is added to emails that were allowed:

For further details about enabling and configuring tags see [Policy](/docs/mdemail/6.4.2/configuration/policy).

## [Displaying tags](/docs/mdemail/6.4.2/operating/email-tags#displaying-tags)

All assigned tags of an email are displayed in **Audit > Email History** / Email details.

Based on the settings, certain tags may also show up in the front of the delivered email’s subject, in square brackets.

No tags in subjects in Email History

The tags are not applied in the subjects displayed in **Audit > Email History** and **Quarantine**.

## [Filtering](/docs/mdemail/6.4.2/operating/email-tags#filtering)

Emails can be filtered in **Audit > Email History** and in **Quarantine** by the tags applied.

For details see [Operating/Email History](/docs/mdemail/6.4.2/operating/email-history).
