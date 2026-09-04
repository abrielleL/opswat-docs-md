<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/f5-big-ip-apm-with-salesforce -->

# F5 BIG-IP APM with Salesforce

OPSWAT MetaDefender IT-OT Access can be easily integrated with an existing F5 BIG-IP & Salesforce integration to ensure that a device is compliant with the organization's security policy before it is granted access to Salesforce. This ensures that the device is not only authenticated by the IdP, but also checked for security risks and vulnerabilities such as encryption, infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

You can learn more details for each step here at [How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

## [Step 1.Enable Secure Access on your MetaDefender IT-OT Access Account](/docs/macloud-sdp/secure-access/f5-big-ip-apm-with-salesforce#step-1enable-secure-access-on-your-metadefender-it-ot-access-account)

1. Log into the MetaDefender IT-OT Access console
2. Navigate to **Secure Access > Protected Apps**
3. Check the box **Enable Secure Access**.
4. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

## [Step 2. Enable Single Sign-On on F5 BIG-IP APM](/docs/macloud-sdp/secure-access/f5-big-ip-apm-with-salesforce#step-2-enable-single-sign-on-on-f5-big-ip-apm)

Note: If you already enabled single sign-on on F5 BIG-IP APM and integrated Salesforce app there, you can jump to downloading a certificate which you configured for Salesforce app on F5 BIG-IP APM for later use. You can refer [F5 - Module 1: SAML Identity Provider](https://f5-agility-labs-iam.readthedocs.io/en/latest/class4/module1/module1.html) for more details.

1. Log into your F5 BIG-IP console.
2. Go to **Access** → **Federation** → **SAML Identity Provider** → **Local IDP Service** then click **Create**

   1. **General Settings:**

      1. *IDP Service Name*: an unique name, for ex: F5_AS_IDP
      2. *Idp Entity ID*: uniqe ID, for ex: https:<ip address>/F5_AS_IDP
      3. *Scheme*: https *Host*: your host name or IP address

3. **Assertion Settings:**

   1. *Assertion Subject Type*: Unspecificed
   2. *Assertion Subject Value*: %{session.logon.last.username}

4. **Security Settings:** Choose your *Singing Key* and *Signing Certificate*, we use default key and value for this demo.

5. Then click **OK**.
6. Go to **Access** → **Webtops** → **Webtop Lists** to create new Webtop

   1. *Name*: an unique name, for ex: full_webtop
   2. *Type*: Full

7. Then click **Finished**.
8. Go to **Access** → **Federation** → **SAML Resources** to create new SAML Resource

   1. *Name*: an unique name, for ex: Salesforce
   2. *Publish on Webtop*: check Enable
   3. *SSO Configuration*: choose the one created in step 2.2.
9. Click **Finished**.

10. **Authentication:** F5 BIGIP provides many authentication methods like Kerberos, Active Directory, LDAP,... We use Local User DB for this demo.
11. Go to **Access** → **Profiles / Policies** → **Access Profiles** then click on

    1. *Create Name:* an unique name, for ex: F5_AS_IDP
    2. *Profile Type*: All

12. Then click on **Finished**.
13. Edit **Access Policy** for the **Access Profile**

    1. Click **Edit** in the **Per-Session Policy** field of the newly created Access profile

       1. Logon page is default
       2. LocalDB Auth is for demonstration purposes only

*Note: For this example, select a valid LocalDB Instance that you can populate.*

14. Advanced Resource Assign: Add an expression for **LocalDB Auth has Passed** and assign the previously created Webtop and SAML Resource based on that success.

15. Change the result of the fallback Branch for **Advanced Resource Assign** to **Allow**.
16. Create Virtual Server for IdP Service and Webtop

    1. Go to **Local Traffic** → **Virtual Servers** → **Virtual Server List** then click **Create**
    2. **General Propteries:**

       1. *Name*: an unique name
       2. *Type*: Standard
       3. *Source Address* : 0.0.0.0/0
       4. *Destination Address/Mask* : your IP address
       5. *Service Port* : An available port that aligns with the port specified or implied in previous steps. For ex: 443, HTTPS
       6. *State*: Enabled

17. Configuration (basic)

18. Access Policy

    1. *Access Profile*: Select the access profile configured in Step 2.6

19. Click **Finished**.
20. Download the certification, as you will need to upload this into MetaDefender IT-OT Access later.
21. Go to **System** → **Certificate Management** → **Traffic Certificate management** → **SSL Certificate List**
22. Choose certificate that is used to singing SAML data. We use *default* certificate for demo purpose.

23. Click **Export**.

## [Step 3. Add Application on MetaDefender IT-OT Access](/docs/macloud-sdp/secure-access/f5-big-ip-apm-with-salesforce#step-3-add-application-on-metadefender-it-ot-access)

1. Log into the MetaDefender IT-OT Access Console.
2. Navigate to **Secure Access > Protected Apps**.
3. Select **Add a Protected Application**.
4. Select **IdP Method**.
5. Fill in required fields for the Identity Provider:

   1. *IdP Name:* an IdP name, for example: Salesforce
   2. *IdP Certificate*: upload BIG-IP APM certificate you downloaded.
6. Click **Continue.**
7. Fill out required information:

   1. *Application*: application name, for example: Dropbox
   2. *Login URL*: https://<BIGIP host>/saml/idp/res=?id=/<SAML Resource path>/ <SAML Resource name>. For ex: [https://10.0.4.83](https://10.0.4.83/) /saml/idp/res=/Common/Saleforce
   3. *App ACS URL* : URL that is provided in Step 6.
   4. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)
8. Click **Add**.
9. After saving your changes successfully, navigate to the **Setup Instructions** of the Salesforce application you have just added and then copy the **URL** MetaDefender IT-OT Access generated there. This URL is used to replace Salesforce login URL on BIG-IP APM.

## [Step 4. Configure SSO settings on applications](/docs/macloud-sdp/secure-access/f5-big-ip-apm-with-salesforce#step-4-configure-sso-settings-on-applications)

1. On MetaDefender IT-OT Access console, navigate to **Secure Access > Protected Apps**.
2. Select the Salesforce app and follow the SSO instructions, you should be prompted to download the **OPSWAT Certificate**.
3. Go to **Local IDP Services** in BIGIP and choose the one created in Step 2.2 Click on **Export Metadata**
4. Log into Salesforce as an administrator
5. Navigate to **Setup > Security Controls > Single Sign-On Settings** , click on **New from Metadata File** then choose the file get from above step.

6. Upload the OPSWAT certificate from your MetaDefender IT-OT Access account which you downloaded.
7. Get Login URL

8. Get Logout URL

   1. You can find "**Logout**" link when you click on your name.
   2. Right-click **Logout** link and select "**Copy link address**" to copy logout URL.

## [Step 5. Configure Access Rules](/docs/macloud-sdp/secure-access/f5-big-ip-apm-with-salesforce#step-5-configure-access-rules)

1. On MetaDefender IT-OT Access console, navigate to **Secure Access > Rules**
2. On **Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application:

   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Configure Access Rules](https://docs.opswat.com/macloud-sdp/secure-access/access-rules)
4. Click **ADD RULE**.

## [Step 6. Update Applications settings on Identity Provider](/docs/macloud-sdp/secure-access/f5-big-ip-apm-with-salesforce#step-6-update-applications-settings-on-identity-provider)

1. Log into your F5 BIG-IP console.
2. Go to **Access** → **Federation** → **SAML Identity Provider** → **External SP Connector** then click Create to create new **SP Connector**

   1. *Service__Provider Name*: an unique service name
   2. *Service__Provider Entity ID*: an unique entity ID
   3. _ACS URL:_specific URL user will be redirected after login to BIG-IP

3. Make sure *Response must be signed* and *Assertion must be signed* checked

4. Then click **OK** to finish
5. Now, choose the IDP Service just created in Step 2.2 then click on **Bind/Unbind SP Connectors** and choose the SP Connector created in Step 5.2.
6. Then click **OK**.

## [Step 7. Test your integration](/docs/macloud-sdp/secure-access/f5-big-ip-apm-with-salesforce#step-7-test-your-integration)

Follow guideline at [Test your integration](https://docs.opswat.com/macloud-sdp/secure-access/test-your-integration) to test your integration to verify if it works as your expectation.
