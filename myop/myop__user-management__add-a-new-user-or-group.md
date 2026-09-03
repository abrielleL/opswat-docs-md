<!-- source: https://www.opswat.com/docs/myop/user-management/add-a-new-user-or-group -->

# Add a new user or group

The **User Management** page > **Users & Groups** tab offers administrator users ability to grant access to users by adding **Local, Active Directory** or **Single Sign-on (SSO)** users/groups and also manage their users/groups. To grant access to users/groups, an administrator user clicks Add Users/Groups, then select a user/group type, **Local, Active Directory, or Single Sign-On (SSO)**, to open Add Users/Groups form. Depend on what type of users/groups, the administrator user needs to fill in different required information to complete.

#### [Local Users](/docs/myop/user-management/add-a-new-user-or-group#local-users)

You can follow the below steps to add local users

1. On The **User Management** page > **Users & Groups** tab, click **Add Users/Groups** button, select **Local** option
2. Select a local user directory from the **Directory Name** dropdown that new users belong to. You can add a new Local user directory in [User Directories](/docs/myop/user-management/add-a-new-user-directory) tab
3. Enter required information about a new user

- **Username/Email/First Name/Last Name:** The new user's information.
- **Assign Role:** The role assigned to the new user.

4. Click Add New User if you would like to add more users
5. *Confirm and Save:* Click Add button to add users. The system will generate a temporary password for each user that system added successfully. You need to copy the temporary password and consent our Terms of Service and Privacy Policy.

#### [Active Directory Users/Groups](/docs/myop/user-management/add-a-new-user-or-group#active-directory-usersgroups)

You can follow the below steps to add local users

1. On The **User Management** page > **Users & Groups** tab, click **Add Users/Groups** button, select A**ctive Directory** (AD) option
2. Select an AD user directory in **Directory Name** that new users/groups belong to. You can add a new AD user directory in [User Directories](/docs/myop/user-management/add-a-new-user-directory) tab
3. Select User or Group to add in **Type** dropdown
4. Use the search to find the users/groups on your configured Active Directory server.
5. Click Add button on the right of users/groups you would like to add then Select a role you want to assign to each user/group.

- If a user is not added to My OPSWAT On-premises but belongs to multiple added groups and those groups are nested, the system will assign a role of a deepest-level group to the user
- If a user is not added to My OPSWAT On-premises but belongs to multiple added groups and those groups are not nested, the system will assign a highest privilege role of groups to the user
- If a user is not added to My OPSWAT On-premises but belongs to multiple added groups and those groups are not complex (some are nested, and some are not), the system will assign a highest privilege role of deepest-level groups among those groups to the user

6. *Confirm and Save:* Click Add button to confirm your choice.

Changing sAMAccountName or userPricipalName in the active directory

Please note that if you change the sAMAccountName or userPrincipalName in the active directory, My OPSWAT On-premises won't be able to match the affected users/groups to the new sAMAccountName or userPrincipalName value. These users/groups won't be able to sign in to My OPSWAT On-premises until they are re-added.

#### [Single Sign-on (SSO) Groups](/docs/myop/user-management/add-a-new-user-or-group#single-sign-on-sso-groups)

By default, users assigned to My OPSWAT On-premises app in your Identity Provider (IdP) can sign in to My OPSWAT On-premises and is assigned with a role you configured for a user directory of that IdP. However, My OPSWAT On-premises offers you ability to assign a specific roles for your IdP groups when a user signs in by adding IdP groups to My OPSWAT On-premises. Here are steps to do so:

1. On The **User Management** page > **Users & Groups** tab, click **Add Users/Groups** button, select **Single Sign-On (SSO)** option
2. Select an user directory in **Directory Name** that new groups belong to. You can add a new IdP user directory in [Add a new user directory](/docs/myop/user-management/add-a-new-user-directory).
3. Enter the required information and click Add Group. Multiple groups can be added by repeating this action.

- **Idp Group:** a value your IdP set for the group attribute in a SAML assertion when a user signs in.
- **Group Name**: a displayed group name in My OPSWAT On-premises.
- **Group Role:** select a role you want to assign to users belong to the IdP group when they sign in.

  - If a user belongs to multiple added groups, the system will assign a highest privilege role to the user
  - If a user doesn't belong to any added groups or the group attribute doesn't exist in SAML assertion, the user will be assigned with a role configured in the user directory.

4. *Confirm and Save:* Click Add to confirm your choice.
