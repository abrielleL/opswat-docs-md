<!-- source: https://www.opswat.com/docs/my/get-started/set-up-sso-with-okta -->

# Set up SSO with Okta

My OPSWAT Portal offers an integration with a 3rd-party Single Sign-on Service (SSO).

My OPSWAT Portal uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

To get started, go to your identity provider's website and follow the instructions to configure a SSO application for My OPSWAT Portal.

1. Log into Okta as an Administrator
2. Navigate to **Applications** and click on the application you want to configure![](https://uploads.developerhub.io/prod/JYvy/eentjcgiyweaf3uop9d4tn1vif9f9exwtgualnhyejyb7qhu4yoowvlrq5arx9fg.png)
3. From the **General** tab >  **SAML Settings >** Select **Edit** button![](https://uploads.developerhub.io/prod/JYvy/3edtxkmlhvz4cickvu9hjfxs3ernk9d3r783i42a97rxc40054bse2u0sqw1wvt4.png)
4. In the **Configure SAML** step, select:
   1. **Name ID format** = **EmailADdress** to match username of My OPSWAT Portal ![](https://uploads.developerhub.io/prod/JYvy/98zseoxpli7sdenndxkazftl2d5ban01sremlekq5xiy8xtu6dbwb858gmsf1rld.png)
   2. **Attribute Statements (optional):**![](https://uploads.developerhub.io/prod/JYvy/xu5ezz06r02jt8jb0cwfkn7ox8wikskro9l25pzwmwdevcft2saoyitz5vv9m4jc.png)
5. In the **Configure SAML** step, **Attribute Statement (Optional),** and filling as below image and save.
6. Access **Applications > Application > Sign On > SAML Signing Certificates**![](https://uploads.developerhub.io/prod/JYvy/e8gl3w7ggosfby3fk9u8nom1h4hf93tj0uuouh8q79z6e33idqb3oclz8udo52ra.png)
7. Click on **Generate new certificate** to add new Cert
8. Click **Action** at the cert row > Select **Activate** > Save the certificate
9. Select **Action > View Idp metadata** and save this file (Save cert file also) ![](https://uploads.developerhub.io/prod/JYvy/ta3ptfmhg84yjtwut89lml4ay8022guwb21l5fwzkm1z5gs2bc2ytfbkqox9tyuf.png)
10. **Contact My OPSWAT support team via **[**Support Service**](https://www.opswat.com/support/contact-support)**  and provide all below info:**
    - **Ticket Summary**: “Integrate Okta with My OPSWAT Portal”
    - **Description**:
      - **Customer Company Name:** *<your company name>*
      - **Domain** name: _<_*opswat.com* *(It must be a valid domain, if not it will not be accepted)>*
      - Short description for the request ticket:
        - How many users?
        - Do you have Organization?
          - No: please provide Organization name, email of the first Admin.(We will create an Organization and add the first Admin for this Org, then you can invite user to the Organization)
          - If Yes: skip this info
        - OPSWAT will redirect users to authenticate by the configured IDP based on provided domain name or specific user. Do you have any specific users in IDP with different domain emails?
          - If No: skip this info
          - If Yes: Please provide a list user emails
    - **Metadata** file (Which is downloaded from step #9)
    - **Certìicate** file
11. Waiting response from Support Team, they will provide back to you **IdP Start URL**
12. Access to the **Application,** in the **Configure SAML** step > **Edit** and move to **General** > **SAML Settings** > **Edit**![](https://uploads.developerhub.io/prod/JYvy/6a6vtn2246go9ik0rr9h4azrfx7f816lqc6ufdmwcozwieyxatk5dgwtsfml7trn.png)
13. Then use the **IdP Start URL** is provided  at step #11 to correct it in **SAML Settings** and click Save button.![](https://uploads.developerhub.io/prod/JYvy/c5big50eo5v91tjt06mt3estidvshmvsgmpf71mbq7al6j923o2zi77axg76u2ng.png)
14. Now you need to assign people/groups who can access this application on Okta

![](https://uploads.developerhub.io/prod/JYvy/vrahz3fqrbv4dxbqyqbo4l85eoq7nhat4y2hqrmdbdnw56o3aggxvpus80d0fot7.png)

> **Info**
>
> After the user signs in to My OPSWAT Portal using Single Sign-On (SSO), the Admin must manually invite the user to the Organization, or the user needs to send a request to join. This is required in order to share organization entitlements.
