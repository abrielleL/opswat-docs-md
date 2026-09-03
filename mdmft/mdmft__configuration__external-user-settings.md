<!-- source: https://www.opswat.com/docs/mdmft/configuration/external-user-settings -->

# External User Settings

Summarize Page    Connect to Cursor Connect to VS Code

### [Show My Files for External Users](/docs/mdmft/configuration/external-user-settings#show-my-files-for-external-users)

Controls whether External Users can access the **My Files** page. When enabled, External Users can see and browse their own files. When disabled, the My Files page is hidden and inaccessible for all External Users.

### [Allow External Users to Share Files](/docs/mdmft/configuration/external-user-settings#allow-external-users-to-share-files)

Controls whether External Users can share files with others. When enabled, External Users can share files as usual. When disabled, sharing is unavailable for External Users, but they can still access files that have been shared with them.

> **Note:** This option is only available when file sharing is globally enabled. If file sharing is turned off system-wide, this control is disabled. It can be enabled under **Settings / File Setting**

### [Disable External User Creation](/docs/mdmft/configuration/external-user-settings#disable-external-user-creation)

Disables external user creation for all users, including administrators. The "Users" → "External Users" page will disappear from the left menu for all users.

This is useful when temporary accounts and file sharing with external users are not desired.

The options below will be inactive when this option is active.

### [Disable External User Creation by Users](/docs/mdmft/configuration/external-user-settings#disable-external-user-creation-by-users)

Prevents users from creating external user accounts while still allowing administrators to do so. Users will not see the "Users" → "External Users" page on the left menu.

This is useful when temporary accounts and file sharing with external people is not desired.

### [Enforce Random Password for External Users](/docs/mdmft/configuration/external-user-settings#enforce-random-password-for-external-users)

When enabled, the system automatically generates a secure password for new external user accounts. The password is sent directly to the external user via email — account creators cannot set or view it.

If disabled (default), the account creator sets the password manually during account creation.

### [Disable External User Expiration](/docs/mdmft/configuration/external-user-settings#disable-external-user-expiration)

Controls whether external user accounts have an expiration date. When enabled, the creation dialog will no longer require an expiration date, and editing the expiration date for existing external users will be disabled.

### [Disable Editing External User Expiration Date by Users](/docs/mdmft/configuration/external-user-settings#disable-editing-external-user-expiration-date-by-users)

Controls the expiration time of external user accounts created by your users. For example, this configuration ensures that your users cannot create external user accounts valid for more than a day and cannot edit the expiration date for existing external user accounts.

### [Default External User Expiration Period](/docs/mdmft/configuration/external-user-settings#default-external-user-expiration-period)

Sets the default period after which a external user account is permanently removed from the system.

Warning

Existing guests will not be able to log in after this option is enabled.

### [Limit Login Attempts for External Users](/docs/mdmft/configuration/external-user-settings#limit-login-attempts-for-external-users)

Enables the user lockout feature for external users. Locks out external users if they fail to authenticate within the maximum amount of login attempts. The lockout duration is set by the "Lock account for (minutes)" configuration field.

| Setting | Description |
| --- | --- |
| Login attempts allowed before the account is locked | Number of failed login attempts allowed before the account is locked |
| Lock account for (minutes) | Duration for which the account is locked if the number of failed login attempts exceeds the predefined limit |
| Reset failed login attempts counter after (minutes) | Resets the failed login attempts counter after the specified duration; 0 - Counter is never reset; X - Counter resets after X minutes |

### [Enable Restriction of Maximum External User Accounts](/docs/mdmft/configuration/external-user-settings#enable-restriction-of-maximum-external-user-accounts)

Restrict the maximum number of external user accounts per user. Administrators can set this limit using the "Maximum Number of External User Accounts Allowed" input.
