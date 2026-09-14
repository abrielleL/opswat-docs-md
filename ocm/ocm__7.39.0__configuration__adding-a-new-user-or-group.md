<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/adding-a-new-user-or-group -->

# Adding a new user or group

The following guideline describes how to add a new user or group in OPSWAT Central Management.

1. In the **USERS AND GROUPS** tab of the **User Management** menu, select **ADD NEW USER/GROUP**.

2. In the **Add New User/Group** page, select the user directory the new user or group should belong to.

The next steps differ depending on which directory type the selected user directory belongs to. **Local Directory:**

1. If the selected user directory is of the local type, fill in the required information and select the roles to be assigned to the new user. Select **ADD** to confirm.

- **First Name, Last Name:** The user's identity

- **Email:** The user's email, also used as part of their login credentials.

- **Assign To Roles:** Assign the user to either Administrator, Operator, or Read-Only role.

2. The new user will be assigned a temporary password and will be asked to change it at their first login.

**Active Directory:**

1. If the selected user directory is of the active directory type, fill in the two fields **User Directory username** (in the format of **<Active Directory Domain Name><Username>**) and **User Directory password** in the **User Directory Information** section

Then select **TEST CONNECTION** to check the connection to the Active Directory and enable the Account Information section.

2. After a successful connection test, select the account type and either the user or user group to be added from the user directory in the **Find Account Name** field. Please use the sAMAccountName value of the user or user group for this field. Select the role to assign to the new user or user group. Select **ADD** to confirm the selection.

Warning

If the selected user directory contains multiple active directories, the find function will return only results from the first active directory that the matches are found in.

Wildcard is not supported. The maximum amount of results returned is 1000.

For both type of user directories, until the new user logs in, their status will be set as **Pending.**

Info

User groups can only be created in user directories of Active Directory type.

Info

Added users that do not belong to the default LOCAL user directory have the login username format of <User Directory>/<Email>. For example, a user with email [abc@email.com](mailto:abc@email.com) belonging to the NEWDIR user directory has the username NEWDIR/abc@email.com.
