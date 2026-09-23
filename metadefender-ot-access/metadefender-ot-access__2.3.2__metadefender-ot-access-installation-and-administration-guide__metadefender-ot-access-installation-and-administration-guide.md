<!-- source: https://www.opswat.com/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide -->

[MetaDefender OT Access](https://www.opswat.com/docs/metadefender-ot-access/overview)Need Help?
# MetaDefender OT Access Installation and Administration Guide

The MetaDefender OT Access *Installation and Administration Guide* describes the procedures used to install and use the following MetaDefender OT Access components:

- Windows Client
- Windows Service Client
- Administration Graphical User Interface

#### [Who should read this](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#change-your-password-name-or-e-mail)

This guide is for system administrators and security engineers responsible for the security of an organization's network.

#### [Support](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#overview)

Contact OPSWAT support using:

- <<https://www.opswat.com/support>>

  - Online Chat
  - Global Phone numbers: [Contact Support - We Want to Hear From You - OPSWAT](https://www.opswat.com/support/contact-support)

## [Introduction](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#who-should-read-this)

MetaDefender OT Access™ is a remote access tool that provides a platform for publishing and monitoring connections between Remote Users and industrial assets. The software contains built-in tools for security and manageability.

MetaDefender OT Access features include:

- The ability to deploy in the Cloud or onsite
- The Cloud deployment has no required hardware and can be set up in one day or less.
- The onsite Management Console is easy to install. This deployment can also be set up in one day.
- Integrates with your Active Directory server for user and Security Group authorization
- Enables Policy Enforcement per user and per session
- Outbound-only connection from endpoint gateway to MetaDefender OT Access Cloud or Management Console, with no inbound firewall exceptions required
- Inexpensive and flexible pricing model on annual or monthly subscription
- Cloud components are hosted on Amazon Web Services (AWS) for maximum reliability and performance

#### [MetaDefender OT Access deployments](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#all-sites)

MetaDefender OT Access has two possible deployments:

- Cloud: OPSWAT manages MetaDefender OT Access configuration, including tasks such as uploading new software versions (personalities) and setting Management IPs.
- Onsite: The Management Console allows the customer to perform MetaDefender OT Access internal configuration tasks. All traffic inspection and policy enforcement are performed in the onsite server, making it suitable for offline deployments with no internet access.

Except for the Management Console, both deployments have the same functionality. You will receive the equipment, software, etc. appropriate to your deployment.

#### [Supported protocols](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#create-a-site)

Both MetaDefender OT Access deployments support various IT and OT protocols. Refer to Appendix B for a table of protocols and their associated policies.

#### [IT protocols](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#enable-or-disable-a-site)

The following IT protocols are supported on non-clientless services only:

- HTTP

The following IT protocols are supported on both clientless and non-clientless services:

- HTTPS
- RDP
- SSH
- Telnet
- VNC

#### [OT protocols](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#edit-or-delete-a-site)

OT protocols are supported on non-clientless services only.

- Ethernet IP
- FINS
- MODBUS
- OPCUA
- S7Comm
- SLMP

#### [MetaDefender OT Access components](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#active-directory)

MetaDefender OT Access components differ, depending on the deployment:

- Admin UI (onsite and Cloud): Configures and manages connections between the Remote User's primary computer and their OT Endpoint Devices.
- Windows Client (onsite and Cloud): Connect the Remote User's computer to the Cloud or the Management Console and ultimately to their OT Endpoint Devices.
- Windows Service Client (onsite and Cloud): Windows system-level service that can be used as an alternative to the Windows Client. The service launches automatically when the system boots.
- Management Console (onsite only): Performs MetaDefender OT Access internal configuration tasks. Refer to the *Management Console Guide* for more information.

#### [Order of Tasks](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#add-configuration)

MetaDefender OT Access installation and configuration require different tasks, depending on whether you are using the Cloud or onsite deployment.

**Cloud deployment**

1. Install and configure Windows Client or Windows Service Client on the Endpoint Gateway.
2. Install and configure Windows Client or Windows Service Client on the Remote User's computer. If the Remote User connects to clientless services only, this step is not necessary.
3. Log into the Admin UI to configure the connections between the Remote Users and their associated assets.

**On premise deployment**

1. Install and configure the Management Console. Refer to the [MetaDefender OT Access Management Console Guide; On premise deployment](/docs/metadefender-ot-access/2.3.2/management-console-guide/management-console-guide) *Management Console Guide*.
2. Install and configure Windows Client or Windows Service Client on the Endpoint Gateway.
3. Install and configure Windows Client or Windows Service Client on the Remote User's computer. If the Remote User connects to clientless services only, this step is not necessary.
4. Log into the Admin UI to configure the connections between the Remote Users and their endpoint devices.

## [Windows Client](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#support)

Windows Client connects the Remote User's computer to their OT Endpoint Devices through the Cloud or the Management Console.

**Important**

Install Windows Service Client if you plan to use the S7 or Ethernet IP protocol. Do not install Windows Client and Windows Service Client on the same system.

Important

Install Windows Service Client if you plan to use the S7 or Ethernet IP protocol.

Do not install Windows Client and Windows Service Client on the same system.

#### [Prerequisites](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#edit-active-directory-config)

- Windows 7 Professional Service Pack 1 or above
- If Windows 7 is used, install the following: .NET 4.5.2

You can install the Microsoft Security updates shown in "Windows Service Client" prerequisites, but this is not necessary.

- For Windows 7 OR Windows 10, download the **32-bit** version (even on a Windows 64 machine) of the VC_redist.x86 redistributable shown below, and select the appropriate Windows 7 or Windows 10 Binary:

Info

<<https://www.microsoft.com/en-us/download/confirmation.aspx?id=48145>>

- Administrators must have created Endpoint Owner or Remote User accounts.
- Before Remote Users can install Windows Client on their computers, Endpoint Owners must install Windows Client on the Endpoint Gateway and provide Remote Users access to services.

#### [Installation](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#test-active-directory-config)

Windows Client is installed on the Endpoint Gateway and on the Remote User's computer. If the Remote User only connects to clientless services, Windows Client needs to be installed on the Endpoint Gateway, but not the Remote User's computer.

You or your Administrator will receive a link through e-mail to download the _OPSWAT_Secure Access for *OT.msi* installer file. Close out all software before you start installation.

1. Double-click the installer file to start the program.
2. Accept the license terms.
3. Follow the instructions in the installer windows. Click **Finish** to exit the software.
4. Start the MetaDefender OT Access software through the desktop icon or your start menu.

#### [Enable Services (Endpoint Owners)](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#delete-active-directory-config)

Services provide Remote Users access to assets on endpoint devices at a site. These services are created on the Admin UI. Refer to "All Services" for more information.

The Endpoint Owner must enable services on the Endpoint Gateway before Remote Users can use the services to access the assets.

After starting the MetaDefender OT Access software, the following window displays. Complete the boxes and click **OK** to log in to the Windows Client.

OT Access Client (legacy)

MetaDefender OT Access Client

The Administrator supplies Endpoint Owners with identification to log on to the Windows Client. The software can send two-factor authorization (2FA), but OPSWAT recommends disabling 2FA for endpoints at trusted, unmanned locations.

Info

When a user account is created, 2FA is enabled and set to SMS by default. MetaDefender OT Access uses [Twilio](https://www.twilio.com/en-us/privacy) as provider for SMS sending. Only a superadministrator can change this value.

The username provided to the Endpoint Owner should be the same as the value selected for **Owner/Provider** when creating the service on the Admin UI.

The **Service Address** box displays only for onsite deployment. This IP address is used to connect the Gateway to the Management Console and must match the Service Address on the Console UI (refer to the *Management Console Guide* for more information).

The **Service Address** box remains populated with the value you entered, even if you log out of Windows Client. You can change the address if you wish.

**Important**

- If you change the address on the Management Console, you also need to change the address on Windows Client.

After clicking OK, Endpoint Owners will see any services that have been configured and assigned on the Admin UI. The services display the name, have an initial status of **Active**, and the address / port of the service.

Endpoint Owners can control how and when their services are available. Double-click the service name to disable the service.

The Endpoint Owner must remain logged on to the Endpoint Gateway for Remote Users to be able to access the services.

**Warning**

- OPSWAT recommends Administrators control service availability at the Admin UI, not at the local client.
- Firewalls and routing may block access to services between the endpoint and network perimeter.
- Endpoint Owner and Administrator must make sure the Endpoint Gateway can communicate with Endpoint Devices.

#### [Access services (Remote Users)](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#grant-access-to-active-directory-service)

This section does not apply if the Remote User is connecting to a clientless service.

*Prerequisites*

Before the Remote User can access the services:

Info

- The Service Owner must be logged into the Endpoint Gateway as the service owner/provider.
- The service must be enabled.

*Accessing services*

After starting the MetaDefender OT Access software, the following window displays. Complete the boxes and click **OK** to log in to the Windows Client.

OT Access Client (legacy) - Sign in for Remote users

MetaDefender OT Access Client - Sign in for Remote user (For example: remote_user)

The Administrator supplies Remote Users with identification to log on to the Windows Client. If 2FA is enabled, the software will send 2FA authorization to a cell phone number or email for the Remote User account.

The **Service Address** box displays only for onsite deployment. This IP address, followed by Port 443, connects the Remote User's machine to the Management Console. Type the Service IP configured on the Console UI. Refer to the *Management Console Guide* for more information.

The **Service Address** box remains populated with the value you entered, even if you log out of Windows Client. You can change the address if you wish.

Important

If you change the Service IP on the Management Console, you also need to change the Serivce IP on Windows Client.

The software shows the available services. For Remote Desktop Protocol (RDP, shown below), you can double-click on a service to initiate it. For all other services, such as Modbus, you must launch the client from your desktop because MetaDefender OT Access does not know which client the endpoint device operates.

Always connect to the LocalHost IP and Port so MetaDefender OT Access translates the IP and encrypts the transmission.

OT Access Client (legacy)

MetaDefender OT Access Client - Remote Services

**Notes**

- Endpoint Owners must make sure required application for the service exists and service is running.
- If you cannot see your Remote Service, but you are sure it is active and you have access, make sure the port is available on your machine. If the port is not available, you can tell the Administrator to change the port to Dynamic mode.

Enter your user name and password for this service. This identification can be different from your MetaDefender OT Access credentials.

After you click OK, the remote session initiates.

The Remote User account is connected to the remote machine through the RDP_Demo service.

When you complete your task, close the Remote Desktop Connection window.

## [Windows Service Client](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#introduction)

Windows Service Client is a Windows system-level service that can be used as an alternative to Windows Client.

The service launches automatically when the system boots, runs separately from any normal user space, and provides a persistent connection through MetaDefender OT Access to the services assigned to the Remote User.

***Important***

- Windows Service Client is required to use the S7 or Ethernet IP protocol.
- Do not install Windows Client and Windows Service Client on the same system.

*Prerequisites*

- Windows 7 Professional Service Pack 1 (SP1) or above
- If Windows 7 SP1, is used, the following must be installed:

.NET 4.5.2

Microsoft Security Updates:

- KB4474419 (SHA256): MUST HAVE: 64-bit. STRONGLY RECOMMEND: 32-bit
- KB4490628 (SHA256): RECOMMEND: 64-bit. STRONGLY RECOMMEND: 32-bit
- KB2901907 (.NET Framework 4.5.2)
- Windows Service Client may be incompatible with VPN software, such as Open VPN. Uninstall VPN software before installing Windows Service Client.
- For Windows 7 or Windows 10, download the **32-bit** version (even on a Windows 64 machine) of the VC_redist.x86 redistributable shown below, and select the appropriate Windows 7 or Windows 10 Binary:

Info

<<https://www.microsoft.com/en-us/download/confirmation.aspx?id=48145>>

- Administrators must have created Endpoint Owner or Remote User accounts.
- Endpoint Owners must have installed Windows Service Client on the Endpoint Gateway and provided Remote Users access to services before Remote Users can access services.
- Users installing the service in Silent or Passive mode must have elevated Administrator rights. On Windows 10, type 'cmd' in the search bar and select **Run as Administrator** from the option menu.

#### [Installation](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#saml-app-integration)

Windows Service Client is usually installed on the Endpoint Gateway and on the Remote User's computer. If the Remote User only connects to clientless services, Windows Service Client must be installed on the Endpoint Gateway but not on the Remote User's computer.

There are several ways to install Windows Service Client:

*Installer wizard*

The Endpoint Owner or Remote User can use the Wizard to install the client on the Endpoint Gateway or their computer. Download and double-click the *OPSWATMetaDefenderOTSvc.msi* file. Follow the instructions to install the service.

*Silent mode*

Administrators can use Silent mode to push the client to the desired location. This mode has no GUI. Open a command window and enter the following command:

msiexec SVC_USERNAME=username SVC_ PASSWORD=password LC_UPLINK=<IP address> /quiet /i "<pathway>\OPSWATMetaDefenderOTSvc.msi"

If you do not have elevated Administrator rights, the command will fail.

*Passive mode*

Administrators can use Passive mode to push the client to the desired location. In this mode, the installer displays a progress bar but doesn't ask any questions during install.

Open a command window and enter the following command:

msiexec SVC_USERNAME=username SVC_ PASSWORD=password LC_UPLINK=<IP address> /passive /i "<pathway>\OPSWATMetaDefenderOTSvc.msi"

If you do not have elevated Administrator rights, the system will ask for the privileges.

#### [Endpoint Owners](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#add-configuration)

Endpoint Owners can use Windows Service Client to monitor all services that have been configured and assigned on the Admin UI. The Endpoint Owner cannot make any changes to these services from Windows Service Client.

Double-click the icon to open the Windows Service Client GUI. The services display the name, have an initial status of **Active**, and the address / port of the service.

OT Access Client (legacy) - Provider Services

MetaDefender OT Access Client - Provided Services

**Warning**

- OPSWAT recommends Administrators control service availability at the Admin UI, not at the local client.
- Firewalls and routing may block access to services between the endpoint and network perimeter.
- Endpoint Owner and Administrator must make sure the Endpoint Gateway can communicate with Endpoint Devices.

#### [Remote Users](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#edit-configuration)

Remote Users can use Windows Service Client to monitor their available services and access RDP services.

Info

This section does not apply if the Remote User is connecting to a clientless service.

The Remote User can access any available services through the Windows Service Client on their computer. Double-click the icon to open the Windows Service Client GUI.

OT Access Client (legacy)

MetaDefender OT Access Client - Remote Services

The GUI shows the services available to the Remote User. For Remote Desktop Protocol, you can double-click on a service to initiate it. For all other services, such as the Modbus client, you must launch the client from your desktop because MetaDefender OT Access does not know which client the endpoint device operates.

Always connect to the IP and Port shown in the Windows Service Client, so MetaDefender OT Access translates the IP and encrypts the transmission.

Info

- Endpoint Owners must make sure the application for the service exists and the service is running.
- If you cannot see your Remote Service, but are sure it is active and you have access, make sure the port is available on your machine. If the port is not available, you can tell the Administrator to change the port to Dynamic mode.

Enter your username and password for this service. This identification can be different from your MetaDefender OT Access credentials.

After you click OK, the remote session initiates.

The Remote User account is connected to the remote machine through the service.

When you complete your task, close the Remote Desktop Connection window.

#### [View events](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#all-services)

Use Windows Services to view events related to MetaDefender OT Access.

When the service starts, a notification displays.

## [Log on to MetaDefender OT Access](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#metadefender-ot-access-deployments)

Before you start

- Users can only be added to a site by an Administrator or a Superadministrator.
- User names cannot be edited.
- Each user needs an email address and cell phone number for 2FA.
- Users must use Windows 7 to 10 operating system and a major internet browser such as Microsoft Edge, Internet Explorer, Chrome, or Safari.

1. Log on to the Admin UI with your organization's custom web link or the management IP configured. Enter your username, (usually your e-mail address) and your MetaDefender OT Access password.
2. Click **Continue**. If enabled, the 2FA verification code is sent to your cell phone number by SMS or your email account.
3. Enter the code where prompted.

The system locks out users after three unsuccessful logons. Speak to your system administrator to unlock your access.

#### [Change your password](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#clientless-services)

Click **Change Password** on the login page. The UI displays a message that an email has been sent to the email address of the logged-in user (if that user exists).

The email will contain a link to change the password. When the user receives the email, they will have 10 minutes to click the link and change their password.

#### [Inactivity timeout](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#create-service)

If you are logged into MetaDefender OT Access but are inactive for the period configured by a superadministrator, you are returned to the login page and must log into MetaDefender OT Access again.

#### [Access levels](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#edit-service)

MetaDefender OT Access has user, administrator (admin), and superadministrator (superadmin) access levels. The Admin UI primary page opens with links to the procedures that persons do most often and a menu pane that is specific to the access level:

- Superadmins see **Create a Site**, **View All Sites**, and **Create a User**
- Admins see **Create a Service**, **View All Services**, and **View My Services**
- Users see the **My Services** page

To open the primary page from any other page, click the **OPSWAT** logo in the menu pane.

The access levels define the tasks each level can do:

- Superadmin has access to all functions on all sites and instances
- Admin or site admin has access to most functions on an instance
- Users can change their personal information and use services that an admin or superadmin has assigned to them

While the levels have some overlap on some tasks, others show different information depending on your access level.

#### [Reset your password](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#delete-service)

1. Click on **Forgot your password** under the login boxes. If enabled, the **2FA verification code** is sent to your cell phone number through SMS or your e-mail account.
2. Enter the code where prompted.
3. Enter a new password in the **Change Password** page.
4. Enter the same password a second time to verify.
5. Click **Save**. The Welcome screen opens. Click **Sign In** to log on to the Admin UI.

#### [View license](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#grant-access-to-local-users)

On the *License* page, administrators can check the number of total user licenses purchased and number of licenses being used. If limits are reached, a warning is displayed.

## [My Account Settings](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#supported-protocols)

MetaDefender OT Access user profiles only contain a user's name and Personally Identifiable Information (PII) used for Two-Factor Authorization (2FA).

**Before you start**

- Only an admin or superadmin can change a user's cell phone number.
- All users can change their name, email address or password through their profile.

#### [Change your password, name, or E-mail](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#remove-user-access-to-a-service)

1. Log on to the MetaDefender OT Access Admin UI.
2. Click your name at the top right, and then click **My Account**. The *My Account Settings* page displays.
3. To change your password, click **Change** next to **Password**. Enter your current and new passwords. Click the **Save** button.
4. To change your name and e-mail address, click **Edit** next to **My Account Settings**. Enter your changes, and click the **Submit** button.

## [Overview](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#it-protocols)

Administrators have a comprehensive Dashboard to check the general status of the MetaDefender OT Access instance. In this dashboard, Administrators can check the live connections, pending requests and the Endpoint Gateway status among other information.

## [All Sites](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#ot-protocols)

A site allows you to group assets. After assets are added to a site, enabling or disabling the site will enable and disable all assets at the site.

**Before you start**

- Only superadmins can create, view, edit, or delete a site.

Click the **All Sites** menu to open the *Sites* pane. You can sort the data in each column or use the **Search** option to display sites containing a specified text string. Click a site name to view details for the site.

#### [Create a site](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#grant-access-to-active-directory-user)

1. Click the **Create a Site** button on the MetaDefender OT Access primary pane. The *Create a Site* pane displays.
2. Type information in all the boxes:

   1. **Site Name**: Alphanumerical name. This must be different from all other site names in your network.
   2. **Description**: Alphanumerical description. Refer to your regulations which can include the physical location or other information.
   3. **Enabled**: If checked, the site will be online and running as soon as it is made. If you plan to enable this site later, then uncheck this box.
3. Click the **Create the Site** button. The *Sites* pane displays the new site in the table.

#### [Enable or disable a site](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#service-groups)

You can create a site and then enable it later. You can also disable a site to prevent users from connecting to it. MetaDefender OT Access does not protect disabled sites.

1. Click the **All Sites** menu. The *Sites* pane displays.
2. In the **Enabled** column, check or uncheck the box for each site you want to change. A banner at the top of the page displays briefly if successful.

#### [Edit or delete a site](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#create-service-group)

1. Click the **All Sites** menu and click on the site you want to change. A detail pane displays.
2. To edit the site, open the **Action** menu and click **Edit**. The *Edit a Site* pane displays. Edit the values as necessary. Click the

**Save your changes** button. A banner at the top of the page displays briefly if successful.

3. To delete the site, open the **Action** menu and click **Delete**. A banner at the top of the page displays briefly if successful. The site is removed permanently.

## [Active Directory](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#metadefender-ot-access-components)

You can create or manage a Remote User's connection to a customer's Active Directory Server, allowing authentication and authorization of all users of the Admin UI.

Info

- Only superadmins can perform Active Directory tasks. Admin and regular users will not see the Active Directory settings in the Admin UI.
- After an Active Directory is configured, admins and superadmins can grant access to Active Directory services and groups.
- Okta can also be used as an Identity source for LDAP authentication. To setup Okta’s LDAP Interface follow the instructions provided on the Okta help center: <https://help.okta.com/en-us/Content/Topics/Directory/LDAP-interface-main.htm>. Specific values required to fill in the configuration can be found here: <https://help.okta.com/en-us/Content/Topics/Directory/LDAP-interface-connection-settings.htm>. Attention should be paid to the values of “Hostname” and “Username” for your Okta organization as they will be required for the configuration of the “Server” and “Username” fields, respectively. MetaDefender OT Access does not support LDAPS on port 636, however StartTLS on port 389 provides an encrypted communication between Okta and MetaDefender OT Access.

A service must be created using the Active Directory Server IP and port **389** (LDAP). The OPSWAT_services account must be granted access to the created service (refer to "Grant access to Active Directory service"). Click the **Active Directory** menu to open the *Active Directory Config* pane.

#### [Add configuration](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#edit-service-group)

Only one configuration is allowed. Once that is added, the **Add Config** button disappears.

1. Open the **Active Directory** menu and click the **Add Config** button. The *Create New Active Directory Config* pane displays.
2. Type values in the following boxes (examples shown):

   1. **Server**: localhost (Connects to Active Directory service used by the OPSWAT_services account)
   2. **Port**: 3389
   3. **Base**: Base search domain for your AD, such as DC=OPSWAT, DC=local
   4. **User Search DN:** DN of the users, such as CN=Users, DC=OPSWAT, DC=local
   5. **Admin Group**: If a user is a member of this group, the user will be granted administrator rights. For example, CN=Secure OT Access Admins, CN=Users, DC=OPSWAT, DC=local
   6. **Username:** Valid Active Directory user
   7. **Password:** Password assigned to the user name
   8. **Okta LDAP Interface:** Check this box if you are using Okta’s LDAP Interface to provide authentication

#### [Edit Active Directory Config](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#delete-service-group)

1. Open the **Active Directory** menu and click on the server row. A detail pane displays.
2. Open the **Action** menu and click **Edit**. The server's Active Directory Config page displays.
3. Edit the values as necessary.
4. Click the **Submit** button.

#### [Test Active Directory Config](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#grant-access-to-user)

This test verifies a user's information is in the Active Directory. The test simulates the user's access and displays the results.

1. Open the **Active Directory** menu and click on the server row. A detail pane displays.
2. Open the **Action** menu and click **Test**. The *Active Directory Test* pane displays.
3. Enter the username and password for the user access you want to test.
4. Click the **Test** button. The results display in the lower box.
5. Click the **Clear Results** button to delete the results information in the box.
6. Click the **Return** button to return to the Active Directory Config pane.

#### [Delete Active Directory Config](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#grant-access-to-active-directory-user)

1. Open the **Active Directory** menu and click on the server row. A detail pane displays.
2. Click **Delete**. If successful, a banner briefly displays at the top of the pane and the All Services page opens. All information about the configuration is removed.

#### [Grant access to Active Directory service](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#users)

Refer to "All Services" for information on granting access to the Active Directory service.

## [SAML App Integration](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#order-of-tasks)

You can create or manage a Remote User's connection to a customer's IdP Identity provider (Ex: Microsoft Entra ID, Okta ...) allowing authentication and authorization of all users of the Admin UI.

Info

- Only Superadmins can perform SAML App Integration tasks. Admin and regular users will not see the SAML App Integration settings in the Admin UI.
- After an SAML App Integration is configured, admins and Superadmins can grant access to SAML App Integration services and groups.

#### [Add configuration](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#create-user-account)

Only one configuration is allowed. Once that is added, the **Add Config** button disappears.

1. Open the **Single Sign-On (SSO)** menu then switch to **SAML App Integration** tab and click the **Add Config** button. The *Create New* SAML App Integration *Config* pane displays.
2. Type values in the following boxes (examples shown):

   1. **Import configuration from XML Metadata file**: Import metadata file provided from Identity provider
   2. **Application Name**: Name of your Application is associated with your app which registered in IdP.
   3. **SAML version**: SAML protocol version ( 2.0 by default).
   4. **IdP SSO URL:** Login URL in IdP ( auto fill after importing metadata file).
   5. **Logout URL**: Logout URL in IdP ( auto fill after importing metadata file).
   6. **Reply URL (Assertion Consumer Service URL):** The URL where OTA handles the SAML response. ( normally the Management IP or the DNS ) . Then you will need to copy this URL and paste it in your IdP configuration.

#### [Edit configuration](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#edit-user-account)

1. Open the **Single Sign-On (SSO)** menu then switch to **SAML App Integration** tab. A detail pane displays.
2. Open the **Action** menu and click **Edit**. The server's SAML App Integration Config page displays.
3. Edit the values as necessary.
4. Click the **Submit** button.

## [All Services](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#windows-client)

A service allows a user to access an asset.

Click the **All Services** menu to open the *All Services* pane. A superadmin or admin will see a list of the services a user can be invited to connect to. A user will see all services they can connect to. You can sort the data in each column or use the **Search** option to display services containing a specified text string. Click on a service to view details for that service.

#### [Clientless services](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#disable-user-account)

A Remote User can reach a clientless service through the Admin UI without having Windows Client or Windows Service Client installed on their primary computer although one of the clients must be installed on the Endpoint Gateway.

Clientless services display a **Connect** button in the **Browser access** column on the *All Services* pane. A Remote User can click this button to access the associated service.

To configure a clientless service, click the **Browser Access** checkbox when creating a service (see below) and enter the correct values on the "Settings" pane.

If you use clientless services with the onsite deployment and HTTPS protocol, you must perform additional configuration. Refer to "HTTPS clientless services" for more information.

#### [Create service](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#audit-user-activity)

Info

A superadmin can create a service on any instance. An admin can create a service on their sites.

1. Open the **All Services** menu and click **Create a Service**. The *Create a Service* pane displays.
2. Type values in the following boxes:

   1. **Service Name**: Required; a unique name for each instance.
   2. **Owner/Provider**: Required; the MetaDefender OT Access user who will expose services.
   3. **Site**: Required; Select from the list of sites that you administer.
   4. **Browser Access**: Click to configure the service as a clientless service. If you click this checkbox, the **Remote Client Port** box disappears.
   5. **Protocol**: Required; Your service's protocol. If you click *Browser Access** and select **RDP or VNC**, a group of **Clientless Settings** boxes and a **Screen Recording** checkbox display. Perform the following tasks:

      1. Enter the Remote User's username and password.
      2. Select the method the Remote User will use to connect to the service. The default is **NLA**.
      3. Click the **Ignore Cert** checkbox if you want them to be able to connect without an SSL certificate.
      4. Click **Advanced configuration** to configure how the clientless service will display on the Remote User's computer. You can configure keyboard layout, resize method, height, width, color, and DPI.
      5. Click **Screen Recording** to enable screen recording for the service within an Onsite deployment. If enabled, the activity of any user who accesses this service will be recorded. Refer to "Screen recording" for more information.
      6. Remote Client Port: Required unless you click **Browser Access**; Port the Remote User connects to. A default value is set for the protocol selected in the dropdown but can be changed.
   6. **Policy**: In some protocols like MODBUS, you can apply policies to prevent service consumers from writing on the provider side. Refer to Appendix B for a table of protocols and their associated policies.
   7. **Enforcement Mode**: Policies can be **Enforced** or can **Report** violations of the policy.
   8. **IP Address or Hostname**: Required; corresponding to the machine providing the service.
   9. **Service Port**: A value is automatically selected depending on the service protocol selected but can be changed.
   10. **Description** (optional).
   11. **Enable Scheduling**: You can set time slots for when the service is enabled. Out of these slots, the service won't be available.
   12. **Schedule Timezone :** Select the time zone of the endpoint.
   13. **Schedule Start**: A calendar pops up; select the desired start date (as YYYY-MM-DD) and time (in 24-hour format), then click Apply.
   14. **Schedule End**: A calendar pops up; select the desired end date (as YYYY-MM-DD) and time (in 24-hour format), then click **Apply.**
   15. **Schedule Hours**: Select the hour that you want the service to run the within dates selected. Midnight (12:00 AM) equals 0, and 11:00 PM equals 23.
   16. **Schedule Week Days**: Select the day or days that you want the service to run within the dates selected. Monday equals 1, and Sunday equals 7.
   17. **Schedule Month Days**: Select the calendar day that you want the service to run within the dates selected. The first day equals 1, and the last day varies with the month. If you specified week days, make sure that the week days and month days correlate.
   18. **Schedule Months**: Select the months that you want the service to run within the dates selected. January equals 1, and December equals 12.
   19. Enabled: You can manually enable or disable the service by this checkbox. Default value is Enabled.
   20. **Group**: You can assign the service to a group of services. See "Service Groups" for more information.
3. Click the Create Service button. If successful, banner briefly displays at the top of the pane.

Info

All Scheduling fields are optional, but if a field is left blank, the service will run constantly for that period. For example, if you set the dates from January 1 to May 31, with the hour as 3 but leave week day blank, the service will run at 3:00 AM every day. If you set the week day as 1-5, then the service will run at 3:00 AM on Monday-Friday only.

Once a service is created, it displays in *All Services* for administrator views and *My Services* for user views.

#### [Edit service](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#delete-user-account)

Info

A superadmin can edit a service on any instance. An admin can edit a service on their sites.

1. Open the **All Services** menu and click a record. A detail pane displays.
2. Open the **Action** menu and click **Edit**. The *Edit a Service* pane displays.
3. Edit the values as necessary.
4. Click the **Save your changes** button.

#### [Delete service](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#grant-access-to-a-service-or-a-service-group)

1. Open the **All Services** menu and click a record. A detail pane displays.
2. Open the **Action** menu and click **Delete**. The *All Services* pane displays with the service removed. All information about the service is removed from the system.

#### [Grant access to local users](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#totp-multi-factor-authentication-method)

You can grant one or more local users access to a specific service. You can also grant an admin access to edit or delete a service.

1. Open the **All Services** menu and click the desired record. A detail pane displays.
2. Open the **Action** menu and click **Grant Access to Local User**. The *Grant Access to Local User to Service* pane displays.
3. Select a user from the **Grant Access To** list. You can also start typing a user name in the **Grant Access To** box to narrow the search. You can select multiple users, one at a time, by repeating this process for each user.
4. Click the **Grant Access** button to provide access to all selected users. A banner indicating status briefly appears at the top of the page, and the Service detail page opens.

#### [Remove user access to a service](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#endpoint-gateways)

1. Open the **All Services** menu and click a record. A detail pane displays.
2. Click the **X** beside the user you want to remove from this service.

#### [Grant access to Active Directory user](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#connections-dashboard-and-live-session-monitoring)

You can grant an Active Directory user access to a specific service. You can also grant an Active Directory admin access to edit or delete a service.

Info

If you have not configured Active Directory, you will see "Grant Access to a User".

1. Open the **All Services** menu and click a record. A detail pane displays.
2. Open the **Action** menu and click **Grant Access to Active Directory User**. The *Grant Access to Active Directory User to Service* page opens.
3. Select a user from the **Grant Access To** list.
4. Click the **Grant Access** button. A banner indicating status briefly displays at the top of the page, and the Service detail pane displays.

## [Service Groups](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#prerequisites)

A service group allows you to associate a user with multiple services at one time. Granting a user access to a service group automatically grants the user access to all services in the group.

Info

You must have admin or superadmin access to do Service Group tasks.

Click the **Service Groups** menu to open the *All Service Groups* pane. You can sort the data in each column or use the **Search** option to display service groups containing a specified text string. Click a service group to display details for the group.

#### [Create service group](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#screen-recording)

1. Open the **Service Groups** menu and click the **Create a Service Group** button. The *Create a Service Group* pane displays.
2. Type information in the boxes:

   1. **Service Group Name:** A specific name for this instance
   2. **Description**: Text that can tell the administrator of the request purpose
   3. **Site:** Select from the list of sites that you administer
3. Click the **Create the Group** button. A green banner across the top of the pane indicates success.

After creating a Service Group, use the **All Services** menu to add new or existing services to the group. Refer to "All Services" for more information.

#### [Edit service group](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#enable-screen-recording)

1. Open the **Service Groups** menu and click a group name. A detail pane displays.
2. Open the **Action** menu and click **Edit**.
3. Edit the values as necessary.
4. Click the **Save your changes** button. A green banner across the top of the pane indicates success.

#### [Delete service group](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#user-warning)

1. Open the **Service Groups** menu and click a group name. A detail pane displays.
2. Open the **Action** menu and click **Delete**. The *Service Groups* pane displays without the service group. All information about the service group is removed from the system.

#### [Grant access to user](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#custom-recording-policy)

1. Open the **Service Groups** menu and click a group name. A detail pane displays.
2. Open the **Action** menu and click **Grant Access to User**. The *Grant Access to Service Group* pane displays.
3. In the **Grant Access To** box, select the user.
4. Click the **Grant Access** button. A green banner across the top of the pane indicates success.

#### [Grant access to Active Directory user](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#view-recordings)

1. Open the **Service Groups** menu and click a group name. A detail pane displays.
2. Open the **Action** menu and click **Grant Access to Active Directory User**. The *Grant Access to Active Directory User to Service Group* pane displays.
3. In the **Grant Access To** box, select the user.
4. Click the **Grant Access** button. A green banner across the top of the pane indicates success.

## [Users](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#installation)

A superadmin can add, edit, audit, or delete users on any site; an admin can add, edit, audit, or delete users on the site they administrate. Users can view the list of services assigned to them and change their profile content.

Info

- At least one site must be created before creating users.
- Only a superadmin can create and perform tasks on admin or superadmin user accounts.

Click the **Users** menu to open the *Users* pane. This pane displays all users currently on a site for admins or on an instance for superadmins. You can sort the data in each column or use the **Search** option to display user information that contains a specified text string. Click a user account to view details for that user.

#### [Create user account](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#export-recording)

1. Open the **Users** menu and click the **Add User** button.
2. Type information in all the boxes:

   1. **Username:** Must be unique across all sites in an instance. This value cannot be changed once it is saved.
   2. **Email:** Must be unique across all sites in an instance.
   3. **First Name** of user.
   4. **Last Name** of user.
   5. **Cell Phone Number** of user, including the country code with a +, but without spaces or additional symbols. Example: +19195555555
   6. **Site** the user will be assigned to; multiple sites are supported (admins can only choose from sites that they administer).
   7. **Password and Password Confirmation** for the user.
   8. **Preferred Notification Service for Windows Client**: Choose None, Email, SMS or TOTP from the drop-down menu for 2FA. The default value is **SMS** and can only be changed by a superadmin. If you are creating an account for an Endpoint Owner, we recommend you select **None**.
   9. **Preferred Notification Service for MetaDefender OT Access Website**: Choose None, Email, SMS or TOTP from the drop-down menu for 2FA. This value default value is **SMS** and can only be changed by a superadmin. If you are creating an account for an Endpoint Owner, we recommend you select **None**.
   10. Check **Superadministrator** or **Administrator** for the access level; Only superadmins can create superadmin or admin users. If neither is checked, the default is **User**.
3. Click the **Submit** button. A green banner at the top of the pane indicates success. The *Users* pane displays.

#### [Edit user account](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#delete-recording)

1. Open the **Users** menu.
2. Click a user. A detail pane for the user displays.
3. Open the **Action** menu. The options vary depending on your access levels. Click **Edit**.
4. Edit the values as necessary. You cannot edit the Username.
5. Click the **Submit** button. A green banner across the top of the pane indicates success.

#### [Disable user account](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#my-services)

When you create a user account, it is enabled by default, and the user can access the remote services. If you disable the account, the user still exists in MetaDefender OT Access, but cannot perform any of the following tasks:

- Login to the Admin UI or Windows Client
- Access services through MetaDefender OT Access
- Create requests
- Do admin or superadmin operations

1. Open the **Users** menu.
2. Click a user. A detail pane for the user displays.
3. Open the **Action** menu in the detail pane and click **Edit**.
4. Click to clear the **Enabled** checkbox on the user detail pane.
5. Click the **Submit** button.

You can re-enable the account by clicking the **Enabled** checkbox in the user detail pane.

#### [Audit user activity](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#see-your-services)

The **Connected Since** column on the *Users* pane displays the date and time the user connected to a system through MetaDefender OT Access.

#### [Delete user account](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#log)

1. Click the **Users** menu.
2. Click a user. A detail pane displays.
3. Open the **Action** menu and click **Delete**. A green banner at the top of the page indicates success. All information about the user is deleted.

#### [Grant access to a service or a service group](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#see-logs)

Info

A superadmin can grant access to any service across all sites. An admin can grant access to the sites that they administer.

1. Open the **Users** menu.
2. Click a user. A detail pane for the user displays.
3. Open the **Action** menu and click **Grant Access to Service** or

**Grant Access to Service Group**.

4. Select a service or group from the **Grant Access To** menu and click the **Grant Access** button. A green banner at the top of the page indicates success. The User detail pane displays the name of the service or service group beside **Service Access** or **Service Group Access**.

#### [TOTP Multi Factor Authentication method](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#export-logs)

The first time a user tries to use the TOTP MFA method for login, he/she needs to include the user and password as normal at the login page. If the credentials are correct, the following page is displayed.

Once the user enters the correct 6-digit code, he/she will be requested to enter credentials again. From now on, the user will be requested to enter the 6-digit code displayed in the Authenticator app selected

Warning

OPSWAT recommends TOTP apps supporting SHA-2 family of hashing algorithms.

## [Endpoint Gateways](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#enable-services-endpoint-owners)

The Endpoint Gateways section provides the administrators with comprehensive information of the Endpoint Gateways they have in place.

Clicking on the Services column will deploy a list of the current services served by that Endpoint Gateway.

Administrators can also Enable/Disable the Endpoint Gateways by using the Enable toggle.

## [Connections Dashboard and Live Session Monitoring](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#access-services-remote-users)

The Connections Dashboard shows the active connections hosted by the MetaDefender OT Access instance.

Info

- Superadmin and Admin can view the Connections Dashboard.
- Live Session monitoring is only available for clientless service.

Click the **Connections Dashboard** menu to display the Dashboard.

The dashboard displays the following information for each connection:

- **Site**: Name of the site hosting the connection
- **Service**: Service the connection is reaching
- **Provider**: Name of the owner of the service
- **Username**: User accessing the connection
- **Start date**: Date the connection was initiated
- **Stop Date/Remove Access**: Displays a **Remove Access** button. Click this button to end the connection for the user and revoke user access to the service.
- **Live monitor:** Display the **Access** button. Click this button to access and view users' session with live monitoring.

Use the **Show** dropdown list to configure the number of entries displayed on the dashboard. If the dashboard contains more than one page of entries, use the **Previous** and **Next** buttons to move through the entries. You can sort the data in each column or use the **Search** option to display entries that contain a specified text string.

## [Screen recording](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#windows-service-client)

MetaDefender OT Access can be configured to record user activity for any clientless service that uses the RDP, VNC or SSH protocolt. After screen recording is enabled for a service, all user activity that occurs after connecting to that service is recorded and stored.

Info

- Only a superadmin can enable and disable screen recording, configure storage parameters, and access recorded sessions.
#### [Enable screen recording](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#remote-syslog)

Click the **Screen Recording** checkbox on the "Create service" or "Edit service" pane to enable screen recording for that service.

#### [User warning](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#requests)

When a user accesses a service where screen recording is enabled, a pop-up displays, stating their session is being recorded. The user must click **Yes** before they can connect to the service.

#### [Custom recording policy](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#request-access-to-a-service)

A company can set a custom recording policy for an RDP or VNC service. A superadmin can use the **Custom Recording Policy** option on the "Settings" pane to enter the URL for the policy. A link to the URL will display on the warning the user sees when they connect to the service, and the user can click the link to view the policy.

#### [View recordings](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#resolve-a-service-request)

Use the **Screen Recordings** menu to view a library of recorded sessions.

OPSWAT sets a maximum size of 50G for all screen recordings (exported and non-exported). This value cannot be changed. The available space displays at the top of the *Screen Recordings* pane.

The following information is displayed for each recording:

- Site where the service is located
- Service Name
- User who accessed the service
- Date the service was accessed
- Length of the service

#### [Export recording](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#settings)

Select a recording and click the **Export** button to export the recorded session as an encrypted .*m4v* file. When you click the button, a popup displays that allows you to set the **Resolution** and **Bitrate** for the recording. Selecting a lower resolution and bitrate reduces the space taken up by the exported recording.

Warning

Remain on the Screen Recordings pane until the export completes. Leaving the pane halts the export.

If you leave the *Screen Recordings* pane before an export completes, the export halts and the amount of space used by the recording increases. Click the **Clean** button to delete the incompletely exported file (the original recording is not deleted). You can then click the **Export** button to export the recording.

#### [Delete recording](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#access-requests)

To delete the original recording, select it, click the **Delete** button, and confirm your action.

## [My Services](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#installation)

My Services lists the services that a user has been assigned to. Users without administrator access will only see the services they have access to; they cannot edit or delete the services.

Admins can click a service and edit or delete it for themselves, and can grant, edit, and delete other users' services for the sites that they administer.

Superadmins have access to all services and sites on an instance. They do not have a separate My Services page; they can access their services by clicking **All Services,** and any changes there will affect all users.

#### [See your services](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#clientless-service-domains)

1. To see the services that you can access, click the **My Sites** menu.
2. The *My Services* page shows a table with the following columns:

   1. **Name:** Service name
   2. **Owner username:** Username of the service owner
   3. **Policy:** If a policy is applied to this service, the policy name shows
   4. **Enforcement Mode:** The choices are None, Enforce, Report
   5. **Address:** IP Address
   6. **Port:** Port used to make this connection
   7. **Group:** Group name if the service is part of a group
   8. **Site:** Site that this user is assigned to

## [Log](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#endpoint-owners)

A superadmin can view or export system-log (syslog) events.

Click the **Syslog** menu to open the *Syslog* pane. This pane displays a list of system-log (syslog) events. You can use the **Search** option to display events that contain a specific text string.

#### [See logs](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#siem-integration)

1. Open the **Log** menu. The *Syslog* pane displays.
2. Select a value from the drop-down menu by **Show entries** to set the number of logs displayed on a pane. The default is 25.
3. Click **Refresh** at the top left corner to refresh the Syslog entries.
4. Type text in the **Search** window in the top right corner to search the logs.

#### [Export logs](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#mft-integration)

1. Open the **Log** menu. The *Syslog* pane displays.
2. Click the **Export** button. A popup displays. You cannot change the file name of the export.
3. Choose to **Open** or **Save** the file.
4. All MetaDefender OT Access syslogs download to the designated folder on your current computer. For Windows, the default folder is the *C:\Users<username>\Download folder*.

#### [Remote syslog](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#secure-file-transfer-with-mft)

OPSWAT does not provide a permanent archive of log messages. However, you can create a service that allows you to access MetaDefender OT Access syslog data on a syslog server that you maintain on your own network. This server allows you to build your own archive of log messages.

Follow the steps in "Create service", and use the following values for the parameters:

- **Owner/Provider:** User providing the remote syslog service.
- **IP:** IP address of the syslog server you want to access remotely.
- **Port:** Port of the syslog server you want to access remotely.

After setting up the service, you can use it to access the remote syslog on your network.

## [Requests](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#remote-users)

A local user can request access to a service for a specified period. An administrator must approve or reject the request.

Click the **Requests** menu to open the *All Requests* pane. You can sort the data in each column or use the **Search** option to display requests containing a specified text string. Click the request to display details for the request.

#### [Request access to a service](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#metadefender-core-integration)

1. Open the **Request** menu. The *All Requests* pane displays.
2. Click the **Create a Request** button. The *Create a Request* pane displays.
3. Type information in the boxes:

   1. **Consumer**: User who is making the request
   2. **Service**: Select the desired service
   3. **Description**: Text that can tell the administrator of the request purpose
   4. **Enable Scheduling**: If the box is checked, you can see the time boxes

Info

All fields are optional, but note that if a field is left blank, the service will run constantly for that period. For example, if you set the dates from January 1 to May 31, with the hour as 3 but leave week day blank, the service will run at 3:00 AM every day. If you set the week day as 0,1,2,3,4, then the service will run at 3:00 AM on Monday-Friday only.

- Schedule Timezone: Select the time zone of the endpoint
- **Schedule Start**: A calendar pops up; select the desired start date (as YYYY-MM-DD) and time (in 24-hour format), then click **Apply.**
- **Schedule End**: A calendar pops up; select the desired end date (as YYYY-MM-DD) and time (in 24-hour format), then click **Apply**
- **Schedule Hours**: Select the hour that you want the service to run within the dates selected. Midnight (12:00 AM) equals 0, and 11:00 PM equals 23.
- **Schedule Week Days**: Select the day or days that you want the service to run within the dates selected. Monday equals 0, and Sunday equals 6.
- **Schedule Month Days**: Select the calendar day that you want the service to run within the dates selected. The first day equals 1, and the last day varies with the month. If you specified week days, make sure that the week days and month days correlate.
- **Schedule Months**: Select the months that you want the service to run within the dates selected. January equals 1, and December equals 12.

4. Click the **Create a Request** button. The *All Requests* pane displays with your request's Resolution showing as Pending. You can see the request details when you click a cell in the row. An email is sent to the administrators for the requested service and to you.

An administrator must approve the request. If the request is approved, you can access the service only on the dates and times that you requested.

#### [Resolve a service request](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#scanning-files-with-metadefender-core)

You must have admin or superadmin access to approve service requests.

1. Open the **Request** menu. The *All Requests* pane displays.
2. Find the service request from the user listed in your email notice.
3. Click in the request row to see details of the request. If the request meets your organization's requirements, click the **Accept** button. If the request is not acceptable, click the **Reject** button.
4. The *All Requests* pane displays with the new Resolution status. The system sends an email to you and the requester with your decision.

## [Settings](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#view-events)

Info

Only a superadmin can change the settings for an instance.

Use the *Settings* pane to change the following:

- **User login max attempts**: Number of attempts a user can make before being locked out of the account
- **Custom Recording Policy**: URL of the customer's recording policy. This URL displays on the warning message the user sees when they access a service where "Screen recording" is enabled.
- **Timeout**: Default inactivity timeout for the Admin UI. You can set any value between 5 -- 120 minutes, in 5-minute increments. If there is no activity for this period, the user is returned to the login page and must log in to MetaDefender OT Access again.
- **Clientless HTTP Domain:** Subdomain used to manage clientless services. Type this value ONLY if you are using clientless services with onsite deployment and the HTTPS protocol.
- **Login logo**: Logo that displays on the MetaDefender OT Access login pane. Files must have a .*png* or .*jpg* format.
- **Clientless Service Port**: Port number from which clientless services will be automatically assigned.
- **Side Menu logo**: Logo that displays above the side menu. Files must have a .*png* or .*jpg* format.
- **Cookie Domain**: Top-level domain. This box is related to the certificate you create for the HTTPS protocol and must include the subject/CN of your certificate. Type this value ONLY if you are using clientless services with the onsite deployment and the HTTPS protocol.
- **Small Side Menu logo**: Logo that displays beneath the Side Menu log. Files must have a .*png* or .*jpg* format.
- **Clientless IP:Port**: IP address and port number for clientless services. The IP address value should correspond to the Management IP or the corresponding URL if assigned in the DNS server. For onsite deployments, this value is automatically populated with the Management IP that was configured on the Management Console. Refer to the *Management Console Guide* for more information.

Click the setting you want to change. An edit pane displays where you can make the change. Click the **Submit** button. A green banner at the top of the page indicates success.

### [Access Requests](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#inactivity-timeout)

A superadmin would be able to require service scheduling to be active when performing a service request. In configuration menu, superadmin can enable that requirement and also define a maximum duration limit for those requests.

### [Clientless service domains](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#access-levels)

If (and only if) you are using clientless services and the HTTPS protocol, you must enter values for the **Clientless HTTP Domain** and **Cookie Domain** settings. The **Clientless HTTP Domain** and **Clientless IP:Port** are subdomains of the top-level **Cookie Domain**.

All three values must incorporate the same URL. You must also create an entry for this URL on your internal DNS server. If you do not create this entry, the user will not be able to log in to the Management Console.

An example of the domain settings when clientless services and the HTTP protocol are used is shown in the following graphic.

### [SIEM Integration](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#reset-your-password)

Use the SIEM Integration tab to configure MetaDefender OT Access to forward logs to your SIEM solution.

Info

So far Splunk is the supported SIEM solution

Use Enable SIEM Integration toggle to configure it:

- **SIEM provider:** Only Splunk can be selected.
- **Server:** IP of the Serer where the logs will be forwarded.
- **HEC token:** HEC uses this token to authenticate inbound connections.
- **Port:** Default value is 8088.
- **Interval:** Default value is 60 seconds.
- **Index:** Sets the index to store events from this input.
- **Host:** Hostname for the machine originating the events, in this case MetaDefender OT Access instace.
- **Source type:** Sets the sourcetype key/field for events from this input.

Use the Test Connection button to check connectivity with the SIEM system

### [MFT Integration](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#view-license)

Use the MFT Integration tab to configure MetaDefender OT Access to work with an MFT (**MetaDefender Managed File Transfer**) instance.

- **Server URL:** URL or IP of the **MetaDefender Managed File Transfer** instance.
- **API Key:** API Key generated in the MFT instance, used for authentication.
- **Service Group:** Members of the selected Service Group will be provided with permission to Upload files.
- **Remove MFT user on user deletion:** Mark this checkbox to remove the users from MFT instance when the user is removed from OT Access.

Warning

Please notice that if you change the API Key in the MFT instance, users created with the old API Key become invalid.

The MFT user is created using the OTA user ID and its site ID. If an OTA user is unable to upload files to the MFT server, the issue may be due to a duplication of the MFT guest user with a local user on the MFT server. In such cases, please remove this local user on MFT Server.

#### [Secure File Transfer with MFT](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#appendix-a--https-clientless-services)

Remote Users can transfer files to a configured MFT instance and eventually to a shared folder linked to an RDP service.

Info

An MFT instance with MDCore is required for file transfer and multi-scanning.

To use this feature, follow the next steps:

1. Create a RDP service to be linked with MFT instance. To do that, when editing the service select MFT Service in the Group drop down list and check the Enable SMB checkbox. Indicated the shared folder in the indicated field.
2. Assign this service to the remote user
3. Then, when the remote user Upload a file by clicking on the Update button a pop-up will appear. Fill in the fields:

4. **File:** Choose the file to be uploaded
5. **Transfer service:** in the dropdown list, select the service previously configured, if it is correclty configured, shared solder, user and password fields would be automatically populated.
6. **Shared Folder:** folder defined when creating the service.
7. **Username/Password:** credentials from the user with permission to read/write the shared folder.

Once populated, click on Submit button and the file will be delivered in the configured folder after scanning.

### [MetaDefender Core Integration](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#my-account-settings)

Remote Users will be able to send files to a configured MetaDefender Core instance configured for file multiscanning.

Info

A MDCore instance is required for multi-scanning.

In this manual we will address how to configure MetaDefender OT Access to work together with a MetaDefender Core instance and how remote users can upload files to the MDCore instance. For more details on MetaDefender Core, please click [here](https://www.opswat.com/docs/mdcore).

To configure an MDCore instance, follow the next steps:

1. Click on Settings -> Integration and go to the MetaDefender Core tab
2. Click on Add MetaDefender Core button
3. Fill in the form:

   1. **Server Name:** MetaDefender Core instace server name.
   2. **Server Address:** IP Address of the MetaDefender Core instance.
   3. **API Key:** Input here the API Key generated from MeaDefender Core. For more details on API Key generation, please click [here](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-generate-an-api-key-on-the-core-deployment-).

4. Click on Test Connection button and once tested, click on Add button to save the changes.

#### [Scanning files with MetaDefender Core](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#configuration-process)

Users will be enabled to upload files to the MetaDefender Core instance where they will be scanned for malware.

To do so users simply need to go to My Files section in the left side menu and click on **Upload** button.

The following pop up will appear so the user can select the file to be uploaded.

Once uploaded, the file status will remain Pending until a Site admin or Superadmin approves it, thus it won't be able to be downloaded until the file is approved.

A file analysis report can be consulted once the file is Pending or Approved. To do that, click on the file name.

## [Appendix A HTTPS clientless services](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#log-on-to-metadefender-ot-access)

Info

This section applies only if you are using clientless services with onsite deployment and the HTTPS protocol.

*Prerequisites*

- One top-level domain. This value will correspond to the **Cookie Domain** value on the *Settings* pane.
- Two subdomains: one for the Console UI and one for the HTTPS clientless services.
- *Clientless IP:Port** and* ***Clientless HTTP Domain*** *values,* pane.
- A specific certificate for each subdomain or one wildcard certificate that is valid for both subdomains

#### [Configuration process](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#configure-domains)

Perform the following procedures to configure clientless services with the HTTPS protocol.

*Configure internal DNS server*

Configure your internal DNS server with the top-level domain and subdomains to associate the Management IP with the subdomains you create. This procedure will vary, depending on your network configuration.

*Associate certificates*

Create a signed certificate for the HTTPS protocol and associate the certificate with the Management Console and Administration GUI. You will perform this process on the Management Console. Refer to "SSL/TLS Credentials" in the *Management Console Guide* for these procedures.

#### [Configure domains](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#appendix-b-protocols-and-policies)

Configure domain values on the *Settings* pane. Refer to "Settings" and "Clientless service domains" for more information.

## [Appendix B Protocols and policies](/docs/metadefender-ot-access/2.3.2/metadefender-ot-access-installation-and-administration-guide/metadefender-ot-access-installation-and-administration-guide#change-your-password)
