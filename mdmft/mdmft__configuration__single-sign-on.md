<!-- source: https://www.opswat.com/docs/mdmft/configuration/single-sign-on -->

# Single Sign-On

Summarize Page    Connect to Cursor Connect to VS Code

Single Sign-On (SSO) allows users to log into MetaDefender Managed File Transfer™ without having to enter the active directory credentials or creating a local account. Enabling SSO is available for Identity Providers (IdP) supporting the OpenID Connect protocol.

Warning

On details about challenges integrating with specific products please see [SSO Integrations](/docs/mdmft/configuration/sso-integrations).

Info

For a step-by-step tutorial, refer to:

- [Integrate with Okta](/docs/mdmft/configuration/integrate-with-okta)
- [Integrate with Active Directory Federation Services](/docs/mdmft/configuration/integrate-with-active-directory-federation-services)
- [Microsoft Entra ID](/docs/mdmft/configuration/mft-integrate-microsoft-entra-id)
## [Requirements](/docs/mdmft/configuration/single-sign-on#requirements)

Below are the technical requirements of MetaDefender® MFT supporting SSO.

### [Technical Details](/docs/mdmft/configuration/single-sign-on#technical-details)

| SSO Details |  |
| --- | --- |
| **Protocol** | OpenID Connect |
| **Authorization Flow** | Authorization Code Flow |
| **Required Scopes** | `openid` , `profile` ,`email` |
| **Response Mode** | `code` and `state` in either:   - OAuth 2.0 Form Post Response Mode - query Response Mode |

### [Claims](/docs/mdmft/configuration/single-sign-on#claims)

Following are the claims used to propagate user details in MetaDefender® MFT by default. Claims are resolved in the following sequence, with the first claim found determining the value for the corresponding user detail.

#### [Default Claim Configuration](/docs/mdmft/configuration/single-sign-on#default-claim-configuration)

| User Detail | Claim(s) |
| --- | --- |
| **User Name** | 1. `upn` 2. `preferred_username` 3. `name` |
| **Display Name** | 1. `unique_name` 2. `name` |
| **Given Name** | 1. `given_name` |
| **Surname** | 1. `family_name` |
| **Email Address** | 1. `email` 2. `upn` |
| **Phone Number** | 1. phone_number 2. phone |
| **Group Memberships** | `Empty by default.` |

Info

If details can not be populated due to missing claims, their values will be left empty.

### [Group Memberships](/docs/mdmft/configuration/single-sign-on#group-memberships)

It is possible to provide MetaDefender Managed File Transfer™ group membership details on SSO claims by providing at least one claim for the **Group Memberships** user detail. The claim should contains a list of group names the user is member of in MetaDefender Managed File Transfer™.

If a group does not exist yet in MetaDefender Managed File Transfer™, it will be created. Group memberships not stated in the claim will be removed.

Info

Names provided for groups in claims are matched against the **Group Name** detail and **not** the **Display Name** value of the MetaDefender Managed File Transfer™ groups.

## [Configuration](/docs/mdmft/configuration/single-sign-on#configuration)

In order to set up single sign-on, go to "Settings" → "Single Sign-On."

### [Redirection](/docs/mdmft/configuration/single-sign-on#redirection)

URL(s) for redirection can be generated on the configuration page of SSO within MetaDefender Managed File Transfer™. The redirection URL's format is the following: `<protocol>://<host>:<port>/vault_rest/authenticate-sso`

For example if MetaDefender Managed File Transfer™ is being accessed on the address `https://my-mft:8010`, then the SSO provider will be asked to redirect authentications to `https://my-mft:8010/vault_rest/authenticate-sso`.

Info

MetaDefender Managed File Transfer™ will always dynamically create the redirection URL based on what address the instance is being accessed on.

| **Name** | **Description** |
| --- | --- |
| Enable SSO | Turn SSO integration on/off |
| Ignore TLS Certificate | Accept requests from the IdP even if the certificate is not fully trusted |
| PKCE Support | Whether to utilize Proof Key for Code Exchange along with the authorization code flow during authentication |
| Load User Profile | Attempt to retrieve user claims by calling the/userinfo endpoint |
| Skip Endpoint Validation | If enabled, the authority of the OpenID endpoints are not validated against the issuer. Acquire this information on the `/.well-known/openid-configuration`endpoint of the SSO provider. |
| Skip Name Validation | If enabled, the name of the authority will not be validated against the issuer. Acquire this information on the `/.well-known/openid-configuration`endpoint of the SSO provider. |
| Provider Name | A friendly name that identifies the IdP in Managed File Transfer |
| Authority | The URL of the IdP |
| IP Address Or Domain | The IP or domain of the MetaDefender Managed File Transfer™ instance used to construct the Redirect URL |
| Redirect URI | The constructed redirection URL to copy and provide in the configuration of the SSO provider |
| Client ID | A unique identifier assigned by the identity provider to registered clients |
| Client Secret | A randomly generated sequence issued by the identity provider and used in client authorization |
| Add /Administrators,Automation Coordinators,Readonly Administrators, etc. | A list of email addresses and subject identifiers used for assigning administrative privileges to their owners ("administrator" / "automation coordinator" / "readonly administrator" / etc. role in MetaDefender® MFT) |
| Integration Scopes (Optional) | A list of optional scopes for making requests to the IdP |
| Additional endpoints (Optional) | Specifies a list of additional base addresses for endpoints |

### [Claims Configuration](/docs/mdmft/configuration/single-sign-on#claims-configuration)

The above mentioned, by default used claims can be modified in the "Claims Configuration" part of the SSO set up page.

### [Role Assignment](/docs/mdmft/configuration/single-sign-on#role-assignment)

Use the role assignment fields to map SSO users to MetaDefender Managed File Transfer™ roles by email address or SSO subject identifier. As you type, the system shows matching existing users along with their name, email address, and subject identifier so you can pick the right match.

You can map users to any of the following roles:

| **Field** | **Role Granted** |
| --- | --- |
| **“Add Administrators”** | Administrator |
| **“Add Automation Coordinators”** | Automation Coordinator |
| **“Add Readonly Administrators”** | Readonly Administrator |
| **“Add Helpdesk Administrators”** | Helpdesk Administrator |
| **“Add Global Supervisors”** | Global Supervisor |
| **“Add Auditors”** | Auditor |
| **“Add Restricted Administrators”** | Restricted Administrator |
| **“Add Verdict Supervisors”** | Verdict Supervisor |
| **“Add User Managers”** | User Manager |

Each field accepts multiple entries, so you can assign more than one email address or subject identifier to the same role.

A single email address or subject identifier can hold only one of these roles at a time. If you add the same entry to more than one field, MetaDefender Managed File Transfer™ displays an error listing the duplicate entries and blocks saving the configuration until you remove the duplicate from all but one field.

Warning

Modern identity providers (e.g., Entra ID) no longer use the `upn` claim as the email field. To ensure proper user mapping and correct functionality of the **dedicated user role** fields, consider adding the `preferred_username` claim to the **Email Address** claims.

Info

There is no technical limit to the number of Single Sign-On (SSO) users. Only the license user limit serves as a restriction.

Warning

Rate limiting may block authentication with SSO. If this occurs, adjust the rate-limiting settings to suit your needs.
