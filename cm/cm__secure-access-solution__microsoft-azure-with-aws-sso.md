<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/microsoft-azure-with-aws-sso -->

# Microsoft Azure with AWS SSO

My OPSWAT Central Management can be easily integrated with an Azure & AWS SSO integration to ensure that a device is compliant with the organization's security policy before it is granted access to AWS Console. This ensures that the user is not only authenticated by Azure, but also a device the user uses to access SaaS applications tested for risks and vulnerabilities such as infections or outdated operating systems, BEFORE it access an organization's cloud services.

Follow below steps to integrate My OPSWAT Central Management with your Microsoft Azure & AWS SSO. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaAccess account](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_AWS_SSO.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Create AWS application on Microsoft Azure](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_AWS_SSO.html#step-2-create-aws-application-on-microsoft-azure)
- [Step 3. Add application and configure Access Rules on MetaAccess](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_AWS_SSO.html#step-3-add-application-and-configure-access-rules-on-metaaccess)
- [Step 4. Configure SSO setting on AWS SSO](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_AWS_SSO.html#step-4-configure-sso-setting-on-aws-sso)
- [Step 5. Update Applications settings on Azure](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_AWS_SSO.html#step-5-update-applications-settings-on-azure)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_AWS_SSO.html#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management

1. Log into [t](https://gears.opswat.com/console)he My OPSWAT Central Management console.
2. Navigate to **Secure Access** > **Protected Apps**
3. Check **"Enable Secure Access".**
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/advvdakqh38zpeq8rwxdaugp45qdtfnx3gky9pudb4y02kbouoiivw8rgjwmcwqg.png)

## Step 2. Create AWS application on Microsoft Azure

1. Log into Azure Portal as Administrator
2. Click **Azure Active Directory** on the left navigation

![](https://uploads.developerhub.io/prod/97qW/v4nz2hq51x1sf31o8fcuyvadmx4t6hntp30skxbzjh7hd0kn5vcqbwh9x5wuuktd.png)

The Azure Active Directory button

3. Navigate to **Enterprise applications >** **All applications**.

![](https://uploads.developerhub.io/prod/97qW/ws4icbrvt2um9a2u0lsxbnhss2i1dlnbyipyhypdkmf6l7q3plu7hzh5gp94h4eg.png)

The Enterprise applications blade

4. Create a Non-gallery application

![](https://uploads.developerhub.io/prod/97qW/tfmd1rbq7li8wa1gc4xlq4qdi3k0yhzqlhw32b0pyob487obhs9ujz2oq2bhku5z.png)

5. Enter some placeholder value for fields in Basic SAML Configuration, then click save. You will need to to update these fields in later steps.

![](https://uploads.developerhub.io/prod/97qW/hbvpdc4neb7ppubawjo9wrvfehszpayjg4zkj02nlsy6k5l19p7z7w8h3ohdxtxz.png)

6. Download Azure Certificate: this allows My OPSWAT Central Management to verify users signing through a trusted Azure. Select Single sign-on on the left navigation, scroll down to SAML Signing Certificate section and and click "Certificate (Base64)" to download the Azure certificate.

![](https://uploads.developerhub.io/prod/97qW/f521rx173envk2lb918ejeimylqjz64hnf3wl9o5pzq61im8d1n8rtq1y78xez6f.png)

7. Collect Idp Login URL. Scroll down copy **Login URL**. Store the URL in somewhere for later use. For example [https://login.microsoftonline.com/60244d0a-5473-4468-b743-f9cc479b7dab/saml2](https://login.microsoftonline.com/60244d0a-5473-4468-b743-f9cc479b7dab/saml2)

![](https://uploads.developerhub.io/prod/97qW/fjv5xpf8vfy0hutbu3yf9ex9dhi4ztcdu3lj8b6vnjr1nim9ysnbi9szq8xa8in2.png)

8. Collect IdP issuer: Scroll down copy **Azure AD Identifier**

![](https://uploads.developerhub.io/prod/97qW/ybn7g7q95qzqklwfllxntou2j2hvpyzada5k076xefsrqff5vg7sskeyqx2jbc9m.png)

9. Collect *User access URL.* Select Properties and copy User access URL

![](https://uploads.developerhub.io/prod/97qW/9uram63mo6sdqj09xdd1gi0ccky6n6dbh3bk6mefkif4qb4yhjsratvntrps0urk.png)

10. Assign your users/groups to this application

## Step 3. Add application and configure Access Rules on My OPSWAT Central Management

1. Log into the My OPSWAT Central Management console.
2. Navigate to **Secure Access** > **Protected Apps**
3. Click **Add Protectedd Application** then choose **IDP METHOD** option
4. Choose option **Add new IDP**, enter name and upload the certificate got in step 2.3. Then **Continue

![](https://uploads.developerhub.io/prod/97qW/9f3shbs3bse91ubpm53hltjpi803xajz23u7gtrt30suy73b93pr1k6qt6a0goyt.png)

**

5. Enter required field
   1. *Application*: application name, for example: Demo
   2. *IdP Login URL*: fill with the link which you have from Step 2.9
   3. *App ACS URL*: fill with the link which you have from Step 2.7
   4. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/p3zqb15tlex5pn7govi7g5d23r8cmogfow4zwxaqsi2dwk8457xbo4h1xe8d8x2u.png)

6. Enter your pin then click **SAVE**
7. After saving your changes successfully, a SSO setup instruction will be shown, copy the **ACS URL** My OPSWAT Central Management generated there and download OPSWAT Certificate. Note that this information can be found in the protected app's details later.

![](https://uploads.developerhub.io/prod/97qW/1019s1cqffwl092egveaqq4u8bg29raok3aqir4dcga1wvwpo0zlb56f4m3xf3bl.png)

8. Configure Access Rules. This step can be skipped if you have done this step in the past or you can use the default rules
   1. Navigate to **Secure Access > Rules**
   2. click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
   3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
      1. *Rule name*: a rule name, for example Block non-compliant devices
      2. *Action*: Block or Allow
      3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
   4. Click **ADD RULE

![](https://uploads.developerhub.io/prod/97qW/c7gbp8n94odxnq87gqh45tox5sxx8v42tvbl9jqj9svdz35x3a36v6lfg9mg4a48.png)

**

## Step 4. Configure SSO setting on AWS SSO

1. Login to your AWS console then go to **AWS SSO > Settings** then click on the **Change** link in the section **Identity source**
2. Go to the section **Identity provider metatdata**
3. Fill **IdP sign-in URL** with the URL link got in step 3.7
4. Fill **IdP issuer URL** with value got in step 2.8
5. Upload Opswat certificate got in step 3.7 to **IdP certificate**
6. Click **Next Review

![](https://uploads.developerhub.io/prod/97qW/niv8m3arg52ud6vapsikx3ay7gpmeg1oizg15is1fdb1jufkcuh9miuo3etquaen.png)

**

7. Expand the metadata values in section **Service provider metadata** then copy **AWS SSO Sign-in URL** and **AWS SSO issuer URL**

![](https://uploads.developerhub.io/prod/97qW/c73rwu5wv3e5onwhpcfyjb00u41yp7ath6zyj71nqk9nehe9e5e1x4wma4ilpzu7.png)

## Step 5. Update Applications settings on Azure

1. Log into Azure Portal as Administrator then go to your application
2. Navigate to your application
3. Select Single sign-on
4. Click the edit icon (pencil icon) on Basic SAML Configuration section
5. Replace **Identifier** with **AWS SSO issuer URL** got from step 4.7 Replace **Reply URL** with the My OPSWAT Central Management URL which you got from Step 3.7 Replace **Sign on URL** with **AWS SSO Sign-in URL** gotfrom step 4.7

![](https://uploads.developerhub.io/prod/97qW/ov4r9c47b19d9rslh4us7raumhi1cb9ayschwzc56pqpc3z76mtioom7udx854et.png)

6. Click **Save**

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_AWS_SSO.html#src-5718831) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
