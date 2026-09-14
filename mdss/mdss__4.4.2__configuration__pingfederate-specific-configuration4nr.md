<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr -->

# PingFederate Specific Configuration

To properly access MDSS, the following AD **Security Groups** are required:

- **SsoAdministrator** - the equivalent of local MetaDefender Storage Security administrator role
- **SsoReadOnlyAdministrator** - the equivalent of local MetaDefender Storage Security read-only role

It is also necessary for the AD user to have an **email address** set up, so that it is set as the MetaDefender Storage Security's user email

This documentation was tested on PingFederate 12.1 with an Active Directory datastore.

## [Create the scopes](/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr#create-the-scopes)

1. Go to System > OAuth Settings > Scope Management.
2. On the **Common Scopes** tab, add the following **Scope Values** along with a description. Click Add after entering each value and description.

   - openid
   - profile
   - email
   - offline_access
3. Skip the Exclusive Scopes tab.
4. On the Default Scope tab, enter a description for Default Scope. A description is required. If Default Scope Description is empty, PingFederate will log the following error: The requested scope is invalid, unknown, malformed, or exceeds that which the client is permitted to request.
5. Click Save.

## [Create a configuration on PingFederate](/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr#create-a-configuration-on-pingfederate)

### [Create the Access Token Manager](/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr#create-the-access-token-manager)

1. Go to Applications> OAuth > Access Token Management.
2. Click Create New Instance
3. On the Type tab:

- Instance Name: Enter an instance name. For example, MDSS Access Token Manager.
- Instance ID: Enter the instance ID. For example, MDSS.
- Type: Select JSON Web Tokens.
- Parent Instance: Leave the default, None.

4. On the Instance Configuration tab:

- Use Centralized Signing Key: Select the checkbox.Leaving this checkbox unselected causes PingFederate to expect "Active Signing Certificate Key ID" to be configured.
- JWS Algorithm: Select an algorithm. For example, RSA using SHA-256.
- At the bottom of the screen, click Show Advanced Fields.

  - JWT ID Claim Length: Add a number greater than zero (0). For example, 24. If you do not enter a value, the JTI claim is omitted in the access token.

5. Click Next.
6. On the Access Token Attribute Contract tab:

- In the Extend the Contract text box, add the following claims to be generated in the Ping access token. Click Add after entering each claim.

  - userName
- Subject Attribute Name: Select the userName claim to be used for auditing purposes.

7. Click Next twice to skip the Resource URIs and Access Control tabs.
8. Click Save.

### [Add the objectGUID Attribute](/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr#add-the-objectguid-attribute)

1. Go to System > Data Stores > Your Data Store > LDAP Configuration.
2. On the LDAP Configuration tab, click Advanced at the bottom.
3. On the LDAP Binary Attributes tab, in the Binary Attribute name field, use objectGUID and click Add.
4. Click Save

### [Create the OpenID Connect Policy.](/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr#create-the-openid-connect-policy)

1. Go to Applications> OAuth > OpenID Connect Policy Management.
2. Click Add Policy.
3. On the Manage Policy tab:

- Policy ID: Enter a policy ID. For example, OIDC.
- Name: Enter a policy name. For example, OIDC Policy.
- Access Token Manager: Select the access token manager that you previously created. MDSS Access Token Manager.
- Tick **Include User Info in ID Token**

4. Click Next.
5. On the Attribute Contract tab:

   - Click **Delete** to remove all the attributes except **sub**.
   - Add the following attributes:

     - Displayname
     - Email
     - Groups
     - upn
     - userName
6. Click Next, then click Next again to skip the Attributes Scope tab.
7. On the Attribute Sources & User Lookup tab, click Add Attribute Source.
8. After entering the information on each tab that follows, click Next to advance.

Data Store:

- Attribute Source ID: Enter an attribute source ID. For example, MDSSLDAP.
- Attribute Source Description: Enter a description. For example: MDSSLDAP
- Active Data Store: Select your Active Directory domain name from the drop-down.

