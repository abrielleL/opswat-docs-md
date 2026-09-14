<!-- source: https://www.opswat.com/docs/mdss/configuration/ad-fs-saml2-specific-configuration -->

# AD FS SAML2 Specific Configuration

To properly access MDSS, the following AD **Security Groups** are required:

- **SsoAdministrator** - the equivalent of local MetaDefender Storage Security administrator role
- **SsoReadOnlyAdministrator** - the equivalent of local MetaDefender Storage Security read-only role

It is also necessary for the AD user to have an **email address** set up, so that it is set as the MetaDefender Storage Security's user email.

The only supported secure hash algorithm for signing SAML requests is **SHA-256**.

To set up AD FS SSO with SAML2 for **MDSS**, follow these steps:

1. Within the AD FS settings, navigate to the "**Relaying Party Trusts**" directory and click "**Add Relaying Party Trust**"

2. Check **Claims Aware** for the first step

3. Select Enter data about the relaying party manually

4. Give your Relaying party any name you like, and at the configure certificate step, do not enter any encryption certificate and go to the next step (MDSS does not currently support claim encryption)
5. Check Enable support for the **SAML 2.0 WebSSO** protocol, and enter the service URL of **MDSS** (this URI is of form *https://<MDSS-Instance-domain>/callback/saml*)

6. Enter the URI of the **MDSS** instance as the relaying party identifier (this URI is of form *https://<MDSS-Instance-domain>*)

7. For the access **control policy**, select "**Permit everyone**"

8. Confirm the settings added so far and finish.
9. Select the created Relaying Party Trust, click on **Edit Access Control Policy**, and go to the Endpoints tab.

10. Select the configured endpoint, change the binding type to **Redirect**, and save it.

11. Select the created Relaying Party Trust and click on **Edit Claim Issuance Policy**

12. Add a rule and select "**Send LDAP Attributes as Claims**" as the **Claim Rule Template**

13. Give the rule a name, select **Active Directory** as the attribute store and configure the following:

- **E-Mail Address** as **E-mail Address**
- **Is-Member-Of-DL** as **" groups*"***
- **Display-Name** as ***"user_display_name"***
- **User-Principal-Name** as ***"UPN"***

14. Add a rule and select "**Transform an Incoming Claim**" as the Claim Rule Template

15. Give the rule a name, select **Active Directory** as the attribute store and configure the following:

- **"UPN"** at **Incoming claim type**
- **"Name ID**" at **Outgoing claim type**
- **"Persistent Identifier"** at ***Outgoing name ID format*** __ Next, within the

16. Next, within the **AD FS settings**, navigate to the "**Service/Certificates**" directory and double click on your token signing certificate. On the Details tab click Copy to File to save the certificate and use it when configuring SSO on MDSS.

17. On **MDSS**, under the **Single Sign On page** from Settings, configure your provider with the following settings:

- **Authority URL**: the base URL of your AD FS server used for retrieving Federation Metadata (eg. https:/adfs.<yourdomain>.com/)
- **Identity provider certificate**: the certificate obtained earlier from AD FS
- (Optional) **Identity provider issuer**: the claim issuer identifier used to sign the incoming claims (eg. https://adfs.<yourdomain>.com/adfs/services/trust)
- (Optional) **Identity provider login URL**: the login URL of the AD FS instance (eg. https://adfs.<yourdomain>.com/adfs/ls/)
- (Optional) **Identity provider logout URL**: the logout URL of the AD FS instance (eg. https://adfs.<yourdomain>.com/adfs/ls/)
- **Administrator account role name**: if you use custom group names assigned to your SSO users, pick a different role from the default
- **ReadOnly account role name**: if you use custom group names assigned to your SSO users, pick a different role from the default

Info

If your AD FS instance supports **Federation metadata** and has it enabled and configured on the *<Authority URL>/FederationMetadata/2007-06/FederationMetadata.xml* URL, the Issuer, login and logout URL fields are not required, and will be retrieved from the received federation metadata. Otherwise, they must be provided.

If the fields are populated, they will override any value retrieved from the federation metadata, and cause the **Authority URL** to not be validated.

**__×**

---

__
