<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/ad-fs-saml2-specific-configuration -->

# AD FS SAML2 Specific Configuration

> **Info**
>
> To properly access MDSS, the following AD **Security Groups** are required:
>
> - **SsoAdministrator** - the equivalent of local MetaDefender Storage Security administrator role
> - **SsoReadOnlyAdministrator** - the equivalent of local MetaDefender Storage Security read-only role
>
> It is also necessary for the AD user to have an **email address** set up, so that it is set as the MetaDefender Storage Security's user email.
>
> The only supported secure hash algorithm for signing SAML requests is **SHA-256**.

To set up AD FS SSO with SAML2 for **MDSS**, follow these steps:

1. Within the AD FS settings, navigate to the "**Relaying Party Trusts**" directory and click "**Add Relaying Party Trust**"

![](https://uploads.developerhub.io/prod/k8zL/93yeaqxec2qkul4o1h1e6jthh0xar4tdttcpyuz6ars93u28sg5ak2g6vk2kuncb.png)

2. Check **Claims Aware** for the first step

![](https://uploads.developerhub.io/prod/k8zL/tom7gwgu92rdeh54gwd87badmsh9pjspyskmonb9p8qhfqj35q6hzr3ftxuwqz9t.png)

3. Select Enter data about the relaying party manually

![](https://uploads.developerhub.io/prod/k8zL/codthay9m0z4ayrgajzdznuf6s59f6x9vpmgpni6u3rgk548qo3i3p2jphim6kpy.png)

4. Give your Relaying party any name you like, and at the configure certificate step, do not enter any encryption certificate and go to the next step (MDSS does not currently support claim encryption)
5. Check Enable support for the **SAML 2.0 WebSSO** protocol, and enter the service URL of **MDSS** (this URI is of form *https://<MDSS-Instance-domain>/callback/saml*)

![](https://uploads.developerhub.io/prod/k8zL/prgyeygik79rqs560y0e0uioayh018k1eju98tn7k66ps5kr2c32pmi4opsvnbvr.png)

6. Enter the URI of the **MDSS** instance as the relaying party identifier (this URI is of form *https://<MDSS-Instance-domain>*)

![](https://uploads.developerhub.io/prod/k8zL/yqklkvwhlp8bdkotk9qqjnc1qm08j4w0gxrgymmlsd9j94xwfcdm0ev4as4xec63.png)

7. For the access **control policy**, select "**Permit everyone**"

![](https://uploads.developerhub.io/prod/k8zL/kglu3b8da7l3d438t9s9ea2xe3b3a1cqx35qd4g1h5voazkywpnvnxkbcwe9tcyi.png)

8. Confirm the settings added so far and finish.
9. Select the created Relaying Party Trust, click on **Edit Access Control Policy**, and go to the Endpoints tab.

![](https://uploads.developerhub.io/prod/k8zL/p07q0vnlpy96g2siji0cjfz84qy3maddaku3xhu0muah30oqcxufox7s9m970s4f.png)

10. Select the configured endpoint, change the binding type to **Redirect**, and save it.

![](https://uploads.developerhub.io/prod/k8zL/gsy56eli7qqp1hdsoctx4ppmzgxbvvcpth2dudr02iu576rg76xh30oacqe017t7.png)

11. Select the created Relaying Party Trust and click on **Edit Claim Issuance Policy**

![](https://uploads.developerhub.io/prod/k8zL/bil8s1vyu55g8g9deljiqci4qlc1hfxvzmhkr9l5dcwkgk0rmfaf2rii0xzo6njp.png)

12. Add a rule and select "**Send LDAP Attributes as Claims**" as the **Claim Rule Template**

![](https://uploads.developerhub.io/prod/k8zL/ug4uxhajgemgfp07v27reovh1ujkl4i3sxb6l5z5jd50hxxt8cyqzieza6bu0a50.png)

13. Give the rule a name, select **Active Directory** as the attribute store and configure the following:

- **E-Mail Address** as **E-mail Address**
- **Is-Member-Of-DL** as **" groups*****"***
- **Display-Name** as ***"user_display_name"***
- **User-Principal-Name** as ***"UPN"***

![](https://uploads.developerhub.io/prod/k8zL/33zmuozzbcegndsadf73e4yq52dozdyzw08qaptlkqvl76kf5itighpf3w7q4tc4.png)

14. Add a rule and select "**Transform an Incoming Claim**" as the Claim Rule Template

![](https://uploads.developerhub.io/prod/k8zL/zb4irwgu7ysbcwz99p2knal8tsegj4in2n0l6iolxi83jby91ch7lubtgwzrmuvu.png)

15. Give the rule a name, select **Active Directory** as the attribute store and configure the following:

- **"UPN"** at **Incoming claim type**
- **"Name ID**" at **Outgoing claim type**
- **"Persistent Identifier"** at ***Outgoing name ID format*** __ Next, within the

![](https://uploads.developerhub.io/prod/k8zL/uz1077tbno7q01yymndadhcndoo4z0mfrdus971v8y5pzki1xm1m127i21sjc37y.png)

16. Next, within the **AD FS settings**, navigate to the "**Service/Certificates**" directory and double click on your token signing certificate. On the Details tab click Copy to File to save the certificate and use it when configuring SSO on MDSS.

![](https://uploads.developerhub.io/prod/k8zL/ib4h9o70zjyua1s9fsj9tdxmib74muc2yiffp03xpvgqdsvmu2hvyor84rpi2ube.png)

17. On **MDSS**, under the **Single Sign On page** from Settings, configure your provider with the following settings:

- **Authority URL**: the base URL of your AD FS server used for retrieving Federation Metadata (eg. https:/adfs.<yourdomain>.com/)
- **Identity provider certificate**: the certificate obtained earlier from AD FS
- (Optional) **Identity provider issuer**: the claim issuer identifier used to sign the incoming claims (eg.  https://adfs.<yourdomain>.com/adfs/services/trust)
- (Optional) **Identity provider login URL**: the login URL of the AD FS instance (eg. https://adfs.<yourdomain>.com/adfs/ls/)
- (Optional) **Identity provider logout URL**: the logout URL of the AD FS instance (eg. https://adfs.<yourdomain>.com/adfs/ls/)
- **Administrator account role name**: if you use custom group names assigned to your SSO users, pick a different role from the default
- **ReadOnly account role name**: if you use custom group names assigned to your SSO users, pick a different role from the default

> **Info**
>
> If your AD FS instance supports **Federation metadata** and has it enabled and configured on the *<Authority URL>/FederationMetadata/2007-06/FederationMetadata.xml* URL, the Issuer, login and logout URL fields are not required, and will be retrieved from the received federation metadata. Otherwise, they must be provided.
>
> If the fields are populated, they will override any value retrieved from the federation metadata, and cause the **Authority URL** to not be validated.

**__×**![](https://uploads.developerhub.io/prod/k8zL/0jx9c8bvajw3d1pionrxljndvqfu4a33k87g1u8wqfn8bjs8clwjmapw3rjpkd4i.png)

---

__

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
