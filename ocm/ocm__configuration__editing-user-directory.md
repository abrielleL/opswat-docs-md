<!-- source: https://www.opswat.com/docs/ocm/configuration/editing-user-directory -->

# Editing User Directory

The following guideline describes how to edit a directory in OPSWAT Central Management.

1. In the **User Directories** menu, select **Edit** in Settings icon

2. In the edit User Directory screen differs between user directory type.

a. For **Local** type user directory, modify the original settings as required and select **UPDATE** to finalize the edit user directory.

- Name: Change name a user directory.
- **Enable this User directory:** Click this checkbox to immediately enable/disable this directory.
- **Number of failed logins before lockout:** Number of allowed login attempts in 1 minute. Setting it to 0 allows unlimited failed logins.
- **Lockout time (minutes):** The length of the lockout period after a user reach maximum amount of failed logins. Setting it to 0 allows unlimited failed logins regardless of the number of failed logins specified.

b. For **Active Directory** type user directory, fill in the required information and select **TEST CONNECTION** to check connection to the Active Directory server. After the connection is verified, select **UPDATE** to finalize the edit user directory.

- **Server Host, Server Port:** The address of the Active Directory server.
- **Encryption:** The encryption type used by the Active Directory server (None, SSL, StartTLS)
- **User Base DN, Group Base DN:** The point where OPSWAT Central Management search for users and groups when adding new users and groups from Active Directories.
- **ADD NEW SERVER:** Add an additional Active Directory server entry.
