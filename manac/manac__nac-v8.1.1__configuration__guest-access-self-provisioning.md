<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning -->

# Guest Access Self Provisioning

Overview

NAC provides three models for guest access as follows:

**Single Click Anonymous Access**: User agrees to an AUP and is given immediate access. No identifying information is collected. **Help Desk Sponsorship**: The guest user account is manually created by the help desk or a guest access administrator. Identity information is collected and validated. **Self-Provisioning**: The guest user provides all necessary information. Account creation is automated. Self-provisioning can be optionally configured to require approval.

The purpose of this document is to introduce you to the configuration and operation of the self-provisioning model of the Guest Access module. This document will provide all the information needed to fully configure your Guest Access module. This document will also step you through how a user will request and receive the credentials needed to access your guest network. This document assumes that standard URLs will be used. If a branded deployment is in use, please refer to the appendix for information on branded URLs.

The NAC Guest Access Module provides a self-provisioning user portal to allow guests to request and receive credentials to access the Guest Network without helpdesk involvement. Administrators can configure one or more Self-Provisioning Guest Profiles. Each administratively configured Provisioning Profile controls the default network access, notification and approval requirement, account “Time to Live” duration, and other policies of guest accounts created through the self-provisioning portal.

Provisioning Profiles allow administrators to configure which information users will be required to provide in order to receive their credentials from the NAC system. This information includes valid email address, full name, reason for requested access, mobile phone number and mobile phone carrier. The email address or mobile phone number is required to deliver the credentials to the user. If this information is not authentic, they will have no way to receive their credentials and thus, no way to access the guest network.

All user information is visible and editable by an administrator through the Guest Access Management page on the NAC Dashboard. Access to this page can be delegated and can be limited to “view only” or “edit”. This allows an event coordinator, RA, librarian, receptionist or any other person to whom policy administrators wish to delegate this responsibility the ability to view/add/edit/delete guest users without granting them access to the overall NAC dashboard.

Administrators have the ability to choose from one or more of four approval methods, depending on the level of control required and the requirements of each profile:

- Instant approval with no credential validation required
- Validate guest Information with no Administrative notifications
- Validate guest Information with a notification sent to designated administrators
- Approval required with a notification sent to designated administrators

## [End User Experience](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#end-user-experience)

## [Self-Provisioned Guest Access Overview](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#self-provisioned-guest-access-overview)

The guest user starts out by connecting to the network and is directed to an authentication page with information about guest access. In this scenario, the guest user clicks on the ‘Guest Account’ button and is redirected to an enrollment portal:

If multiple profiles are present, the user is presented with a list of profiles to choose from. If the user already has an account, they can request their credentials be resent by entering their email address. If only one profile is present, this page will not be displayed to the end user.

The guest user fills out the enrollment form, providing a valid name, e-mail, reason, cell phone and cell phone carrier, and then clicks on the ‘Submit Information’ button.

The guest user is redirected to a page notifying them about how their login credentials will be validated and that a message will be sent to them via text message or email.

The guest user will receive a text message containing their username and password either immediately, or upon validation depending on whether approval is automatic or manual, and whether or not the text message and/or email is configured to be sent. In the event the guest user does not have text messaging capabilities, the password can be provided to the user by the help desk. Once the guest user has their credentials, they can return to the authentication page and login.

## [Administrator Self-Provisioning Approval Overview](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#administrator-self-provisioning-approval-overview)

The self-provisioning approval process will vary depending on the guest access model that is in use by NAC

- **Instant** – The user is asked to enter their personal information but gains instant access to the network with no need to sign in. The user will still appear in the Guest User Dashboard module. If configured, credentials can be sent via SMS or email for future logins.
- **Validate** – The guest user account is immediately created and no notification is sent to administrators. The guest user will have their credentials sent to them by text message or email. The user will still appear in the Guest User Dashboard module.
- **Validate and Notify** – The guest user account request is automatically approved. The guest user will have their credentials sent to them by text message or email. If the guest user does not have text messaging capabilities, they can call the help desk. The help desk can find the username and password via the Guest User Dashboard module. An email is sent to administrators alerting them of the granted notification request. If necessary, an administrator can revoke enrollment via a link in the email or via the administrative ‘Guest Access’ dashboard module.
- **Approval Required** – If approval is required for guest user access, an email is sent to administrators alerting them of the pending request. Administrators can then click on the link in the email to approve a request. Alternatively, administrators can click on a link to deny the user request. The user will be sent their login information based on the configured profile.

## [Guest Manager](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#guest-manager)

The ‘Guest Manager’ portal shows all enrollment requests. Pending and existing requests can be edited by clicking on the Pencil icon under the Modify column:

To allow guest access and send the user a notification:

1. Change the State to ‘Active’
2. Choose the Notification Method
3. Click on ‘Save’

At this point a notification with login credentials will be sent to the guest user via text message and email. If the guest user does not receive the notification, they can call the help desk using the phone number that was displayed when they submitted their request.

