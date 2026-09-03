<!-- source: https://www.opswat.com/docs/my/troubleshooting/account-creation-confirmation-email-troubleshooting -->

# Why don’t I receive a Confirmation Email after creating My OPSWAT Portal account?

### Issue

When creating a new account on the My OPSWAT Portal, users do not receive the expected confirmation email.

### Environment

- OPSWAT Portal: [https://my.opswat.com/](https://my.opswat.com/)
- Any corporate or internal email domains

### Cause

There are two primary reasons why confirmation emails may not be delivered:

1. **Internal-Only Email Domain:** Your email address uses an internal company domain that is not configured to receive messages from external networks.
2. **Corporate Email Filtering:** Your organization’s email security policies are blocking incoming messages from OPSWAT’s mail servers.

### Resolution

#### 1. Internal-Only Email Domain

If your email address is hosted solely within your organization’s internal network, contact OPSWAT Support and **submit a Manual Activation Request of your account**. Provide your name and the email address used for creating the account.

#### 2. Corporate Email Filtering

If your company blocks external inbound email traffic:

- **Whitelist OPSWAT’s Email Domain**: Ensure that your IT or email administrator allows incoming mail from the following domain: **asend.opswat.com**
- **Verify Spam/Quarantine Folders:** Ask your administrator to check any email security appliances or quarantine systems for messages from OPSWAT.

If further assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
