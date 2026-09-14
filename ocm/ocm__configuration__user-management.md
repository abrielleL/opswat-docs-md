<!-- source: https://www.opswat.com/docs/ocm/configuration/user-management -->

# User Management

Active Directory is a directory service developed to manage permissions and access to network resources. OPSWAT Central Management offers integration with Active Directory service along with a suite of accompanying user management features.

Administrators can manage access to the OPSWAT Central Management console for users registered in an existing Active Directory in the current network or create new access credentials in a locally-stored User Directory. Administrators can also define user roles to control the access level granted to different users and configure account security measures.

## [Users and Groups](/docs/ocm/configuration/user-management#users-and-groups)

In the Users and Groups menu, users can add or remove user and group (Active Directories only), reset PIN and password for individual users, and perform role reassignment.

To access the **Users and Groups** menu, navigate to **User Management** sidebar and select the corresponding tab.

There are 3 categories of user types:

- **Local:** Individual users originally created in the OPSWAT Central Management console. The administrator user created in the configuration wizard is designated the master account and cannot be modified (please refer to [Configuration wizard](/docs/ocm/quick-start/configuration-wizard) for more information).
- **Active Directory User:** Individual users stored on an Active Directory server.
- **Active Directory Group:** Groups (as defined by the Active Directory service) of one or more users stored on an Active Directory server.

The **Actions** drop-down menu contains various user management features. Click the checkboxes in the user entries that require modifications. Select **Reset Pin** or **Reset Password** and then select **Reset** in the pop-up dialog to reset the selected users' PIN or password to a randomly generated one. For password, the user will be prompted to change their password at their next login after using the temporary password.

Warning

The reset password function is disabled for active directory group.

Select **Update Role** to change the designated role of the selected users. In the pop-up dialog, select the new role from the drop-down menu and then click **Update** to confirm the selection.

Info

For Active Directory Group, the role assigned to the group apply to all member users. If a user belongs to multiple groups with different roles (for example. both Administrator and Read-Only), the role with the higher privilege applies (Administrator in this case).

Warning

If a user with Administrator role demotes their roles to Read-Only, they will be immediately logged out of the session.

Select **Delete** to remove an existing users. In the pop-up dialog, select **Delete** again to confirm the selection.

Info

The currently logged-in user cannot delete themselves, even if they have administrative access to user management.

Warning

An action performed against a user group applies to all member users.

## [Roles](/docs/ocm/configuration/user-management#roles)

Roles define the level of access a given user or user group has in OPSWAT Central Management.

There are currently 3 roles available in OPSWAT Central Management:

- **Administrator:** Have full access to the management console. Can edit settings and perform all functions within OPSWAT Central Management.
- **Operator:** Have limited access to the management console. For the product management feature, users with the Operator role can only manage the product groups (and by extension, product sets and product instances) that they are assigned to. They also do not have edit permission for the user management and OPSWAT Central Management license management features. Aside from the aforementioned restrictions, these users have the same capability as users with the Administrator role.
- **Read-Only:** Only have viewing access. Cannot interact with settings nor perform any functions in OPSWAT Central Management.

The **Roles** tab is located in the **User Management** menu and shows the number of users assigned to each role.

## [User Directories](/docs/ocm/configuration/user-management#user-directories)

The User Directories menu allow users to add or remove user directories, change which user directories are currently enabled, and edit their settings.

The **User Directories** menu is a tab located in the **User Management** menu.

User Directories define the locations where user data is stored. There are two type of user directories.

- **Local:** User data is located locally within OPSWAT Central Management's database.
- **Active Directory:** User data is stored on an Active Directory service.

The **RELEASE LOCKOUT** button resets the lockout status of all users. Lockout refers to the security measure that prevents users from logging in after exceeding the maximum number of allowable failed login attempts.

To enable or disable user directories, click on the **ENABLE** slider.

To delete user directories, click the checkboxes on their entries and select **Delete** in the **ACTIONS** drop-down menu.

Warning

All user belong to deleted AD will also be deleted

Warning

A user directory with at least one currently logged in user cannot be disabled or deleted.

To edit user directories, click the checkboxes on their entries and select **Edit** from the gear icon. The edit interface is similar to the **ADD NEW USER DIRECTORY** menu. Please refer to [Adding User Directory](/docs/ocm/configuration/adding-user-directory) for more information. Modify the settings as needed and select **UPDATE** to confirm the changes.
