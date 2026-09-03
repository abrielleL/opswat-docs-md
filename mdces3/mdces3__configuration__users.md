<!-- source: https://www.opswat.com/docs/mdces3/configuration/users -->

# Users

Summarize Page

The **Users** interface allows administrators to manage platform users efficiently. This section explains how to view, add, modify, and delete user accounts.

## [Users List Features](/docs/mdces3/configuration/users#users-list-features)

- **Search Bar**: Allows users to find specific users by name or email address.
- **Filters**:

  - **Type**: Filter by role (e.g., System Administrator, Security Auditor).
- **Columns**:

  - **User Name**: User display name.
  - **Email Address**: User's email address.
  - **Role**: Assigned user role (for details, see [Available Roles](/docs/mdces3/configuration/users#available-roles))
  - **Buttons:**

    - **Edit:** Change user role.
    - **Delete:** Delete the user.

## [Adding a New User](/docs/mdces3/configuration/users#adding-a-new-user)

Click the **"Add new user"** button in the top-right corner.

### [Add user dialog](/docs/mdces3/configuration/users#add-user-dialog)

- **User Display name**: Enter the user’s display name.
- **Email Address :** Enter the user’s email address associated with their My OPSWAT account.
- **Role**: Select a role from the dropdown (for details, see [Available Roles](/docs/mdces3/configuration/users#available-roles)).

My OPSWAT account required

Only users with an **active My OPSWAT account** can be added. To register a new user in My OPSWAT, go to <https://my.opswat.com>

## [Available Roles](/docs/mdces3/configuration/users#available-roles)

The following roles are available in **MetaDefender Cloud Email Security ™**:

| Role | Description |
| --- | --- |
| **System Administrator** | Has full access to all features and settings, including the ability to configure tenants. |
| **Administrator** | Has access to all features except tenant configuration. |
| **Security Auditor** | Has full access to Events, Quarantine & Audit only. |
| **Read-Only User** | Has read-only access to all features. |
