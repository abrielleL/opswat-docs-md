<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/provision-users-with-idp -->

# Provision Users with IdP

**In this article you will learn at a high level how to:**

> **Info**
>
> - Set up and configure My OPSWAT Central Management as a Service Provider (SP) in most IdPs
> - Export the resulting connection data from your IdP and import it to the My OPSWAT Central Management Console.
> - Enable SAML SSO for your Secure IT Access (SDP) end users.
> - Provide access to SDP-protected applications based on IdP group membership.
> - Invoke SDP by logging in to your IdP as an end user.

If you need help with your specific IdP, please see one of the pages below.

- [Provision Users Through Okta](https://www.opswat.com/docs/cm/secure-access-solution/provision-users-through-okta)
- [Provision Users Through JumpCloud](https://www.opswat.com/docs/cm/secure-access-solution/provision-users-through-jumpcloud)
- [Provision Users Through Microsoft Azure](https://www.opswat.com/docs/cm/secure-access-solution/provision-users-through-microsoft-azure)
- [Provision Users Through Google Workplace Gsuite](https://www.opswat.com/docs/cm/secure-access-solution/provision-users-through-google-workplace-gsuite)

Here are steps to provision end-users from your own IdP

1. Log into your existing SAML IdP as an administrator or create a trial account
2. In an existing production IdP, you will likely already have a number of user accounts organized into groups. For a test IdP, you will need to create one or more users and assign them to groups
3. In your IdP, create an application. If there is a catalogue of common SP applications, you will **NOT** want to use those options. You will want to create a custom app.
4. Give the new app a label.
5. Configure the SP Entity IDs. If required, you may also need to fill in an IdP EntityID, but most IdPs specify this for you. These are identifiers the two ends are going to use to verify that authentication attempts are coming from and going to the right places. It doesn’t really matter what they are, just remember them for later when configuring MetaDefender IT Access.
6. In some IdPs, you will also need to configure an IDP URL.
7. Assign one or more existing Users or Groups to access the new application.
8. Enable group attributes for the application. Some IdPs will **NOT** let you pick a group attribute (Microsoft Azure for example). In this case, you will need to determine your IdP’s group attribute. Whatever your group attribute, you will need to remember it later for entry into MetaDefender IT Access.

**NOTE:** Some IdPs will not allow you to assign groups attributes at this point. For those providers, you will need to wait until after you configure My OPSWAT Central Management. As such, a couple of these steps will be repeated below. Please ignore them if you have already done the work here!

9. Export the IdP metadata that you will later load into the My OPSWAT Central Management Console. In some cases your IdP will require you to save the application first and go to a different part of the UI to export the metadata.
10. Navigate to the My OPSWAT Central Management administration console. Enable single sign-on for SDP.

**Note: that there are two kinds of SAML SSO setup here. The “Console” setup is for logging into the** **My OPSWAT Central Management** **administration console itself. The “SDP” setup is for logging in end-users to the SDP product. We’re setting up SDP here.**

![](https://uploads.developerhub.io/prod/97qW/hncykvq7xip4a05pvmfx5msnz9h7tepuuv978jz2m6fn1ny4mobsw5v1mtn3sem4.png)

![](https://uploads.developerhub.io/prod/97qW/9gtnp20dfp6u4iqg0jqrmah2sg35uiuoxsg2t0ho2thhyhryhwl7e33b5x00cew4.jpg)

12. At the bottom of this form is configuration for Group Attributes. You need to tell My OPSWAT Central Management what your IdP is going to use as the attribute containing group information. This can be anything, you’ll just need to enter the same thing into your IdP later.

![](https://uploads.developerhub.io/prod/97qW/mgdeme90d6cc9xlzatlvib4s1yea50wyo1gozg4wcmac4sjfbao7uepglqoatat4.jpg)

13. Copy the My OPSWAT Central Management Login URL.

![](https://uploads.developerhub.io/prod/97qW/ho84l4c7zqgttjg7w1qen3tnaxegh2ph8d466sgegacf1ssd0ww7a7440qb1a65a.jpg)

14. Save the My OPSWAT Central Management SDP SSO configuration using the Save button in the upper right of the current page.

![](https://uploads.developerhub.io/prod/97qW/7z32kujlncb6bzobg3jxtroubg5yn4705reo918d97x3lnephl2hq8965cuw1717.jpg)

15. Go back to the IdP configuration for this application. Paste the My OPSWAT Central Management Login URL as the ACS URL or the SP Login URL.
16. Enable group attributes for the application. Make sure to use the same name specified earlier in the My OPSWAT Central Management configuration.
17. Add the group you created earlier to this application in the User Groups tab.
18. Save the application again in your IdP.
19. The My OPSWAT Central Management settings applied to a device depend on what My OPSWAT Central Management group it is in.
20. You should now define the IdP groups. This should match the name of the group used earlier when configuring the group in your IdP.

![](https://uploads.developerhub.io/prod/97qW/agskkr7m4f45534vjz646q89jm6qbliao7xyj1xursmvujt6mp47h9kh2xadpxd2.jpg)

21. Add an IDP Group to act as an anchor for the SAML group within My OPSWAT Central Management. The “Identity Provider Group” value should match exactly what you entered as the group name in your IdP. The “Name On My OPSWAT Central Management” can be anything you like. Some IDPs don’t expose nice names for groups, so this is a chance to give the group a name that is easy to work with on the My OPSWAT Central Management side.

![](https://uploads.developerhub.io/prod/97qW/wl89fkfhg0uup66gj3ncznv1rfxvgm8qr4q93kbf1d1dei4zjdag0vbdqls6w6a0.jpg)

22. At this point you can add any protected applications. When prompted for what users have access to these applications select the IDP groups you created earlier.

![](https://uploads.developerhub.io/prod/97qW/f40n5ujbzrl4hjj0rlabqa2p5xmvwxry8wngylwl5yu7jlc10uf3gvwdch0nn4yw.jpg)

![](https://uploads.developerhub.io/prod/97qW/7kx5ybo9fpf95lg08bpru8iks3y3vrxgmbwk3mzpjgrfq17lk2pklrtlprrbvw4c.png)

23. Log in to your IdP as an end user. You may need to log out of the administrator console to get back to a login prompt.
24. Select the My OPSWAT Central Management application.
26. SDP should launch and connect. You should have access to that test resource.
