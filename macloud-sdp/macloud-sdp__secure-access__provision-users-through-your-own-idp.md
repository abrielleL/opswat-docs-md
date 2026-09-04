<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/provision-users-through-your-own-idp -->

# Provision users through your own IdP

**In this article you will learn at a high level how to:**

Info

- Set up and configure MetaDefender IT-OT Access as a Service Provider (SP) in most IdPs
- Export the resulting connection data from your IdP and import it to the MetaDefender IT-OT Access Console.
- Enable SAML SSO for your Secure IT Access (SDP) end users.
- Provide access to SDP-protected applications based on IdP group membership.
- Invoke SDP by logging in to your IdP as an end user.

**If you need help with your specific IdP, please see one of the pages below.**

- [3.2.1.3.1.1.1 Okta](https://onlinehelp.opswat.com/metaaccess/3.2.1.3.1.1.1_Okta.html)
- [3.2.1.3.1.1.2. JumpCloud](https://onlinehelp.opswat.com/metaaccess/3.2.1.3.1.1.2._JumpCloud.html)
- [3.2.1.3.1.1.3 Microsoft Azure](https://onlinehelp.opswat.com/metaaccess/3.2.1.3.1.1.3_Microsoft_Azure.html)
- [3.2.1.3.1.1.4 Google Workspace/GSuite](https://onlinehelp.opswat.com/metaaccess/3.2.1.3.1.1.4_Google_Workspace_GSuite.html)

1. Log into your existing SAML IdP as an administrator or create a trial account (for example [3.2.1.3.1.1.2. JumpCloud](https://onlinehelp.opswat.com/metaaccess/3.2.1.3.1.1.2._JumpCloud.html) )
2. In an existing production IdP, you will likely already have a number of user accounts organized into groups. For a test IdP, you will need to create one or more users and assign them to groups as shown here: [3.2.1.3.1.1.2. JumpCloud](https://onlinehelp.opswat.com/metaaccess/3.2.1.3.1.1.2._JumpCloud.html)
3. In your IdP, create an application. If there is a catalogue of common SP applications, you will **NOT** want to use those options. You will want to create a custom app.
4. Give the new app a label.
5. Configure the SP Entity IDs. If required, you may also need to fill in an IdP EntityID, but most IdPs specify this for you. These are identifiers the two ends are going to use to verify that authentication attempts are coming from and going to the right places. It doesn’t really matter what they are, just remember them for later when configuring MetaDefender IT-OT Access.
6. In some IdPs, you will also need to configure an IDP URL.
7. Assign one or more existing Users or Groups to access the new application.
8. Enable group attributes for the application. Some IdPs will **NOT** let you pick a group attribute (Microsoft Azure for example). In this case, you will need to determine your IdP’s group attribute. Whatever your group attribute, you will need to remember it later for entry into MetaDefender IT-OT Access.

**NOTE:** Some IdPs will not allow you to assign groups attributes at this point. For those providers, you will need to wait until after you configure MetaDefender IT-OT Access. As such, a couple of these steps will be repeated below. Please ignore them if you have already done the work here!

9. Export the IdP metadata that you will later load into the MetaDefender IT-OT AccessConsole. In some cases your IdP will require you to save the application first and go to a different part of the UI to export the metadata.
10. Navigate to the MetaDefender IT-OT Accessadministration console. Enable single sign-on for SDP.

**Note: that there are two kinds of SAML SSO setup here. The “Console” setup is for logging into the** **MetaDefender IT-OT Access** **administration console itself. The “SDP” setup is for logging in end-users to the SDP product. We’re setting up SDP here.**

12. At the bottom of this form is configuration for Group Attributes. You need to tell MetaDefender IT-OT Access what your IdP is going to use as the attribute containing group information. This can be anything, you’ll just need to enter the same thing into your IdP later.

13. Copy the MetaDefender IT-OT Access Login URL.

14. Save the MetaDefender IT-OT Access SDP SSO configuration using the Save button in the upper right of the current page.

15. Go back to the IdP configuration for this application. Paste the MetaDefender IT-OT Access Login URL as the ACS URL or the SP Login URL.
16. Enable group attributes for the application. Make sure to use the same name specified earlier in the MetaDefender IT-OT Access configuration.
17. Add the group you created earlier to this application in the User Groups tab.
18. Save the application again in your IdP.
19. The MetaDefender IT-OT Access settings applied to a device depend on what MetaDefender IT-OT Access group it is in.
20. You should now define the IdP groups. This should match the name of the group used earlier when configuring the group in your IdP.

21. Add an IDP Group to act as an anchor for the SAML group within MetaDefender IT-OT Access. The “Identity Provider Group” value should match exactly what you entered as the group name in your IdP. The “Name On MetaDefender IT-OT Access” can be anything you like. Some IDPs don’t expose nice names for groups, so this is a chance to give the group a name that is easy to work with on the MetaDefender IT-OT Access side.

22. At this point you can add any protected applications. When prompted for what users have access to these applications select the IDP groups you created earlier.

23. Log in to your IdP as an end user. You may need to log out of the administrator console to get back to a login prompt.
24. Select the MetaDefender IT-OT Access application.
26. SDP should launch and connect. You should have access to that test resource.
