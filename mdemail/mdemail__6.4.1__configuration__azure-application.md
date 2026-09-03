<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/configuration/azure-application -->

# Registering Azure applications

To create an Azure application in Microsoft 365 for OAuth SMTP authentication for an Outbound/SMTP server profile or to integrate to for an Outbound/Microsoft365 server profile, perform the following steps.

## [Register application](/docs/mdemail/6.4.1/configuration/azure-application#register-application)

First, register the application performing the following steps:

1. Go to `portal.azure.com` and log in
2. Among *Azure services* click on *App registrations*

__

3. On the *App registrations* page click *New registration*

   1. Give a name to this new Azure application
   2. Set the account type to *Single tenant only*
   3. Click *Register* to commence the registration

4. You land on the page of the the newly created application
5. Click *Overview* and take note of the following properties:

   1. Client ID
   2. Tenant ID
   3. Client secret (not existing yet, created in the next steps)

## [Create client secret](/docs/mdemail/6.4.1/configuration/azure-application#create-client-secret)

Create the client secret performing the following steps:

1. Click on Add a certificate or secret

---

2. Select *Client secrets* and click on *New client secret*

3. Add a *Description* to the new secret and set the expiry
4. Click *Add* to add the new secret to the application

5. The value of the new *client secret* together with the *client ID* and the *tenant ID* will be used to configure oAuth or Graph API access in Email Gateway Security

## [Set application permissions](/docs/mdemail/6.4.1/configuration/azure-application#set-application-permissions)

Click on *Manage > API permissions*. By default only the *User.Read* permission is set.

The following permissions still need to be added taking the next steps:

1. In the *Select an API* dialog select *Microsoft Graph*

2. In the *Microsoft Graph* dialog select *Application permissions* then add the following permissions (the filter can help in finding them):

   1. For OAuth authentication in an Outbound/SMTP server profile:

      1. Mail.ReadWrite
   2. For delivering emails through Graph API in an Outbound/Microsoft365 server profile:

      1. Group.Read.All
      2. GroupMember.Read.All
      3. Mail.ReadWrite
      4. User.Read.All

3. These permissions may require admin consent so after selecting the permissions click on *Grant admin consent for <tenant name>*
