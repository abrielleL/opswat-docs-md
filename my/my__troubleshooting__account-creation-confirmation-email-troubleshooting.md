<!-- source: https://www.opswat.com/docs/my/troubleshooting/account-creation-confirmation-email-troubleshooting -->

# Why don't I receive a Confirmation Email or MFA verification code from My OPSWAT Portal?

### **Issue**

When creating a new account on the My OPSWAT Portal, or when using Email as a Multi-Factor Authentication (MFA) method, users do not receive the expected confirmation email or MFA verification code.

**Environment**

- OPSWAT Portal: [https://my.opswat.com/](https://my.opswat.com/) | [https://id.opswat.com/](https://id.opswat.com/) <<< NEW
- Any corporate or internal email domains

**Cause**

There are two primary reasons why these emails may not be delivered:

1. Internal-Only Email Domain — Your email address uses an internal company domain that is not configured to receive messages from external networks.
2. Corporate Email Filtering — Your organization's email security policies are blocking incoming messages from OPSWAT's mail servers.

Note on sender domains and infrastructure: OPSWAT sends account and authentication emails through two providers. It is expected and legitimate to see either of the following as the sender:
- @[opswat.com](http://opswat.com) — sent via SendGrid
- @[asend.opswat.com](http://asend.opswat.com) — sent via AWS Simple Email Service (SES)
Because emails are delivered through AWS SES, the message header may show a sender host such as [xxxxxxxxx.smtp-out.us-west-2.amazonses.com](http://xxxxxxxxx.smtp-out.us-west-2.amazonses.com). This is normal. AWS SES does not publish a fixed list of sender IP addresses, so allowlisting must be done by domain, not by IP.

**Resolution**

1. Internal-Only Email Domain

If your email address is hosted solely within your organization's internal network, contact OPSWAT Support and submit a Manual Activation Request for your account. Provide your name and the email address used to create the account.

2. Corporate Email Filtering

If your company blocks external inbound email traffic:

- Whitelist OPSWAT's email domains: Ensure your IT or email administrator allows incoming mail from both of the following domains:
  - - @[opswat.com](http://opswat.com) (SendGrid)
    - @[asend.opswat.com](http://asend.opswat.com) (AWS SES)
- Verify Spam/Quarantine folders: Ask your administrator to check any email security appliances or quarantine systems for messages from OPSWAT.

> If further assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/my/llms.txt)
