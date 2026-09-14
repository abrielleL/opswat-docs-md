<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/ad-fs-specific-configuration -->

# AD FS Specific Configuration

To properly access MDSS, the following AD **Security Groups** are required:

- **SsoAdministrator** - the equivalent of local MetaDefender Storage Security administrator role
- **SsoReadOnlyAdministrator** - the equivalent of local MetaDefender Storage Security read-only role

It is also necessary for the AD user to have an **email address** set up, so that it is set as the MetaDefender Storage Security's user email

To set up AD FS SSO for MDSS, follow these steps:

1. Within the AD FS settings, navigate to the "**Scope Descriptions**" directory and click "**Add Scope Description**"

2. Create a scope with the name "**offline_access**"

3. Navigate to the "**Application groups**" directory and click "**Add Application Group**"

4. Give your application any name you like and for the template, select "**Server application accessing a web API**"

5. Give the server app a name, save the generated **Client Identifier** somewhere, and as the "**Redirect URI**", write the the base URL of the MDSS deployment, followed by the "**/callback**" suffix.

6. Select "**Generate a shared secret**" and store the secret somewhere

7. For the "**Identifier**" field, put the previously generated **Client Identifier** that you saved

8. For the access **control policy**, select "**Permit everyone**"

9. For the **permitted scopes**, select the following from the list: **allatclaims**, **email**, **offline_access**, **openid**, **profile**

10. After saving the created application group, select it and click on **Properties**

11. Select the configured **Web API** and click on **Edit**

12. Go to "**Issuance Transform Rules**" and click "**Add Rule**"

13. Select "**Send LDAP Attributes as Claims**" as the **Claim Rule Template**

14. Give the rule a name, select Active Directory as the attribute store and configure the following:

- **E-Mail Address** as **E-mail Address**
- **Is-Member-Of-DL** as **" groups*"***
- **Display-Name** as ***"user_display_name"***
