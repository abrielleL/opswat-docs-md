<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/password-recovery -->

# Password Recovery

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Prerequisites](/docs/mdcore/v5.22.1/configuration/password-recovery#prerequisites)

- Password Recovery **only supports local users**, not applicable to Active Directory / LDAP users where all their credential settings should be managed on Domain controller / LDAP server.
- The feature authenticates local users via email to reset their own password (assuming user was registered with a valid email on MetaDefender Core, if not then user should update their email properly on User Management page), and therefore it is mandatory for MetaDefender Core's administrators to follow steps at [Email Configuration](/docs/mdcore/v5.22.1/configuration/email-configuration) and ensure all SMTP configurations set properly beforehand.

  - Otherwise, expecting users to hit following warning message when trying to reset their password: `"We are sorry, confirmation email cannot be sent. Please contact your administrator to check email configurations."`

## [How This Feature Works](/docs/mdcore/v5.22.1/configuration/password-recovery#how-this-feature-works)

Just in case MetaDefender Core user credentials are lost or forgotten, basically any local user (not AD / LDAP) will be supported to reset their password by either one of two methods:

- **Forgot password (active):** Any local user can choose to reset their own password.
- **Reset password by administrators (passive):** Any local user's password can be reset by administrators.

Both methods require authentication via email, and force the affected user to change their password at the first login time for security reason.

### [Forgot Password](/docs/mdcore/v5.22.1/configuration/password-recovery#forgot-password)

Any local user registered with email on MetaDefender Core should be able to reset their own password by clicking on **Forgot password?** link on login page.

You will be redirected to Recover Password page.

An email with a token will be sent to user's registered email entitled `MetaDefender Core Password Reset`

Warning

If that user does not take any action, the token will be expired in 15 minutes

Input the token from the mail and press `Reset password` in MetaDefender Core management console

Following steps in email will be redirected to MetaDefender Core management console where user will be allowed to create a new password:

You will be automatically redirected to MetaDefender Core dashboard after resetting password successfully.

### [Reset Password By Administrators](/docs/mdcore/v5.22.1/configuration/password-recovery#reset-password-by-administrators)

As an administrator, you are allowed to reset password of any local user on MetaDefender Core, it could be either other local user (admin / non-admin) or even oneself.

Go to "User Management" → under "Users And Groups", mouse over on user to choose "Reset Password" option

**Admin to RESET PASSWORD**

Then administrator must create a new password by clicking **Generate** link or typing any text in the textbox.

Click RESET PASSWORD button once done.

An email titled "MetaDefender Core Password Reset" will be sent to user's email. Please check the inbox to collect a temporary password.

When the impacted user tries to log into MetaDefender management console afterwards with the provided temporary password in the email at the first time, that user will be redirected to page where they are required to change their password.

Once successfully changed the password, the user will be automatically redirected to the MetaDefender dashboard.
