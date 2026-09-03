<!-- source: https://www.opswat.com/docs/my/get-started/set-up-sso-with-microsoft-entra -->

# Set up SSO with Microsoft Entra

My OPSWAT Portal offers an integration with a 3rd-party Single Sign-on Service (SSO).

My OPSWAT Portal  uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any identity provider that supports SAML 2.0.

**To get started, log into** **Microsoft Entra** **and create an application for** My OPSWAT Portal . Details can be found [**here**](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-single-sign-on-non-gallery-applications)

1. Log into [Microsoft Entra](https://portal.azure.com) as an Administrator
2. Select **Application **→ **Enterprise** applications → **”New Application”** ![](https://uploads.developerhub.io/prod/JYvy/8zor48eay573qry65n30w53s097vi1aa2k2zrrs9nksw8osak3p9ydd44lxzyd3c.png)
3. Select **“Create Your own Application”** ![](https://uploads.developerhub.io/prod/JYvy/uoklhkg27hnvjiwwxbfi9sk1u5dwxkz8ztqxmqnruxra793czupq9y4b6fy4uud1.png)
4. Input Application Name into **"What's the name of your app?"** field and select **“Integrate any other application you don't find in the gallery (Non-gallery)”** → Click **Create** button![](https://uploads.developerhub.io/prod/JYvy/74m907b3u1alm93xxpuhgu2nyka3sgvjxj0rzovcwturaw2gg59tm77l2aicw7b3.png)
5. After the Create new application finished. In the middle of page, choose **“Set up single sign on”**

   ![](https://uploads.developerhub.io/prod/JYvy/7zpqxssakg0xhwq5eryy0c4u0cchv4o7xd7y1biwqnvup07bdyrl0ylcv3urbt2f.png)
6. Select **SAML** method

   ![](https://uploads.developerhub.io/prod/JYvy/91bb2xyf3ln2i2xbbxxl0pkwou1w1ptj5s86r9nsul3ra1f09ogs1pa6kqyst7kb.png)
7. At **SAML Certificate** section → **App Federation Metadata Url** → Copy the **XML file/URL**. URL example: [https://login.microsoftonline.com/xxxxxxx/federationmetadata/2007-06/federationmetadata.xml?appid=xxxxxxxx](https://login.microsoftonline.com/xxxxxxx/federationmetadata/2007-06/federationmetadata.xml?appid=xxxxxxxx)

   ![](https://uploads.developerhub.io/prod/JYvy/h560lvn9bvp29xw9kfmo1zbndsj4y2dvtkcrqju3zovlfgwh2ja2iy7khywo1vqz.png)
8. Contact My OPSWAT support team via Support Service and provide all below info:
   - **Ticket Summary:** “Integrate Microsoft Entra with My OPSWAT Portal”
   - **Description**:
     - Customer Company Name:*<your company name>*
     - **Domain** name: <*opswat.com* *(It must be a valid domain, if not it will not be accepted)>*
     - Sample user*: <user_email> * **To minimize the risk of blocking all users in the domain from signing in if there is an issue with the SSO configuration, we would like to enable SSO for a single test user first. Once you confirm that everything is working correctly, we will roll it out to all users in the domain.**
     - **The XML file/URL:** <*Which is downloaded from step #7>*
     - How many users?
     - Do you have Organization?
       - No: please provide Organization name, email of the first Admin.(We will create an Organization and add the first Admin for this Org, then you can invite user to the Organization)
       - If Yes: skip this info
     - OPSWAT will redirect users to authenticate by the configured IDP based on provided domain or specific user. Do you have any specific users in IDP with different domain emails?
       - If No: skip this info
       - If Yes: Please provide a list user emails
9. Waiting response from Support Team, they will provide back to you:
   - Assertion Consumer Service URL (ACS Url): [https://id-api.opswat.com/saml/acs/{opswat_will_provide}](https://id-api.opswat.com/saml/acs/%7Bopswat_will_provide%7D)
   - Identifier (Entity ID): cognito_sso (this is typically the expected value)
10. At **“Basic SAML Configuration"** section, Setup ACS Url and Entity ID with data is received from step #9

    ![](https://uploads.developerhub.io/prod/JYvy/icc1givvbemzky7psalq7crwkglhp3yptx5gq8rgsjoywfc7ndif5c6vbvpi88y5.png)
11. [Option] If you change or add any attributes or claims in the **Attributes & Claims** section, please let us know. Otherwise, you can keep the default configuration for a stable setup.

    ![](https://uploads.developerhub.io/prod/JYvy/kg1999krk73pic1pkd0bhi6c9mxp5zysah1hm96ijupqftox0akcp463232dpu2y.png)
12. Now you need to assign people/groups who can access this application on Microsoft Entra. On the left menu, select **Users and groups** → **Add user/group**.

    ![](https://uploads.developerhub.io/prod/JYvy/k6m8o1kelpi6u41cvh3k52sv6upfzx3ongq6fjl1823enoux2eh4gwceoqr5wdur.png)

> **Info**
>
> After the user signs in to My OPSWAT Portal using Single Sign-On (SSO), the Admin must manually invite the user to the Organization, or the user needs to [send a request to join](https://www.opswat.com/docs/my/my-information/organizations#how-to-request-access). This is required in order to share organization entitlements.

> **Warning**
>
> If user is created without emailAddress, lastName, firstName info on Microsoft Entra, the user cannot single sign-on My OPSWAT Portal.
