<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-expensify -->

# Okta IdP with Expensify

My OPSWAT Central Management can be easily integrated with an existing Okta Expensify integration to ensure that a device is compliant with the organization's security policy before it is granted access to Expensify. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access Expensify with Okta Single Sign On (SSO) service, you set up SSO between Okta and Expensify manually as below steps even you already have SSO set up for Expensify on Okta. The built-in Expensify application doesn't allow you to modify a single sign on URL of Expensify.

1. Log into the Okta console as an Administrator
2. Switch to Admin view, navigate to Application

![](https://uploads.developerhub.io/prod/97qW/n88h4lwifpd4ftdwd2s90mbp1hmp22j5swqrlo7813e92rwoqfavan90s2541bhh.png)

3. Click **Add Application**

![](https://uploads.developerhub.io/prod/97qW/2hrvm6s5d3pyu45bvyoo1h5t1myt02zs69dnw6awpw9fkg3zfr0w5udanwa3xfr9.png)

4. Click "**Create New App**" button to create an application manually

![](https://uploads.developerhub.io/prod/97qW/o9ftba86e8z5qrw87psutsa7nat7urmuuh9i5evcfkeq8dh8jlsq3odt2rll6pja.png)

5. Select **SAML 2.0** option and click **Create**

![](https://uploads.developerhub.io/prod/97qW/sqdflf12k252cfb6qwjwoxjuxfe41o69dnvqbgqotg8cj530gsf5e85yome6cgvm.png)

6. On the step **1 General Settings**, fill in the app name and upload a new logo for the app if needed, then click Next

![](https://uploads.developerhub.io/prod/97qW/y7pllcu7gzxe8z47jccp9wf2lf1cy3c38nhxb63rxlwxgkszrqfsddl04atbcfo0.png)

7. On the step **2 Configure SAML**, fill in the below information and then click Next
   1. *Single sign-on URL* is a Expensify single sign-on post back URL: [https://www.expensify.com/authentication/saml/loginCallback?domain=your_domain.com](https://www.expensify.com/authentication/saml/loginCallback?domain=your_domain.com)
   2. *Audience URL (SP Entity ID)*: [https://www.expensify.com/authentication/saml/loginCallback?domain=your_domain.com](https://www.expensify.com/authentication/saml/loginCallback?domain=your_domain.com)
   3. *Name ID format*: EmailAddress
   4. *Application username*: Okta username

![](https://uploads.developerhub.io/prod/97qW/4p1vm2o8tc5tz77cgn2y0xf53eiu1olv8nn95u4n4lt4lmdfdzilk75mu4lyxfxq.png)

8. On the step **3 Feedback**, select the option "**I'm an Okta customer adding an internal app**" and click Finish

![](https://uploads.developerhub.io/prod/97qW/cn42u7ep8ydu5n35pizbp98ziyekct7m273scend5831viszh84n18mysnvgl1kv.png)

9. On Sign On tab, you can view Setup instructions to get IdP metadata and follow guideline [here](https://docs.expensify.com/advanced-admin-controls-domain-control/saml-single-sign-on-sso) to set up single sign-on settings on Expensify.
10. On Assignments tab, click on Assign to assign person you want to allow to access this application

![](https://uploads.developerhub.io/prod/97qW/ooff6sn11bjpj0c3kceiy166ztzm0o2raczq1f0zzxeoi61o9vedmupzumrd7yts.png)

After configuring SSO, you should test it out to make sure that SSO works as expected.

Now it's the time you can implement integration My OPSWAT Central Management with your Okta Expensify by following the below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your My OPSWAT Central Management account](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Expensify.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Expensify.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Expensify.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Expensify.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on applications](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Expensify.html#step-5-configure-sso-settings-on-applications)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Expensify.html#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations.**
3. Check on the box **"****Enable access control****".**
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/1rlha6841ic8xglsdk2ab1h6ntnilariut68i03bok7oqv4wb856dgm84py1bznl.png)

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Login to Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/3lr736ufsfsqimmxdbtj8i962zts9ibcpo9fslxaciiwkxvgbiin29rskefhsjmq.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/h0c1vbmy6k0k2v6mvbvs1ay5oowohfv39afgzzhnzf84ibxcjqpojjas7ic244hm.png)

4.  Select the Expensify application which you just added above

5.  Go to **Sign On** tab and click **View Setup Instruction** **

![](https://uploads.developerhub.io/prod/97qW/0vznzo7st6lr7wyq06ss1so0s1szxodevp295ovkpfwwkta56wwzkw2k23r3dc3n.png)

**

6.  Search for **X.509 Certificate** and c lick **Download certificate** to download Okta certificate

![](https://uploads.developerhub.io/prod/97qW/4abdlxo3zzy1q1f2v1g5wq0brpe3fom6r1m9p025ns5hqdknaa2y4j7t0qo8hmy5.png)

2. IdP Login URL: this is an embed link which Okta generated for the app to embed outside Okta. You can find this URL on General tab, scroll down to the App Embed Link section

![](https://uploads.developerhub.io/prod/97qW/v1aptkn64odtbb04ccua6wstrbu3un4slz667n5wzu93fxj53ijwwl3ikcumgcih.png)

3. Expensify LoginURL: is a Expensify single sign-on post back URL of your organization's Expensify which you configured when you set up SAML SSO in the Okta, for example [https://www.expensify.com/authentication/saml/loginCallback?domain=your_domain.com](https://www.expensify.com/authentication/saml/loginCallback?domain=your_domain.com)
4. Collect Expensify Logout URL: you can find this URL inside of Expensify, for example [https://www.expensify.com/authentication/saml/logoutCallback?domain=your_domain.com](https://www.expensify.com/authentication/saml/loginCallback?domain=your_domain.com)
   1. Log into your organization's Expensify account
   2. Click on your avatar, right click on **Sign out** and choose **Copy link address** to get log out URL

![](https://uploads.developerhub.io/prod/97qW/l3nb1iwue7twzjxza39tlx61vc34pvdwozg4wgvo4a6mdp6waywkd1mkn3a3lks9.png)

3.  Store the log out URL in somewhere for a later use

5. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to 5 to add Expensify application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Access Control** and then **Configurations**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: Okta
      2. *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/lr1fju4ibapnajl5f8435keufvxq8qt3ku3vyjic9inewpi3artq4u3mk4apzqwv.png)

5.  Click **Add IDP**

6.  Click **SAVE**

6. Add Expensify application:
   1. Expand the Okta IdP settings you have just added in Step 2.4 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: Expensify
      2. IdP Login URL:
      3. *Login URL*: application login URL which you have from Step 2.2
      4. *Logout URL*: application logout URL which you have from Step 2.3
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/7l3pqjgp9khq8z3344525t5bajm60as6q39bnq62ij56tex8r344n9r3snj4wtwc.png)

4.  Click **SAVE**

7. After saving your changes sucessfully, click the **Setup Instructions** button of the Expensify application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace Expensify login URL on Okta in Step 4.

![](https://uploads.developerhub.io/prod/97qW/voxpx3qr3wfjr90mcgic361c6cbcxcbubyvna2hm7i4kf1vzxfd5hk2vv7yyarlr.png)

Note: you can add Expensify application (step 2.6) when you add Okta IdP settings in step 2.5.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Configurations**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/d8wvhp3vequpaz1uy5udjjnfrb7invdo2qgre95cjae87n6y95v5baxx3pxy2n0v.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Go to Applications dashboard
3. Select Expensify application
4. On **General** tab, click Edit on the SAML Settings box
5. Click **Next** at the first step
6. Replace **Single sign on URL** with the My OPSWAT Central Management URL which you got from Step 2.6

![](https://uploads.developerhub.io/prod/97qW/wtw98w3zc1twj1y4mv1i74kvxrntsag0x5o5jk838teq179u9dzthck33e9tngy5.png)

7. Click **Next** and **Finish**

## Step 5. Configure SSO settings on applications

1. On My OPSWAT Central Management console, navigate to **Access Control** > **Configurations**
2. Download OPSWAT certificate

![](https://uploads.developerhub.io/prod/97qW/v3239tldcx9g8jadl64xf36rf6v4fb6ucfix070xdfkmc3zytljy1zu3uduklgzl.png)

3. Login to Expensify as an administrator
4. Navigate to **Admin > Domain Control > [yourDomainName] > SAML**
5. Replace a certificate in the IdP MetaData with OPSWAT certificate OPSWAT generated for your account (you downloaded in step 5.1). The certificate in the IdP metadata is placed in a tag **"<ds:X509Certificate>"**

![](https://uploads.developerhub.io/prod/97qW/nd3opv3bpmmyf9csvc4nneeh4odhv74csn9vb9cr8yyd81pyciijr0z9672ff29d.png)

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
