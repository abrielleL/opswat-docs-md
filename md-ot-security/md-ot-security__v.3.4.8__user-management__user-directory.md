<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/user-management/user-directory -->

# User Directory

The User Directory feature in MetaDefender OT Security provides a user interface (UI) to configure and manage connections to an LDAP or Active Directory (AD) server for user authentication and authorization.

To configure the User Directory in MetaDefender OT Security, follow these steps:

1. Sign in to the Web Management Console.
2. Navigate to **User Management** → **User Directories** in the Web Management interface.
3. Click **Add New** and input the name.
4. Enter the required LDAP server details, such as:

   - **Host**: The LDAP server address (e.g., the IP address or hostname of your LDAP server, such as 192.168.1.x or [ldap.mdots.com](http://ldap.mdots.com/)).
   - **Port**: The port of the LDAP server (e.g., 636, as shown in the UI, which is the default for LDAPS when using SSL).
   - **Encryption**: Select the encryption method from the dropdown: None, StartTLS, or SSL (e.g., SSL is selected in the UI, recommended for security to encrypt communication and prevent credentials from being sent in clear text).
   - **Trust Encryption Certificate from the LDAP Server**: Check this box (as shown in the UI) to trust the LDAP server’s certificate, especially if it uses a self-signed or untrusted certificate.
   - **Apply to All Below Servers**: Check this box if you have multiple LDAP servers and want to apply the same certificate trust settings to all of them (as shown in the UI).
   - **Anonymous Bind**: Leave this unchecked (as shown in the UI) to require credentials for binding. If checked, MetaDefender will attempt an anonymous bind, which is less secure.
   - **Bind User Name and Password**: Credentials for an account with search privileges in the LDAP tree (e.g., cn=admin,dc=mdots,dc=com, as shown in the UI, with the corresponding password).
   - **User Base DN**: The starting point for user searches in the directory tree (e.g., ou=people,dc=mdots,dc=com, as shown in the UI).
   - **Group Base DN**: Optionally, specify the starting point for group searches (e.g., the UI shows this field as empty; you might set it to ou=groups,dc=mdots,dc=com if needed for role mapping).
   - **User Object Class**: The LDAP object class that defines user entries (e.g., inetOrgPerson, as shown in the UI under LDAP User Schema Settings).
   - **User Account Attribute**: The attribute that uniquely identifies a user account (e.g., cn, as shown in the UI under LDAP User Schema Settings). This is the attribute MetaDefender uses to match usernames during authentication.
5. Test the connection to ensure the settings are correct, then save the configuration.
