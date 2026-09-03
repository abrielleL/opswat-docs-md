<!-- source: https://www.opswat.com/docs/mdmft/configuration/integrate-with-active-directory-federation-services -->

# Integrate with Active Directory Federation Services

Summarize Page    Connect to Cursor Connect to VS Code Info

Integration with Active Directory Federation Services (AD FS) as Single Sign-On (SSO) provider is available for AD FS servers running Windows Server 2016 AD FS or Windows Server 2019 AD FS.

Below is a step-by-step tutorial on integrating Active Directory Federation Services IdP with MetaDefender Managed File Transfer using the OpenID Connect protocol.

1. Open the "Server Manager Desktop App" and go to "Tools" → "AD FS Management."

2. Inside the "AD FS Management" app go to "Application Groups" → "Add Application Group."
3. Enter a descriptive name for the application group and select the "Server application accessing a web API" template.

4. To find the "Login redirect URI:"

   1. Go to the MetaDefender Managed File Transfer™ web console and navigate to "Settings" **→** "Single Sign-On."
   2. Turn on "Enable Single Sign-On."

c. If the AD FS server uses a self-signed certificate, it may be necessary to enable "Ignore Certificate Issues."

d. Disable "Load User Profile" as AD FS 2016 and newer do not support calling the "/userinfo" endpoint.

e. Set the "Authority" to the AD FS URL, which can be composed by appending "/adfs" to the AD FS server’s fully qualified domain name (FQDN).

f. Set the "IP Address or Domain" to the location of the Managed File Transfer instance. Once this information is provided, Managed File Transfer will automatically generate the "Redirect URI."

g. Copy the "Redirect URI" and past it back into the AD FS Application Settings (step 5).

5. Add the copied URI to the list of known redirect endpoints, and save the "Client Identifier" for future use.

6. Generate a client secret by selecting the "Generate a shared secret action" and copy the generated GUID for future use.

7. Add the client identifier (generated at step 5) to the list of known clients.

8. Select the users allowed to authenticate. For this tutorial, all users will be allowed.

9. Configure the allowed scopes. The following selections are mandatory:

   1. **openid** → Enables the OpenID Connect protocol
   2. **profile** → Receives the user’s name related claims (upn, display_name, first_name, last_name)
   3. **email** → Receives the user’s email claim (necessary for administrator role asignment)
   4. **allatclaims** → Allows profile and email related claims to be included in the identity token, as AD FS does not support loading profile-related claims from the userinfo endpoint

10. After completing the setup, the newly created application group should be displayed in the "Application Groups" list.

11. The final step on the AD FS server side is attribute to claim mapping. Double-click the newly created application group and edit the Web API.

12. Go to the "Issuance Transform Rules" tab and click "Add Rule…."
13. Select the "Send LDAP Attributes as Claims" template and click "Next."

14. Select "Active Directory" as an "Attribute store" and create the following mappings, recognized by MetaDefender Managed File Transfer:

    1. **upn** (required)
    2. **email** (required)
    3. **name** (optional)
    4. **given_name** (optional)
    5. **family_name** (optional)
    6. **phone_number** (optional)

15. Click "Finish" and "Apply."
16. In Managed File Transfer, input the "Client ID" (created at step 5) and "Client Secret" (created at step 6).

17. If the "Client ID" and "Client Secret" are misplaced, they can be retrieved by accessing the application group’s affiliated server application.

18. Add relevant "Administrator Emails" to designate which users should be granted administrator rights, and add the "allatclaims" scope to "Integration Scopes."

19. Once all configurations are complete, click "Update."

## [Testing the Integration](/docs/mdmft/configuration/integrate-with-active-directory-federation-services#testing-the-integration)

To test the integration:

- Log out of MetaDefender Managed File Transfer™.
- A new "Sign In with SSO" button appears on the login page.

- Click "Sign In with SSO" to be redirected to "Active Directory Federation Services" to login. Once logged in, you will be redirected back to MetaDefender Managed File Transfer™.
