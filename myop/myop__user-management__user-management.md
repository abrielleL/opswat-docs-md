<!-- source: https://www.opswat.com/docs/myop/user-management/user-management -->

# User Management

The **User Management** page (accessible from the left navigation menu) offers administrators seamless user provisioning and management to the My OPSWAT On-premises console.

Here is what you can do:

- Users & Groups: Manage users and groups who can access to the My OPSWAT On-premises console.
- Roles: Manage roles assigned to users and groups.
- User Directories: Manage user directories from Local, Active Directory, and Single Sign-On.

## [User Roles](/docs/myop/user-management/user-management#user-roles)

By default, there are 2 pre-defined roles are available

- Administrator: a user with this role has full access to all features
- View-Only: a user with this role only views and exports data.

Administrators can add roles with specific permissions to only certain My OPSWAT features. Please refer to [Add a new user role](/docs/myop/user-management/add-a-new-role) for more information.

## [Users & Groups](/docs/myop/user-management/user-management#users--groups)

In the **Users and Groups** tab of the **User Management** page from the left navigation menu, administrator users can

- Add or remove users and groups
- Reset PIN and password for individual users
- Update roles for users and groups

Each user belongs to a user directory in User Directories tab. There are 3 types of users/groups:

- **Local Users:** individual users invited on the My OPSWAT On-premises console. The administrator user created in the configuration wizard is designated as the root account and cannot be modified
- **Active Directory Users/Groups:** Individual users/groups added on an Active Directory server. Note that users belong to a group won't be listed in Users & Groups. However, you can track who signed in to the console via the Events and History trail.
- **Single Sign-on (SSO) groups:** mapping groups with an Identify Provider. Note that users sign in through Single Sign-On service won't be listed in Users & Groups. However, you can track who signed in to the console via the Events and History trail.

The **Actions** drop-down offers various actions on selected users/groups.

- First, select users/groups by clicking checkboxes in user/groups entries.
- Then select an action inside the Actions dropdown

**Available actions:**

- **Reset Password:** reset the selected users' password. The system will generate a temporary password for each selected user. The user will be prompted to change their password at their next login after using the temporary password.

- **Update Role:** update the designated role of the selected users. In the pop-up dialog, select the new role from the drop-down and then click **Update** to confirm the selection.

- **Delete**: remove selected users/groups. In the pop-up dialog, click Delete again to confirm the selection.

- **Reset PIN:** reset the selected user's PIN, such as if they have forgotten it. The user will be assigned a temporary PIN that should be changed as soon as possible.

## [User Directories](/docs/myop/user-management/user-management#user-directories)

In the **User Directories** tab of the **User Management** page from the left navigation menu, administrator users can manage user directories.

There are 3 types of user directories:

- Local: directly create new user accounts within the system.
- Active Directory: integrate with your organization's Active Directory for user management.
- Single Sign-On (SSO): seamlessly integrate with your organization's Identity Provider using the SAML 2.0 protocol to utilize SSO for a simplified and secure authentication process.

You can perform some action on each individual user directory by clicking on the ellipsis ("...") menu located at the end of the user directory entry to access the action menu. You can then:

- Click **Edit** to change the user directory's settings. After making changes, click **Save** to save all changes.

The descriptions for the available settings are located in [Add a new user directory](/docs/myop/user-management/add-a-new-user-directory).

- Click **Delete** to delete the user directory. Review the user directory you want to delete and click **Delete** button in the pop-up dialog to confirm your choices.

Known Limitations: Deleting local user directories

Please note that there is a known issue where users cannot log in if all local user directories have been deleted.

Please make sure that the My OPSWAT On-premises server possesses at least one local user directory.
