<!-- source: https://www.opswat.com/docs/ocm/configuration/adding-user-directory -->

# Adding User Directory

The following guideline describes how to add a new user directory in OPSWAT Central Management.

1. In the **User Directories** menu, select **ADD NEW USER DIRECTORY**.

2. In the **General Information** step, fill in the required information and select **USER DIRECTORY SETTINGS** to continue to the next step.

- **Name:** The name of new user directory.

- **User Directory Type:** The type of user directory, either **Local** or **Active Directory.**

- **Enable this User directory:** Click this checkbox to immediately enable this directory for use after creation.

3. The **USER DIRECTORY SETTINGS** step differs between user directory type.

   1. For **Local** type user directory, modify the default settings as required and select **ADD** to finalize the new directory's creation.

- **Number of failed logins before lockout:** Number of allowed login attempts in 1 minute. Setting it to 0 allows unlimited failed logins.

- **Lockout time (minutes):** The length of the lockout period after a user reach maximum amount of failed logins. Setting it to 0 allows unlimited failed logins regardless of the number of failed logins specified.

2. For **Active Directory** type user directory, fill in the required information and select **TEST CONNECTION** to check connection to the Active Directory server. After the connection is verified, select **ADD** to finalize the new user directory's creation.

- **Server Host, Server Port:** The address of the Active Directory server.

- **Encryption:** The encryption type used by the Active Directory server (None, SSL, StartTLS)

- **User Base DN, Group Base DN:** DN is short for Distinguished Name. The User/Group Base DN is the starting point OPSWAT Central Management uses to search for users and groups when adding new users and groups from Active Directories.

- **ADD NEW SERVER:** Add an additional Active Directory server entry.

Warning

Adding multiple Active Directory servers under the same user directory requires that all these Active Directories share the same credentials.

Info

Log-in of users under user-defined User Directory should follow [How do I log into OPSWAT Central Management](/docs/ocm/knowledgebase/how-do-i-log-into-opswat-central-management)

Info

Adding an encrypted user directory may require importing its certificate to OPSWAT Central Management's Java Runtime Environment keystore. Please follow the instructions at [Adding certificates to Java keystore](/docs/ocm/configuration/adding-certificates-to-java-keystore).
