<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/operating/workflows-page -->

# Workflows Page

Workflows can be created or edited on the Workflows page of the Kiosk Management Console. Workflows define sets of individual work behaviors for different users/groups/guests.

There are 3 workflow groups: Simplified, Employee and Guest group. Workflows in the Employee group requires authentication while the Guest and Simplified do not. Each group can be enabled or disabled but there must be at least one group enabled at a time. If Simplified group is enabled, Employee and Guest groups are disabled, and vice versa.

In each group, there must be at least one workflow enabled. The default workflows in each group are created and enabled by the installer. However, the default workflow in each group might be disabled after the upgrade to keep consistent to the settings of previous version. Any workflow can be edited even its group is disabled. Default WF in each group cannot be deleted, but editable.

**Note:** Workflows labeled with an "!" do not match with any existing Core workflow rules. You must select a corresponding MetaDefender Core in the [4.5. Selecting a Server to Process Files](/docs/mdkiosk/v4.8.5/operating/selecting-a-server-to-process-files) section.

For the Simplified group, only the Simplified workflow is created and set as the default workflow. See [How do I use Simplified workflow](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-use-simplified-wf) for more detail.

For the Employee group, each user or user group can join multiple workflows but only one workflow is selected for a session. Users that are not included in any workflows will be assigned to the Default. Each user or group can join multiple workflows but only one workflow is selected for a session. See [9.1. Logging In on the User Authentication Screen](/docs/mdkiosk/v4.8.5/operating/logging-in-on-the-user-authentication-screen) for more details

**Note:** Any users that are not included in one of the defined workflows will be assigned the Default workflow (if "Default login" is enabled).

For the Guest group, there is a bit different from the Employee. The administrator can create additional custom guest workflows but there must be either default guest workflow or customs are enabled. The default and custom guest workflow should never be both enabled at the same time.

Selfscan always uses the default workflow of Employee group in regardless of the group or the workflow is enabled/disabled.

## [Default workflows](/docs/mdkiosk/v4.8.5/operating/workflows-page#default-workflows)

| Name | Description |
| --- | --- |
| Simplified | Plug-and-play media scanning with automatic decryption and result display |
| Default | Users that are not covered by other workflows |
| Guest | Default when no other custom workflows active |

## [Creating a new workflow](/docs/mdkiosk/v4.8.5/operating/workflows-page#creating-a-new-workflow)

To create a new workflow, click **Create New Employee/Guest Workflow**. You will be guided through the process of creating a new MetaDefender Kiosk Workflow. After the workflow has been created, each step in the workflow can be edited independently. A newly created workflow is always disabled by default.

## [Cloning an existing workflow](/docs/mdkiosk/v4.8.5/operating/workflows-page#cloning-an-existing-workflow)

From MetaDefender Kiosk 4.8.1, administrators can easily clone existing workflow configurations directly within the Workflow page. This new feature streamlines administration by providing a one-click replication of all rules, engines, and UI customizations from a source workflow, eliminating the need for external tools. Upon cloning, users are prompted to assign a new name, ensuring consistency and reducing manual setup time for Employee and Guest workflow types.

## [Workflows after upgrade](/docs/mdkiosk/v4.8.5/operating/workflows-page#workflows-after-upgrade)

Any workflows existing in the previous (prior to 4.5.6) version must be kept the same after the upgrade. The previous version’s Default workflow must become Default in Employee group; The previous version’s Guest workflow must become default Guest in Guest group.

In a very particular case where the Default workflow of the previous version is selected in non-authentication mode, then after the upgrade to 4.5.6 or higher, that Default workflow of the previous version is cloned as a custom workflow in Guest group, with new name "Cloned" and set as the only one enabled. This particular behavior would keep same behavior after the upgrade to 4.5.6.

## [Select Default Login Method](/docs/mdkiosk/v4.8.5/operating/workflows-page#select-default-login-method)

Info

User Authentication Method

As of Kiosk 4.5.6, User Authentication has been moved from the Configuration page to Workflows page as a User Authentication Method link.

Since Kiosk 4.6.6, User Authentication Method has been renamed to Select Default Login Method

The Select Default Login Method link helps to configure and select default user authentication method.

### [Windows user login](/docs/mdkiosk/v4.8.5/operating/workflows-page#windows-user-login)

The Windows user login allows only local system users to log on Kiosk UI. The Kiosk administrator can choose whether to restrict the users by domain. If selected, only users on the same domain as the system are allowed to use MetaDefender Kiosk. If this is not selected, users will be able to enter authentication information for users on any domain as well as local system users.

*Windows user login option*

### [Remote Active Directory](/docs/mdkiosk/v4.8.5/operating/workflows-page#remote-active-directory)

The Remote Active Directory allows both local and AD users to do. The address of the remote Active Directory server, as well as user credentials to authenticate against the server are required. These credentials will be used to retrieve the list of users from the remote AD server for the purposes of assigning users to specific workflows.

Proper permission is required

*Add new Remote Active Directory*

Multiple Active Directories can be configured. Click `Add new` to add a server to the list and "Delete server" on the right hand side to delete the specific entry. The "Status" indicator will show in real time whether Kiosk is able to connect to the AD server. For "Server address", input can either be the IP or DNS name of the AD server; "<ip or dns name>:<port>". The default port 389 (636 if SSL is enabled) will be used if one is not supplied.

Warning

With KIOSK configuration in My OPSWAT:

- The port must be entered, even if it is the default one.
- The username must include the domain

Once SSL enabled, the server address should be in FQDN (Full Qualified Domain Name) format, for example:

*Adding second AD*

### [Single Sign-On](/docs/mdkiosk/v4.8.5/operating/workflows-page#single-sign-on)

The Single Sign-On allows users log in through a SAML IdP server which acts as the central authority for authenticating users and issuing security tokens.

- **Name:** Specify name of the IdP server
- **Choose Protocol Type:** SAML 2.0 is supported
- **Metadata URL**: used for fetching metadata of the IdP server
- **Identifier:** unique identifier generated by Kiosk that will be assigned to each **Relying Party Trust** (RPT)

The Kiosk administrator must configure Kiosk as one **Relying Party Trust** on IdP server to complete the integration.

Info

Kiosk UI **Relying Party Trust** format:

<http/https>://**localhost**:<port>/metadefender_rest/**uissologin**/saml/<identifier>

Please modify the elements enclosed in <> to match your Kiosk's configuration. It must be **localhost** for Kiosk UI login

See [Configuring ADFS as SAML Identity Provider](https://docs.opswat.com/mdkiosk/advanced-deployment/configuring-adfs-as-saml-identity-provider) for more detail to configure ADFS as SAML IdP.

The "Status" indicator will show in real time whether Kiosk is able to connect to the Idp server.

For the purposes of assigning SSO log in users to a specific workflow, the SAM (Security Accounts Manager) accounts of users need to be added manually to Properties & Membership of that workflow.

### [Custom Authentication](/docs/mdkiosk/v4.8.5/operating/workflows-page#custom-authentication)

If User Authentication enabled, the Kiosk administrator can choose between using the default MetaDefender Kiosk authentication or using a custom authentication module that has been installed on that MetaDefender Kiosk. For more information, see [11.1. Custom Authentication Module](/docs/mdkiosk/v4.8.5/advanced-deployment/custom-authentication-module).
