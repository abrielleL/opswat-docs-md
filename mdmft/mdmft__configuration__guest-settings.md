<!-- source: https://www.opswat.com/docs/mdmft/configuration/guest-settings -->

# Guest Settings

Summarize Page    Connect to Cursor Connect to VS Code

To edit Guest user settings go to "Settings" -> "Global Settings" -> "Guests" tab.

### [Disable Guest Creation](/docs/mdmft/configuration/guest-settings#disable-guest-creation)

Disables the guest creation option for all users, including administrators. The "Users" → "Guests" page will disappear from the left menu for all users.

This is useful when temporary accounts and file sharing with external people are not desired or when the Single Sign-On enforced authentication is active.

When active, all other options are inactivated.

Warning

Existing guests will not be able to log in after this option is enabled.

### [Disable Guest Creation by Users](/docs/mdmft/configuration/guest-settings#disable-guest-creation-by-users)

Prevents users from creating guest accounts while still allowing administrators to do so. Users will not see the "Users" → "Guests" page on the left menu.

This is useful when temporary accounts and external file sharing is not desirable.

### [Disable Editing Guest Expiration Date by Users](/docs/mdmft/configuration/guest-settings#disable-editing-guest-expiration-date-by-users)

Controls the expiration time of guest accounts created by users. For example, this configuration ensures that users cannot create guest accounts valid for more than a day.

### [Default Guest Expiration Period](/docs/mdmft/configuration/guest-settings#default-guest-expiration-period)

Sets the default period after which a guest account is permanently removed from the system.

### [Guest ID Length](/docs/mdmft/configuration/guest-settings#guest-id-length)

You can configure the ID length to be between 12 and 255 characters. The default length is 12.

### [Enable Restriction of Maximum Guest User Accounts](/docs/mdmft/configuration/guest-settings#enable-restriction-of-maximum-guest-user-accounts)

Restricts the maximum number of guest user accounts per user. Administrators can set this limit using the "Maximum Number of Guest User Accounts Allowed" input.
