<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-reset-password-for-users -->

# How to reset password for users?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

[Resetting a User’s Password](/docs/mdcore/v5.22.1/configuration/password-recovery) User Management in MetaDefender Core requires an active SMTP Server Configuration upfront, to provide a way to inform the users by Email of their Credentials Change, so they can acknowledge and act immediately, changing their temporary password:

The user’s Email Address should also be configured correctly for the SMTP Server to send the email to the recipient successfully.

This represents an enforcement action to prevent security breaches like someone impersonating the actual user and taking advantage of their account.

[SMTP Server can be configured](/docs/mdcore/v5.22.1/configuration/email-configuration) accessing **Settings** > **Network** > **Email Server** > **Add Server**:

For cases when MetaDefender Core is deployed in an isolated environment and SMTP cannot be configured, the alternative way to bypass this is by removing the User and Re-Adding it with a new password.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
