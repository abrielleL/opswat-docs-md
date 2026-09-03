<!-- source: https://www.opswat.com/docs/cm/user-management/with-adfs -->

# Provision console users via ADFS

## [Add Relying Party Trust fo](https://www.opswat.com/docs/mdcore/configuration/adfs-saml-single-sign-on#add-relying-party-trust-for-adfs)r ADFS

In the top right corner of **Server Manager**, click **Tools** and select **AD FS Management** from the drop-down list.

![](https://uploads.developerhub.io/prod/97qW/l2mzpg72d2a2zsbw5b9lcsnir2qnt26pkzydj9elgpsh1to5o5jikor0tzbjqgta.png)

In the **AD FS** window, right click on **Relying Party Trusts** and select **Add Relying Party Trust** from the drop-down menu.

![](https://uploads.developerhub.io/prod/97qW/vpsxct0316ohnu54y2lb185csu1i3dphkzrnxwuh6a57fsd03z5imks76gnoznig.png)

In the **Add Relying Party Trust Wizard**, there is **Steps Column** on the left side, on the **Welcome** page, select **Claims aware** and click **Start**.

Then, On the **Select Data Source** page, choose **Enter data about the relying party manually** and click **Next**.

![](https://uploads.developerhub.io/prod/97qW/v3adhpr29vjkw6uzk8fuwjzlzrv3n8svucka7u3y58tgfn9qkoygk98bqnb1nhbb.png)

Then, next on the **Specify Display Name** page, provide a descriptive name for your relying party, and click **Next**.

![](https://uploads.developerhub.io/prod/97qW/375so3fnp1fndonju8ka9ft6c5ogmgdacja9gdct8d72qc14364lv9yyy738ry5j.png)

Then, on the **Configure Certificate** page, Click **Next.**

Next, on the **Configure URL** page, check the box for **Enable support for the SAML 2.0 WebSSO protocol** and set a placeholder, using [https://myplaceholder](https://myplaceholder) as an example, for **Relying party SAML 2.0 SSO service URL**.

![](https://uploads.developerhub.io/prod/97qW/hrcc2k86ntvt35us0f6tk6ob7v3d7um21f1b5icpxtjfvbvytgu1j90iq0na8psd.png)

Next, on the **Configure Identifiers** page, set **OPSWAT_CENTRAL** as **Relying party trust identifier**, then click **Add** and **Next**.

![](https://uploads.developerhub.io/prod/97qW/83jrv1ugah6ztkn48b22tm3qw4esl8c39f0giyt9w9a1snsac6zvhmr7qlhlpsbk.png)

Then, on the **Choose Access Control Policy** page, select **Permit everyone** and click **Next**.

![](https://uploads.developerhub.io/prod/97qW/o3zkassppb4zxf63hd50edvulsymxirjfb8a949j8g8ulylvrsiwc4vddpjry187.png)

Then, on the **Ready to Add Trust** page, Click **Next** to save your information.

If everything goes well, **Finish** page will be displayed for you to click **Close**.

![](https://uploads.developerhub.io/prod/97qW/srfyniqzl7bg7qj701er7oy4maowhzvt2qrkgx24vka15xd65gho1vf6zxvp589k.png)

## [Configure claims Issuance Policy for ADFS](https://www.opswat.com/docs/mdcore/configuration/adfs-saml-single-sign-on#configure-claims-issuance-policy-for-adfs)

In the **Relying Party Trusts** pane of **AD FS** window, navigate to the **relying party** that was added in the previous step, right-click on it, and select **Edit Claim Issuance Policy...** from the drop-down menu.

![](https://uploads.developerhub.io/prod/97qW/nxz9ac6jux85gbmi09ch8mepj9rms62s5rw3pgp4m964v10z8wqqgqvt6w1lifv5.png)

Click **Add Rule,** and in the **Select Rule Template window**, under the **Steps** column, select **"choose Rule type"**.

Select **Send LDAP Attributes as Claims** for Claim rule template and click **Next**.

![](https://uploads.developerhub.io/prod/97qW/8sx012bzxq68us5089af1ml3s0kt90bm3itfx8d1n16t8lno72r7n3wbi5ez1o0c.png)

Enter a name for Claim rule name, for instance, **NameId**. Select **Active Directory for Attribute Store**. Under LDAP Attribute column, choose User-Principal-Name (make sure the value of this field is an email address) from the drop-down list, type **Name ID** for the Outgoing Claim Type column, and click **Finish**.

![](https://uploads.developerhub.io/prod/97qW/voqms9u7vxfe70wj9om8zfizahrt4sddc9i98ujql25b3r6vuv6akgo42w87rmme.png)

Add another Claim rule like this one:

![](https://uploads.developerhub.io/prod/97qW/q4wmhno2tgxel4vzdm5ymgalwnbkvgs0lpmokugchmvgackt0kvsu5qmfb8j1zpt.png)

The SAML response should be like this after adding claim rules

![](https://uploads.developerhub.io/prod/97qW/syhungc26jbkpzw3016lfyefx0isd6b2fin1girc43cesljwaj14nnui5jgp4msf.png)

## Configure SSO in My OPSWAT Central Management

Access the **AD FS Management** tool from Server Manager, expand **AD FS** --> **Service** --> **Endpoints**. In the Endpoints panel, navigate to Metadata section and copy the URL path of type "Federation Metadata".

![](https://uploads.developerhub.io/prod/97qW/bwybwsgeaxfm9hawgw1yw9k2vn0dxbzbg5qzyjbjnd43mgs1lb2vqrsi27udkuwo.png)

Download metadata file with this link:

```html
https://your-adfs-server/FederationMetadata/2007-06/FederationMetadata.xml
```

Then, login to My OPSWAT Central Management console.

Navigate to **User Management** > **SSO** > **Console Authentication**

Check **Enable Single Sign On**

Upload the metadata file, enter the field [**http://schemas.xmlsoap.org/claims/Group**](http://schemas.xmlsoap.org/claims/Group) in the **Group Attributes** box, and click the **Save** button.

![](https://uploads.developerhub.io/prod/97qW/cor1hyhm2te2w6hdwsvl6xy41ml3sgkuu5t1jqjzbm7vfthzf51movg61r3auxal.png)

![](https://uploads.developerhub.io/prod/97qW/4wh4x9la8zov68zem9z7o6rshqtd94gw13092o94mzu2irlbjfon76vchg00jp4y.png)

Scroll down and copy **My OPSWAT Central Management Login URL** and copy **My OPSWAT Central Management Entity ID**

![](https://uploads.developerhub.io/prod/97qW/a901s43p0s5mvlmh1bl4wrgugpf23wnit9xjsbm9j0mnvhni2qne79x8e28hmi4m.png)

Go back to the **AD FS** --> **Relying Party Trusts** and right click on your **relying party trust name** then, select **Properties**

![](https://uploads.developerhub.io/prod/97qW/jr8t50w16307ebhq22z39bgzgx5ly7clgutws236l29lbzu13tpm5g3h6tj78xg9.png)

Then go to **Endpoints** tab, select the placeholder URL and click Edit

![](https://uploads.developerhub.io/prod/97qW/c34rabe6ipm206lgik45uhj71i0omozp36m4d0p6wgmj8ny15ti8uzv70xt2e4h4.png)

Replace the Trusted URL with the **My OPSWAT Central Management Login URL**

![](https://uploads.developerhub.io/prod/97qW/50v6iw1zhqrnr0fa66szvt73o1o51mz1uhvnfye654tof10efv3low50290qybdx.png)

Then go to **Identifiers **tab and replace the placeholder **OPSWAT_CENTRAL** with the **My OPSWAT Central Management Entity ID**

![](https://uploads.developerhub.io/prod/97qW/4toicsjlm49bg4j2xropgn0ovqwmunzmr64s7p6r7vcf66dcsomrneloynfuk8ob.png)

## Update Singing Certificate

Note: This step is optional if you use an incorrect signing certificate from the metadata file.

Go to the **AD FS** --> **Service** --> **Certificates** and right click on the **Token-signing** certificate then export the certificate

![](https://uploads.developerhub.io/prod/97qW/kmun5sg1zzir89bld5qvf08ldv6nwb34t02h2ldn9xo6k28jimpwh0js80a3axhm.png)

Then go to **User Management** > **SSO** > **Console Authentication** to upload the certificate and click **Save**

![](https://uploads.developerhub.io/prod/97qW/fglg699rvwb3xt29xgtjpkdr2kyr21sxwey257eynjkwkfa4nmm1ucewnivaia1f.png)

## Enable IdP-initiated SSO login for ADFS server

By default, in ADFS 2016+, IdP-initiated sign-on is disabled. You need to enable it with PowerShell:

```powershell
Set-AdfsProperties -EnableIdpInitiatedSignonPage $true
```

Navigate to the IdP-Initiated Sign-on page with link like this:

```html
https://your-adfs-server/adfs/ls/idpinitiatedsignon
```

ADFS will show a list of Relying Party Trusts (apps configured in ADFS). Then pick the app you want to log into.

![](https://uploads.developerhub.io/prod/97qW/2omwgvcao7670wg4mrs81wy1tkjco8qjzi8oi4gq63kqspruoo4jtno7vg390h1v.png)
