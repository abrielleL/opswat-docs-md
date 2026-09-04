<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/provision-users-through-your-jumpcloud -->

# Provision users through your JumpCloud

**Objective: Configure a SAML IDP for authenticating users in the** **MetaDefender Endpoint.**

Info

In this article you will learn how to:

- Set up and configure Secure Access for IT as a Service Provider (SP) in JumpCloud.
- Export the resulting connection data from JumpCloud and import it to the MetaDefender IT-OT Access Console.
- Enable SAML SSO for your SDP end users.
- Provide access to SDP-protected applications based on JumpCloud group membership.
- Invoke SDP by logging in to JumpCloud as an end user.

1. Sign up for an account at [jumpcloud.com](http://jumpcloud.com). They provide free IDP services for a limited number of users. Once you’ve got the account created and are signed in to the administrator console you should see something like this:

2. Add a new user using manual entry.

3. Fill in details. I’ve specified an initial password here, but you can let it generate a temporary password too. It’s fine to leave all the other tabs with their default settings for now.

4. Create a group for that user.

5. Give the new group a name

6. Include the user you just created in this new group

7. Save the group, the rest of the group settings can be left alone.
8. Create an application. This will be a “Custom SAML App”.

9. Give it some label.

10. Configure the IDP and SP Entity IDs. These are identifiers the two ends are going to use to verify that authentication attempts are coming from and going to the right places. It doesn’t really matter what they are, just remember them for later when configuring MetaDefender IT-OT Access.

11. Configure the IDP URL. It doesn’t matter what this is, it just can’t conflict with the URL you specified for any other applications you have defined. I’ve changed mine here, but the default would probably also work for you.

12. We’ll come back here later when we have some more information from MetaDefender IT-OT Access. Save your progress so far by selecting “activate”. When you save this application it warns you that you can’t change this later. That’s fine.

13. Edit the application you just created, and export the JumpCloud Metadata. You’ll need this to upload to MetaDefender IT-OT Access.

14. Navigate to the MetaDefender IT-OT Access administration console. Enable single sign-on for SDP. Note that there are two kinds of SAML SSO setup here. The “Console” setup is for logging into the MetaDefender IT-OT Access administration console itself. The “SDP” setup is for logging in end-users to the SDP product. We’re setting up SDP here.

16. At the bottom of this form is configuration for Group Attributes. You need to tell MetaDefender IT-OT Access what JumpCloud is going to use as the attribute containing group information. This can be anything, you’ll just need to enter the same thing into JumpCloud later.

17. Copy the MetaDefender IT-OT Access Login URL.

18. Save the Secure Access for IT SSO configuration using the Save button in the upper right of the current page.

19. Go back to the JumpCloud configuration for this application. Paste the MetaDefender IT-OT Access Login URL as the ACS URL.

20. Enable group attributes for the application. Make sure to use the same name specified earlier in the MetaDefender IT-OT Access configuration.

21. Add the group you created earlier to this application in the User Groups tab.

22. Save the JumpCloud application again.
23. The MetaDefender IT-OT Access settings applied to a device depend on what MetaDefender IT-OT Access group it is in. In this case we want to make sure that SDP is enabled for the MetaDefender IT-OT Access group. For this example I only have the single default group. Note that I’ve already got a device in this group. If you need to install the MetaDefender Endpoint and get a device in inventory do so now.

24. You should now define the IDP groups. This should match the name of the group used earlier when configuring the group in JumpCloud.

25. Add an IDP Group to act as an anchor for the SAML group within MetaDefender IT-OT Access. The “Identity Provider Group” value should match exactly what you entered as the group name in JumpCloud. The “Name On MetaDefender IT-OT Access” can be anything you like. Some IDPs don’t expose nice names for groups, so this is a chance to give the group a name that is easy to work with on the MetaDefender IT-OT Access side.

26. At this point you can add any protected applications. When prompted for what users have access to these applications select the IDP groups you created earlier.

27. Log in to JumpCloud as a the user you added earlier. You may need to log out of the administrator console to get back to a login prompt at <https://console.jumpcloud.com/login>. You may need to switch to the “User Login” version of this page. If you’re on the Administrator Portal the button in the top left can switch to the User Portal.

28. Select the MetaDefender IT-OT Access application.

30. SDP should launch and connect. You should have access to that test resource.
