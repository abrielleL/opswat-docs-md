<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/g-suite-with-aws-sso -->

# G-Suite with AWS SSO

OPSWAT MetaDefender IT-OT Access can be easily integrated with an existing G-Suite & AWS SSO integration to ensure that a device is compliant with the organization's security policy before it is granted access to AWS Console. This ensures that the user is not only authenticated by G-Suite, but also a device the user uses to access SaaS applications tested for risks and vulnerabilities such as infections or outdated operating systems, BEFORE it access an organization's cloud services.

To get started with implementing OPSWAT MetaDefender IT-OT Access integration to enforce device posture check before granting a device to access AWS with G-Suite service.

After configuring SSO, you should test it out to make sure that SSO works as expected.

Now it's the time you can integrate MetaDefender IT-OT Access with your G-Suite & AWS SSO by following the below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](https://onlinehelp.opswat.com/metaaccess/G-Suite_with_AWS_SSO.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method on MetaDefender IT-OT Access](https://onlinehelp.opswat.com/metaaccess/G-Suite_with_AWS_SSO.html#step-2-add-protected-applications-with-idp-method-on-metaaccess)
- [Step 3. Update Applications settings on G-Suite](https://onlinehelp.opswat.com/metaaccess/G-Suite_with_AWS_SSO.html#step-3-update-applications-settings-on-g-suite)
- [Step 4. Configure SSO settings on AWS SSO](https://onlinehelp.opswat.com/metaaccess/G-Suite_with_AWS_SSO.html#step-4-configure-sso-settings-on-aws-sso)
- [Step 5: Test your integration](https://onlinehelp.opswat.com/metaaccess/G-Suite_with_AWS_SSO.html#step-5-test-your-integration)

## [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](/docs/macloud-sdp/secure-access/g-suite-with-aws-sso#step-1-enable-access-control-on-your-metadefender-it-ot-access-account)

1. Log into [the MetaDefender IT-OT Access console](https://gears.opswat.com/console)
2. Navigate to **Secure Access** > **Protected Apps**
3. Check **"Enable Secure Access".**
4. Click **SAVE**.
5. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

## [Step 2. Add protected applications with IdP Method on MetaDefender IT-OT Access](/docs/macloud-sdp/secure-access/g-suite-with-aws-sso#step-2-add-protected-applications-with-idp-method-on-metadefender-it-ot-access)

1. Log into G-Suite admin console
2. Go to **Apps > Web and mobile apps** then click on your application. For example: AWS

3. Download G-Suite certificate: the next step is importing an G-Suite certificate to MetaDefender IT-OT Access. This allows MetaDefender IT-OT Access to verify users signing though a trusted G-Suite. Download the certificate by following these steps:

   1. Click on **Download Metadata** on the left and click the download button to download the certificate

4. Collect Idp Login URL

   1. In the **Download Metadata** popup, scroll down and copy **SSO URL**

5. Collect **AWS SSO Sign-in URL**

   1. Login to your AWS console then go to **AWS SSO > Settings** then click on the **Change** link in the section **Identity source

6. **Show individual metadata values** then copy **AWS SSO Sign-in URL

**

7. Add AWS application on MetaDefender IT-OT Access:
8. Log into the [MetaDefender IT-OT Access console](https://gears.opswat.com/console).
9. Navigate to **Secure Access** > **Protected Apps**
10. Click **Add Protected Application** then choose **IDP METHOD** option
11. Choose option **Add new IDP**, enter name and upload the certificate got in step 2.3. Then **Continue**
12. Enter required field

- *Application*_:_ application name, for example: aws
- *IDP*: choose the IDP created in the previous step
- *IdP Login URL*: fill with the link which you have from Step 2.5
- *App ACS URL*: fill with the link which you have from Step 2.4
- *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

8. Enter your pin then click **SAVE**
9. After saving your changes successfully, it shows a popup, copy the **URL** MetaDefender IT-OT Access generated there and download Opswat Certificate.
10. *Configure Access Rules*. This step can be skipped if you have done this step in the past or you can use the default rules

- Navigate to **Secure Access > Rules**
- Click **"ADD NEW RULE"**
- With a new access rule, you need to specify how you would like to block/allow access a device from the application

  - *Rule name*: a rule name, for example Block non-compliant devices
  - *Action*: Block or Allow
  - Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
- Click **ADD RULE**

## [Step 3. Update Applications settings on G-Suite](/docs/macloud-sdp/secure-access/g-suite-with-aws-sso#step-3-update-applications-settings-on-g-suite)

1. Log into G-Suite admin console
2. Navigate to your application
3. Click to section **Service provider details** then replace the **ACS URL** with the link got in step 2.7

4. Click **Save**

## [Step 4. Configure SSO settings on AWS SSO](/docs/macloud-sdp/secure-access/g-suite-with-aws-sso#step-4-configure-sso-settings-on-aws-sso)

1. Login to your AWS console then go to **AWS SSO > Settings** then click on the **Change** link in the section **Identity source**
2. Go to the section **Identity provider metatdata**
3. Fill **IdP sign-in URL** with the URL link got in step 2.7
4. Upload OPSWAT certificate got in step 2.7 to **IdP certificate**
5. Click **Next Review**

## [Step 5: Test your integration](/docs/macloud-sdp/secure-access/g-suite-with-aws-sso#step-5-test-your-integration)

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/G-Suite_with_AWS_SSO.html#src-5719139) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