## [Configuration](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#configuration)

## [Email Configuration](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#email-configuration)

Guest User Self-Enrollment requires email for sending notifications. Steps to configure email can be found [here](/docs/manac/nac-v8.1.1/operating/email-setup).

## [Profile Configuration](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#profile-configuration)

The configuration for Guest Access can be found in the ‘Self Enrollment Portals > Guest Profiles’ section of the system configuration page (<https://portal.myweblogon.com:8443/manage/#/configuration/GuestSelf-ProvisioningSetup> or your branded URL). In a cluster environment, ensure that this is completed on the manager node. Upon opening the page, an administrator will see the following screen. To add a new profile, click on the “Create new profile” button.

When adding a new profile, the following form will be presented. A Guest Profile Name and Display Name should be entered. To make the profile available, the “Profile Enabled” checkbox will need to be checked.

### [Required Information](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#required-information)

Guest access requires an email address for all guest profile types. NAC uses this as a unique identifier. Additional items can be required, optional or hidden from the “Required Guest Information” section.

Optional items will be displayed on the registration page but can be left blank when submitted.

### [Role Management](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#role-management)

Guest profiles can optionally be associated with one or more user roles. Roles can later be used as qualifiers when assigning the user to a policy group. If there are no roles available, new roles can be added by going to Configuration Manager>Self-Enrollment Portals>Guest and Device Roles>Create new role.

*Note: If a Contextual Intelligence Publisher integration exists, the guest profile role(s) will be published as part of the information about guest user devices.

### [Account Lifecycle](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#account-lifecycle)

Setting the account lifecycle will determine when an account is active and when it expires. The account lifecycle section also determines how many times an account can be renewed or how long a user has to wait before they can create a new account with the same email.

1. Start Date – When the account becomes active

   1. If “Start at Activation” is checked, new accounts are active immediately
   2. If “Start at Activation” is NOT checked, a starting date and time must be chosen
2. Expiration Options

   1. If “Never Expire” is chosen, new guest account will be active until they are manually de-activated or deleted.
   2. If “Expire In” is chosen, a duration must be set for the length of time the account will be active. This is the most commonly used expiration option. If renewals will be allowed, the number of renewals allowed and the duration renewed accounts will be good for must also be set.
   3. If “Expire At” is chosen, a specific end date and time must be selected. “Expire At” is not typically used with renewals, however, if this option can still be configured with the option for renewals. Renewals will always follow the “Expire In” method.
   4. If the account has an expiration, it is recommended to check the “Revoke access upon account expiration” checkbox. If this is not checked, the guest users authentication will expire based on the authentication frequency set on the guest user authentication policy.
3. Lockout Duration

   1. After an account expires and there are no renewals remaining, setting a lockout duration will prevent the user from registering a new guest account with their email. If no lockout duration is required, this value should be set to “0”.

### [Messaging](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#messaging)

The Guest Access Module comes with notification/validation settings. The notification options have four validation levels explained below:

- **Instant** – Once the guest user account is created it is immediately active and no validation response is needed from the administrator. The Administrator is not notified via email that the account was set up. The guest user account will show up in the Guest User Management Page and can be modified or deleted by an Administrator. The guest user will automatically be authenticated and will receive a text message or email for future logins.
- **Validate** – Once the guest user account is created it is immediately active and no validation response is needed from the administrator. The Administrator is not notified via email that the account was set up. The guest user account will show up in the Guest User Management Page and can be modified or deleted by an Administrator. The guest user will be required to authenticate using credentials that are emailed and/or text messaged to them.
- **Validate & Notify** – Once the guest user account is created it is immediately active. A notification email is sent to the configured administrative notification email address. The administrator can revoke access via a link in the email. The guest user account will show up in the Guest User Management Page and can be modified or deleted by an Administrator. The guest user will be required to authenticate using credentials that are emailed and/or text messaged to them.
- **Approval Required** – Once the guest user account is created it is inactive. A notification email is sent to the configured administrative notification email address with the option to accept or decline the account. The guest user account will show up in the Guest User Management Page and can be modified or deleted by an Administrator. The administrator also has the option to activate the user from the Guest User Management Page. The guest user will be required to authenticate using credentials that are emailed and/or text messaged to them.

The end user notification method can be chosen. End user notifications should include the username and password.

- **Email** – Sends credentials using an email only
- **SMS** – Sends credentials using a text message only
- **All** – Sends credentials using both an email and a text message
- **None** – End users will not receive their credentials – This option should only be used with “Instant” or “Approval Required” validation levels.

Both a Notification and a Sender email address is required for email and text message notifications to work properly. These addresses must be different.

**NOTE**: If required, please ensure that the sender address is valid in your directory structure.

For each messaging option, templates can be edited with custom content for the notifications sent to both the end user and/or administrators. If a template is not applicable the notification methods selected, it will be greyed out in the interface. The legend contains variables that can be used within each email template. Before emails can be sent, a Sender email and an Admin Email must be populated. The Admin email is a requirement regardless of whether or not Admin notifications are enabled. The Admin Email field can contain multiple email addresses separated by a semi-colon (;).

NOTE: The $URLApprove, $URLDeny variables should only be included in Administrator notifications.

### [Security](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#security)

Guest user profiles contain two additional options to prevent users from frivolously creating guest accounts.

- **Prevent clients from becoming guests** – When this option is selected, users who have previously passed a NAC Authentication Policy with LDAP credentials will not be able to create a guest account from a device where they have previously authenticated using their LDAP credentials.
- **Prohibited email domains** – This option will prevent users from creating a guest account using a specific email domain. This is helpful for keeping valid LDAP users from using their corporate/institution email accounts to create guest accounts as well as preventing the use of disposable email addresses.

## [Policy Manager Configuration](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#policy-manager-configuration)

### [Guest Authentication Page](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#guest-authentication-page)

If your guest users will be logging into your production network, you can simply add the ‘Guest Account’ button to your normal authentication page. Newer installations will already have this button present. If your guest network will be separate from your secure network, you will need to create a separate authentication page for it. This can be done by simply creating a copy of your normal authentication page, renaming it, and attaching it to the new Policy Group that will authenticate your guest users. This is done through the Policy Manager.

After logging into the Policy Manager, perform the following steps:

1. Click on the “Messaging” tab to open the Custom Messaging interface
2. Select your normal authentication page from the left-side menu
3. Click on “Create a Copy”
4. Give your new authentication page a name (i.e. “Guest Authentication”)
5. Give an optional description if you wish
6. Click “OK” to save the new page

The next step is to add the Guest Account button to your authentication page. Perform the following steps to add the Guest Account button to the appropriate authentication page:

1. Select the appropriate authentication page from the drop down menu at the top center of the screen
2. Download the JSP file for the web message.
3. Add the following code at the end of the source code above the last “</div>” statement if not already present:

<br />
<br />
<div class="optionText optionButton primText03 compBack01" onclick="location.replace(/guest');">
<div class="bigger">GUEST ACCOUNT</div>
(Request guest access)
</div>

1. The URL can used to redirect users can be customized based on the organizations' requirements

   1. <https://portal.myweblogon.com:8443/guest> will redirect users to a page where they will be required to select a specific guest user profile
   2. If the desire is to direct users to specific profile rather than have them choose, the URL should be replaced with <https://portal.myweblogon.com:8443/guest?action=selectProfile&guestProfileId=1>. The guestProfileId parameter should be replaced with the Profile Id corresponding with the desired profile.
2. Click the “Upload and Preview” button to see how the page will look

   1. The location of the button code may need to be adjusted to ensure proper placement on the screen
   2. Once the page is complete, click “Upload and Save"

### [Guest Access Policy Group](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#guest-access-policy-group)

It will be necessary to create a Guest Access Policy Group to authenticate your guest users. The decision whether or not to enforce policy or require the guest user to install the Policy Key is totally up to you. Please refer to NAC documentation for the creation of the policy group. Key factors to keep in mind when creating this policy group include:

1. Network Qualifier set to IP address Range or Subnet of the guest network
2. Device Qualifier set to the devices that guest will be bringing
3. **Optional** Identity Qualifier set to the Role assigned by the Guest Profile
4. Policy Container must have an Authentication Policy

   1. Authentication Policy must be set to use the Guest User DB or a chain that includes the Guest User DB.
   2. Authentication Message should have the guest registration button. The default Authentication Message is already configured with the guest registration button.

Once the Guest Access Policy Group is created click the “Apply and Use” button in the Policy Manager.

## [Appendix](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#appendix)

- Guest User Self-Provisioning Portal:

  - Standard: <https://portal.myweblogon.com:8443/guest>
  - Branded example: [https://nac.customer.edu:9443/guest](https://metaaccessnac.customer.edu:9443/guest)
- Administrative Links:

  - Standard: <https://portal.myweblogon.com:8443/manage/#/configuration/GuestSelf-ProvisioningSetup>
  - Branded example: [https://nac.customer.edu:9443/manage/#/configuration/GuestSelf-ProvisioningSetup](https://metaaccessnac.customer.edu:9443/manage/#/configuration/GuestSelf-ProvisioningSetup)
- Notes:

  - In a clustered deployment, please reference the manager IP address.
  - The standard default port is 8443, however, in a branded deployment it will default to 9443.

## [Manually Creating Guest Users through the dashboard](/docs/manac/nac-v8.1.1/configuration/guest-access-self-provisioning#manually-creating-guest-users-through-the-dashboard)

In some cases, it may be desirable to manually create guest users through the Guest Manager.

To reach the guest manager click the triple bar menu in the top left of the NAC UI and select "Guest Manager". From here, click the “Add User" button to create a new user.
