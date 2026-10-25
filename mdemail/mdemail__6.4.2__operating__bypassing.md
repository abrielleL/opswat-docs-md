<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/bypassing -->

# Bypassing

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdemail/6.4.2/operating/bypassing#overview)

To provide continuity of the email flow, Email Gateway Security can be

1. configured in the [Policy](/docs/mdemail/6.4.2/configuration/policy) to bypass processing in certain conditions;
2. instructed in the [Email History](/docs/mdemail/6.4.2/operating/email-history) to bypass in case of an emergency.

Risk of outbreak

If an email gets bypassed, then the original, potentially harmful email is delivered to the original recipient.

## [Policy-based bypass](/docs/mdemail/6.4.2/operating/bypassing#policy-based-bypass)

For configuration details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).

### [Disclaimers](/docs/mdemail/6.4.2/operating/bypassing#disclaimers)

Email Gateway Security should be configured to append a disclaimer to the email when it is bypassed. This disclaimer can inform the user about the fact that the email was bypassed and that it may contain harmful content.

For details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).

The disclaimer warning about bypassing rendered in an email:

### [Monitoring](/docs/mdemail/6.4.2/operating/bypassing#monitoring)

Bypassing exposes the email system and the whole organization to higher level of risk. Bypassing can be monitored on the **Dashboard** via the *Risk* and *Risk summary* widgets.

For details see [Dashboard](/docs/mdemail/6.4.2/operating/dashboard).

If the number of bypassed emails is raising, that indicates a potential problem in the system and the raised level of security risk.

## [Emergency bypass](/docs/mdemail/6.4.2/operating/bypassing#emergency-bypass)

In case of an emergency, emails can be bypassed using the *Bypass email processing* button or action in Email history. Bypassed emails are pushed immediately to the SMTP delivery queue, skipping scanning.

For details see the *Bypass processing emails* subsecion in [Bulk email operations](/docs/mdemail/6.4.2/operating/email-history#bulk-email-operations).
