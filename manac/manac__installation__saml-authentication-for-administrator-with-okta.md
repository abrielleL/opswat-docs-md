<!-- source: https://www.opswat.com/docs/manac/installation/saml-authentication-for-administrator-with-okta -->

# NAC - Configuring SAML Authentication for Administrator

### [Preparing NAC to process SAML authentication](/docs/manac/installation/saml-authentication-for-administrator-with-okta#preparing-nac-to-process-saml-authentication)

1. Before beginning, [contact OPSWAT support](https://www.opswat.com/support) and request that the SAML Authentication for Administrator feature be enabled on your appliance. Also tell them what Identity Provider you intend to use so they can make the necessary remediation resources available to quarantined users.
2. Only continue once you receive confirmation from OPSWAT support that SAML integration has been enabled on the NAC appliance.

### [Configuration on Identity Provider](/docs/manac/installation/saml-authentication-for-administrator-with-okta#configuration-on-identity-provider)

The exact steps for adding a Service Provider will vary by Identity Provider. The steps below use [Okta.com](http://okta.com/), but your Identity Provider may have slightly different steps.

#### [Create a SAML Attribute for Okta user](/docs/manac/installation/saml-authentication-for-administrator-with-okta#create-a-saml-attribute-for-okta-user)

- Navigate to your Okta organization dashboard as a user with admin privileges. Then click **Admin** in the upper right.
- Click **Directory**, select **Profile Editor**
- Click on the default Okta profile

- On Profile Editor screen, click **Add Attribute**

- Provide a name for this attribute, which will be used to assign the NAC profile to the Okta user. You can customize this attribute name according to your organization's requirements.

#### [Create SAML Application](/docs/manac/installation/saml-authentication-for-administrator-with-okta#create-saml-application)

- Navigate to your Okta organization dashboard as a user with admin privileges. Then click **Admin** in the upper right.
- Click **Application**, select **Applications**.

- On the next page, click "Create App Integration", select "SAML 2.0" on the dialog this brings up, then click "Next".

- On the "General Settings" page set "App Name" to "NAC" and upload a custom logo if you would like. Then click "Next".

- On the **SAML Settings** page, set **Single sign on URL** and **Audience URI (SP Entity ID)** to these specific values:

  - *Single sign-on URL* : **https://<your-nac-ip>:8443/api/v1/HandleSAMLResponseLogin.api**
  - *Audience URI (SP Entity ID)* : urn:opswat:saml:auth

- Scroll down to **Attribute Statements** section, click on **Add Another**

- Fill in an extra attribute for [SAML profile](/docs/manac/manac/installation/integrating-nac-with-okta-using-saml-authentication-for-administ#create-a-saml-profile), then click **Next**

- On the **Feedback** page, choose the best answer for you and then click **Finish.**
- On Application details, click **View Setup Instructions** to be taken to the page where we'll get the last piece of information we need to finish setting up the NAC SAML configuration.

- Scroll to the bottom of the page to find a text box referred to as the IDP **metadata**, and NAC will use this to configure itself to use this particular Identity Provider. Copy all of the text from the text box and save it to a .xml file.

#### [Assign Okta user to the Application](/docs/manac/installation/saml-authentication-for-administrator-with-okta#assign-okta-user-to-the-application)

- On your Okta's organization dashboard, navigate to **Directory** and then **People.**
- Select an Okta user.

- On User details page, click on **Assign Applications.**
- Assign user to the application we just created.

#### [Assign NAC Profile to Okta user](/docs/manac/installation/saml-authentication-for-administrator-with-okta#assign-nac-profile-to-okta-user)

- Navigate to **Profile** tab and click on **Edit** attributes.

- Scroll down to the SAML attribute that we created from this [step](https://app.developerhub.io/manac/installation/integrating-nac-with-okta-using-saml-authentication-for-administ#create-a-saml-profile).
- Fill in the NAC Profile to the Okta user

- Sample NAC Profiles could be found on User Management screen.

### [NAC Configuration](/docs/manac/installation/saml-authentication-for-administrator-with-okta#nac-configuration)

- From the NAC UI, under **Configuration** > **Administrator SSO** > **Identity Provider Configuration**, click on the **New SSO IDP** button.

- Give the new Identity Provider a name, check the **Default SSO IDP** box, select the .xml file with the metadata you got from your [Identify Provider](/docs/manac/manac/installation/saml-authentication-for-administrator-with-okta#create-saml-application), and click Create SSO IDP.

- After create, you should observe the integration display successfully

###

### [Test The Integration](/docs/manac/installation/saml-authentication-for-administrator-with-okta#test-the-integration)

From the Login screen of NAC, the button Sign In With SSO should display.

- After click on the button, you will be redirect to Okta login page (if you're currently logged out)

- Sign in with an Okta user and you will be able to access NAC corresponding to your Profile.

- SAML user could not change their password from NAC side.
- And will be display on User Management screen as SAML user
