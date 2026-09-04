<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/provision-users-through-your-okta -->

# Provision users through your Okta

1. On the Okta Admin login splash page choose “Create a new app”

2. Choose Web and SAML 2.0

3. In the “App name” field, fill in “MetaDefender IT-OT Access” or something similar. You can also upload a logo if you like. Do not check the “App visibility” checkboxes. Click Next to continue.

4. Under the “SAML Settings” , fill in the “Single Sign on URL” field with a properly formatted URL as a placeholder. **NOTE:** You will change this later after retrieving the applicable value from MetaDefender IT-OT Access.
5. Leave the box checked next to “Use this for Recipient URL and Destination URL”. Leave the box unchecked, next to “Allow this app to request other SSO URLs“
6. Fill in the Audience URI: eg “metaaccess-sp”
7. Default setting are fine for “Default Relay State”, “Name ID format”, “Application username”, and “Update application username on”
8. Skip the first “Name” and “Value” fields
9. Under “GROUP ATTRIBUTE STATEMENTS (OPTIONAL)”, fill in the “Name” and “Filter” fields.

   1. For “Name” enter whatever you want but save the value to use later in the MA UI”, eg: “groups”
   2. Under Filter , choose “Matches regex” and “.*”
   3. Advanced users may choose other options but it’s recommended to use these setting unless you’re very familiar with Okta.

10. Click “Next” to continue.

11. The next page is just feedback for Okta, and has no functional impact. You can choose “I'm an Okta customer adding an internal app”, then leave all the other fields blank and click “Finish”.
12. On the next page (under the “Sign On” tab), in the Info Box labeled “SAML 2.0” there is a link called “Metadata URL”. Click Copy, open new tab and paste that url, press Enter. Save as metadata.xml file you will import into MetaDefender IT-OT Acces

13. Log into your MetaDefender IT-OT Access Console at <https://www.opswat.com/products/metadefender/it-ot-access>.
14. Navigate to User Management > SSO > SDP and check “Enable Single Sign On”

15. Next to “Import configuration from XML Metadata file”, click “Choose File” and upload the “metadata” file you just downloaded from Okta. This should automatically fill in the “Current Certificate”, “Issuer”, and “IdP SSO URL” fields
16. In the “IdP Name” field, enter “Okta” or some other string. This is only for reference in the MetaDefender IT-OT Access UI.
17. Leave the Logout URL and Error URL fields blank

18. At the bottom, click “Add Group Attribute” and enter the value the value from the “Name” field in Okta. Presumably something like “group”.

19. Scroll to the top of the page, click “Save” and enter your MetaDefender IT-OT Access admin PIN
20. At the bottom of the page you will see a new value called “MetaDefender IT-OT Access Login URL”. Click “Copy to clipboard”

21. Switch back to Okta, click the “General” tab, scroll down to “SAML Settings” and click “Edit”

22. Click “Next” on the first panel

23. There will be a placeholder URL under “Single sign on URL”. Replace this with the URL you just copied from MetaDefender IT-OT Access.

24. Scroll to the bottom and click “Next” and then “Finish”

25. In the navigation bar on the top, mouse over Applications and click the Applications link. Then click the Gear icon next to the MetaDefender IT-OT Access app, and choose “Assign to Groups”.

26. On the groups panel, you can decide which groups you want to use for assigning SDP access in the MetaDefender IT-OT Access console. Click “Assign” next to each SDP user group. **Note:** You will need to record the selected group names for use in MetaDefender IT-OT Access. Please copy and paste the group names to minimize human error!
27. Click “Done.”

28. Navigate to the MetaDefender IT-OT Access console at [MetaDefender IT-OT Access](https://www.opswat.com/products/metadefender/it-ot-access), then go to User Management > IdP Groups, and click “Add”.
29. Fill in a group name you copied from Okta, enter your PIN and choose Add. Your new group will show up in the “IdP Groups” section.

30. Repeat for each SDP user group in Okta.
31. When you are ready to assign your new groups to protected applications, go to Secure Access > Protected Apps, click the “Assign” link next to your desired application(s)
32. On the “Assign End Users/IdP Groups to Protected Applications” Move groups “Available Users/Groups” to “Selected Users/Groups” to assign access, then enter your PIN again and choose Enter.

33. Log back in to the Okta console as an end user and click on the “MetaDefender IT-OT Access” application.
