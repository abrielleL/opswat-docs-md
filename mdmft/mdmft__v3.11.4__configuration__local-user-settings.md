<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/local-user-settings -->

# Local User Settings

Summarize Page    Connect to Cursor Connect to VS Code
###

### [Force Password Reset on Local User Creation](/docs/mdmft/v3.11.4/configuration/local-user-settings#force-password-reset-on-local-user-creation)

Enables the "Force password reset on next logon" option during local user creation. Administrators can override this global configuration.

### [Limit Login Attempts for Local Users](/docs/mdmft/v3.11.4/configuration/local-user-settings#limit-login-attempts-for-local-users)

Enables the user lockout feature for local users. Locks out local users if they fail to authenticate within the maximum allowed login attempts. The lockout duration is set by the "Lock account for (minutes)" configuration field.

| Setting | Description |
| --- | --- |
| Login attempts allowed before the account is locked | Number of failed login attempts allowed before the account is locked |
| Lock account for (minutes) | Duration for which the account is locked if the number of failed login attempts exceeds the predefined limit |
| Reset failed login attempts counter after (minutes) | Resets the failed login attempts counter after the specified duration; 0 - Counter is never reset; X - Counter resets after X minutes |