LDAP Directory Search:

- Base DN: Enter your base DN to find your users and groups.
- Search Scope: Leave the default, Subtree.
- Attributes to return from search: Select <Show All Attributes> and select the following.Click Add Attribute.

  - displayName
  - memberOf
  - objectGUID
  - userPrincipalName
  - mail
- LDAP Binary Attribute Encoding Types:

  - ObjectGUID: Select Hex for the Attribute Encoding Type.
- LDAP Filter:

  - Filter: Enter a filter. For example, `userPrincipalName=${userName}`.

9. On the Summary page, click Done.
10. Click Next to advance, and on the Contract Fulfillment tab, map the Attribute Contract for the ID token:

| Attribute Contract | Source | Value |
| --- | --- | --- |
| displayname | MDSSLDAP | displayName |
| email | MDSSLDAP | mail |
| groups | MDSSLDAP | memberof |
| sub | MDSSLDAP | objectGUID |
| upn | MDSSLDAP | userPrincipalName |
| userName | No Mapping |  |

11. Click Next, then click Next again to skip the Insurance Criteria tab.
12. Click Save

### [Create the OAuth Client Application](/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr#create-the-oauth-client-application)

1. Go to Applications > OAuth > Clients.
2. Click Add Client.
3. On the Clients | Client page:

   1. Client ID: Enter the client ID. For example, MDSS
   2. Name: Enter a name. For example, MDSS.
   3. Client Authentication: Select Client Secret.
   - Client Secret: You can input your own client secret or generate a secret. After you leave this page, you cannot view the secret again. You only have the option to change the secret
   - Redirection URIs: write the the base URL of the MDSS deployment, followed by the "**/callback**" suffix.
   - Allowed Grant Types: Check Authorization Code, Implicit, Refresh Token, Client Credentials.
   - Default Access Token Manager: Select the access token manager you previously created. MDSS Access Token Manager.
   - OpenID Connect: For Policy, select the one you previously created. For example, the one used in this documentation is OIDC
4. Click Save.

## [Create the Password Grant Flow Configuration](/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr#create-the-password-grant-flow-configuration)

1. Create the Password Credential Validator.

   1. Go to System > Data & Credential Stores > Password Credential Validators.
   2. Click Create New Instance.
   3. In the Password Credential Validators | Create New Instance page, enter the information as follows for each tab, then click Next to advance.

      - On the Type tab:

        - Instance Name: Enter the instance name. For example, MDSS Validator.
        - Instance ID: Enter the instance ID. For example, MDSS.
        - Type: Select LDAP Username Password Credential Validator.
      - On the Instance Configuration tab:

        - LDAP Datastore: Select the data store you are using.
        - Search Base: Enter your base DN to find your users and groups.
        - Search Filter: Enter a filter. For example, userPrincipalName=${userName}.
        - Scope of Search: Select Subtree.
      - On the Extended Contract tab:

        - By default, the following are added:

          - DN
          - email
          - givenName
          - username
   4. Click Next then click Save.
2. Map the Validator in the Authorization Server Settings.

   1. Go to System > OAuth Settings > Authorization Server Settings.
   2. In Password Credentials Validator, select the one you previously created. For example, this documentation uses MDSS Validator.
   3. Click Save.
3. Create the Resource Owner Credentials Grant Mapping.

   1. Go to Authentication > OAuth > Resource Owner Credentials Mapping.
   2. In the Resource Owner Credentials Grant Mapping window:

      - Source Password Validator Instance: Select the one you previously created and click Add Mapping.
   3. In the Resource Owner Credentials Grant Mapping | Resource Owner Credentials Mapping page, click Next to skip the Attribute Sources & User Lookup tab.
   4. On the Contract Fulfillment tab:

      - For USER_KEY, select Password Credentials Validator, and for Value, select username.
   5. Click Next to skip the Insurance Criteria tab then click Save.
