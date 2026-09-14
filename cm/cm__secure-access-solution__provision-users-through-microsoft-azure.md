<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/provision-users-through-microsoft-azure -->

# Provision Users Through Microsoft Azure

## [Step 1. Create SDP app on Microsoft Azure](https://www.opswat.com/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure#step-1-create-sdp-app-on-microsoft-azure)

1. Log into Azure Portal as Administrator.
2. Navigate to **Enterprise applications >** **All applications**. Then click on **New application**.

![](https://uploads.developerhub.io/prod/97qW/odekq5e0akmnge3cdrdpaah9bwvenqwfqgo3ylzj55x5mcwitvl5z54j4pavo2rl.png)

3. Click on **Create your on application** and input a name. Then click **Create**.

![](https://uploads.developerhub.io/prod/97qW/cssuqjz1iwisomhmnritkomysy8lkw20zvolo8qfk1op77vf4zq5n4510cfqz4nw.png)

4. Enter some placeholder value for fields in Basic SAML Configuration, then click save. You will need to to update these fields in later steps.

![](https://uploads.developerhub.io/prod/97qW/ttyaw1231m5frcsk06215grkge5wft52mz6bx60hho149v9x34751rpkok2qu7gn.png)

5. Add group claim for SAML Response.

5.1. Click *Edit* on section *User Attributes & Claims.*

![](https://uploads.developerhub.io/prod/97qW/ht2253ukbucb7mhyqmquahpwje4mimps4v0evxil8r1yehatsnbm5hagnippz9uc.png)

__

5.2. Click on "Add a group claim", choose "All groups" options(or you can choose what group you want to include in the SAML response) then click **Save**.

![](https://uploads.developerhub.io/prod/97qW/idwll0c5e3if0e8kqujdzjg6sdfp4q6nd4nay27o28c21k8igztn2xa83hj5uvon.png)

5.3. Get the Group Claim name.

![](https://uploads.developerhub.io/prod/97qW/7pqvcalua5quzjmket2ifu9unczkmnlvnpb74lztwzqr5080effrwn0b4hzrdmuf.png)

__

6. Download Azure metadata for the SDP app. This data will be used to upload to My OPSWAT Central Management to enable single sign on for your users. Select Single sign-on on the left navigation, scroll down to SAML Signing Certificate section and and click on "Federation Metadata XML" to download IDP metadata file.

![](https://uploads.developerhub.io/prod/97qW/jwwdwj8948t1htiiur9onw66nelu0vdqjomij0ga21wgf58ngudqcnxdqt6b96jc.png)

7. (Optional) Get additional information

7.1. Download Azure’s certificate.

![](https://uploads.developerhub.io/prod/97qW/s6shy4sgeow1jbay9veql9yvhzxg6qznzvujveuv4aesj9eywtjmln5z9gql5q56.png)

7.2. Get Azure Login URL.

![](https://uploads.developerhub.io/prod/97qW/av5hupkx21uxas2w1ivaizcncf6pjeqvdfe17ceaqpmet978n40jbnbgu9f7ij1e.png)

7.3. Get Azure AD Identifier.

![](https://uploads.developerhub.io/prod/97qW/ah913b6l44fselbxsbtju6zb25cnsdkzuxrlovxlja7mfepcv552x15v2jsn1ywf.png)

8. Assign your users/groups you want to allow log into SDP on My OPSWAT Central Management to this application.

## [Step 2. Configure SSO SDP on My OPSWAT Central Management](https://www.opswat.com/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure#step-2-configure-sso-sdp-on-metadefender-it-ot-access)

1. Log into the [My OPSWAT Central Management](gears.opswat.com).
2. Navigate to User Management > SSO > SDP and check “Enable Single Sign On”.

![](https://uploads.developerhub.io/prod/97qW/h1cayi4y35aqek5ytcm1t68d1y6v4y5iqlsqlmsvtqmir6a4xzbki9ktaeymaig8.jpg)

3. Next to “Import configuration from XML Metadata file”, click “Choose File” and upload the “metadata” file you just downloaded in Step 1.6. This should automatically fill in the “Current Certificate”, “Issuer”, and “IdP SSO URL” fields Leave the Logout URL and Error URL fields blank.
4. (Optional) Use this step if you can not import the metadata file
   1. **IdP Certificate**: Upload the certificate downloaded in Step 1.7.1
   2. **Issuer:** Use the value got from Step 1.7.3
   3. **IdP SSO URL**: Use the value got from Step 1.7.2
5. At the bottom, click “Add Group Attribute” and enter the value from Step 1.5.3

![](https://uploads.developerhub.io/prod/97qW/q8k7cw92pg4d80epbq9hvx7dyg9qrybg1vcyjg0mt6oi9sylhuix3cgbd1oaq2sy.png)

6. Scroll to the top of the page, click “Save” and enter your PIN.
7. At the bottom of the page you will see a new value called “My OPSWAT Central Management Login URL”.

![](https://uploads.developerhub.io/prod/97qW/25lgysh7t47h0fejpsi1myv88btlknuvjpgdkuuf7vppctcfe08jbskh0x391sjw.png)

8. Copy new value called “My OPSWAT Central Management Entity ID“

![](https://uploads.developerhub.io/prod/97qW/4az4wcdkpnao8mmyxy24ct8htm90ptxj49yrx8dyo4heuu6n8z5n9vizhnfp6tcl.png)

## [Step 3. Update Applications settings on Identity Provider](https://www.opswat.com/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure#step-3-update-applications-settings-on-identity-provider)

1. Log into Azure Portal as administrator.
2. Click **Azure Active Directory**.
3. Navigate to **Enterprise applications >** **All applications**.
4. Select the SDP application.
5. Select Single sign-on.
6. Click the edit icon (pencil icon) on Basic SAML Configuration section.
7. Replace Identifier with value got from Step 2.8. Replace Reply URL with the My OPSWAT Central Management URL which you got from Step 2.7.
8. Click **Save.**

![](https://uploads.developerhub.io/prod/97qW/6ckpccpevio3hogqi9qu86yf2o4gqqvewd3sime5egoya8u7e5q7bya2zwphkvcf.png)

## [Step 4. Configure IDP Groups on My OPSWAT Central Management](https://www.opswat.com/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure#step-4-configure-idp-groups-on-metadefender-it-ot-access)

1. Navigate to the My OPSWAT Central Management console, then go to User Management > IdP Groups, and click “Add”.
2. Fill in a group name from your Azure, enter your PIN and choose Add. Your new group will show up in the “IdP Groups” section.

![](https://uploads.developerhub.io/prod/97qW/ldbc5hqaak5rdh3z4bruv8mbslesgxut66r56nhoqjqf72z8254dkhnzrh82gjsd.jpg)

3. When you are ready to assign your new groups to protected applications, go to Secure Access > Protected Apps, click the “Assign” link next to your desired application(s).
4. On the “Assign End Users/IdP Groups to Protected Applications” Move groups “Available Users/Groups” to “Selected Users/Groups” to assign access, then enter your PIN again and choose Enter.

![](https://uploads.developerhub.io/prod/97qW/ft8k25l0aiem0swb1skfarostwdxx2tnf9dvmtiqv0eujpwoxnbubmyfgbqybyer.png)