4. Create the Access Token Mapping - Map the Password Credentials Validator to the Access Token Manager.This mapping is needed for the Password Grant workflow. If the mapping does not exist, PingFederate logs the following error: There are no access token managers available for the selected client and authentication context.

   1. Go to Applications > Access Token Mappings.

      - Context: Select the one you previously created. For example, this documentation uses MDSS Validator.
      - Access Token Manager: Select the one previously created. For example, this documentation uses MDSS Access Token Manager.
   2. Click Add Mapping.
   3. Click Next to skip the Attribute Sources & User Lookup tab.
   4. On the Contract Fulfilment tab select userName
   5. Click Next to skip the Insurance Criteria tab then click Save.

## [Create the Authorization Code Flow Configuration](/docs/mdss/4.4.2/configuration/pingfederate-specific-configuration4nr#create-the-authorization-code-flow-configuration)

1. Create the IdP Adapter.

   1. Go to Authentication > Integration > IdP Adapters.
   2. Create Create New Instance.
   3. On the Type tab:

      - Instance Name: Enter a name, for example, HTML Form Auth Adapter.
      - Instance ID: Enter an ID, for example, HTMLFormAuthAdapter.
      - Type: Select HTML Form IdP Adapter.
      - Parent Instance: Select None.
   4. Click Next.
   5. On the IdP Adapter tab:Under Password Credential Validator Instance, click Add a new row to 'Credential Validators.' then select a validator (in this documentation, MDSS Validator is used), and click Update.
   6. Click Next.
   7. Click Next to skip the Extended Contract tab.
   8. On the Adapter Attributes tab:

      - Unique User Key Attribute: Select username and check Pseudonym.
   9. Click Next to skip the Adapter Contract Mapping tab then click Save.
2. Create IdP Adapter Grant Mapping.

   1. Go to Authentication > OAuth > IdP Adapter Grant Mapping.
   2. Source Adapter Instance: Select the Adapter instance you just created and click Add Mapping.
   3. On the Attribute Sources & User Lookup page, click Add Attribute Source.
   4. Enter the information as follows for each tab, then click Next to advance.

      - On the Data Store tab:

        - Attribute Source ID: Enter an ID with alphanumeric values.
        - Attribute Source Description. Enter a description.
        - Active Data Store: Select the active directory in use.
      - On the LDAP Directory Search tab:

        - Base DN: Enter your base DN to find your users and groups.
        - Search Scope: Use the default, Subtree.
        - Attributes to return from search: Select <Show All Attributes>, then, once loaded, from the attribute list, select userPrincipalName.
   5. Click Add Attribute then click Next.
   6. On the LDAP Filter tab:

      - Filter: Enter the filter. For example, `userPrincipalName=${userName}`.
   7. Click Next then click Save.
   8. In the IdP Adapter Grant Mapping | IdP Adapter Mapping page, finish creating the IdP Grant Mapping.On the Contract Fulfillment Lookup tab, use the following table.

| Contract | Source | Value |
| --- | --- | --- |
| USER_KEY | Select the source previously created. | Subject DN |
| USER_NAME | Select the source previously created. | userPrincipalName |

I. Click Next then click Save

3. Map the IdP Adapter to Access Token Manager.
4. Go to Applications > OAuth > Access Token Mappings.

   - Context: Select IdP Adapter:Adapter Name.
   - Access Token Manager: Select the access token manager instance previously created. For example, in this documentation, it is MDSS Access Token Manager.
5. Click Add Mapping.If you do not perform this mapping, PingFederate generates the following log file message: There are no mapped authentication sources to choose from. Please map an IdP Adapter or IdP connection first.
6. Skip the Attribute Sources & User Lookup tab, and on the Contract Fulfillment tab, add the following:

| Contract | Source | Value |
| --- | --- | --- |
| userName | Adapter | username |

- Click Next to skip the Insurance Criteria tab then click Save.
