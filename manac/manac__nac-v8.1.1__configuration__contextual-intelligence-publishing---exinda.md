<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda -->

# Contextual Intelligence Publishing - Exinda

## [Overview](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda#overview)

Using Contextual Intelligence Publisher (CIP), Exinda can be used to assign identity (role) and ownership based policies for devices on a per-user basis. Once configured, device data will be passed transparently to Exinda from CIP in real-time. The CIP integration currently provides the following device attributes to Exinda:

- IP Address (current IP of the device the user is connecting from)
- Username
- Group Memberships (LDAP groups or NAC specific groups)
- Domain (If user is on a Domain managed device AND NAC is set up for Domain Member SSO)

The purpose of this guide is to walk through the configuration requirements for sending identity and ownership information from CIP to Exinda.

Prior to working through this document, Exinda and NAC must be installed and functional on the network. CIP must also be installed in the NAC system. Before CIP can publish domain machine specific information, NAC must be deployed with either the AD Connector plugin or the Policy Key.

## [Configure Exinda](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda#configure-exinda)

## [Locate Exinda AD Service settings](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda#locate-exinda-ad-service-settings)

Navigate to Exinda’s AD Service Settings by selecting Configuration and then choose “Network” under the “System” settings. Finally, choose the “Active Directory” tab. Once there, ensure that the service is running and make a note of the Listen Port. If the service is not running, click “Restart” to enable the listener service.

## [Locate the Admin user account](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda#locate-the-admin-user-account)

To locate the user accounts page, navigate to Configuration and choose “Authentication” under the “System” settings. Finally, choose the “Local Users” tab. The ‘admin’ user account must be used for the integration.

## [Configure Contextual Intelligence Publisher](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda#configure-contextual-intelligence-publisher)

Once the admin username and Listen Port have been verified on Exinda, the details can be entered into the Management Console of NAC on the “Identity Publisher” Tab. Navigate to https://<*NAC__Appliance* IP>:8443/ManagementConsole (In a cluster environment, this will be the manager node).

On the Identity Publisher tab, complete the following:

- Choose “Exinda” from the Publisher dropdown.
- Enter a Name to describe where CIP is publishing Data.
- Enter the ‘admin’ user Password.
- Enter the URL will be in the format of https://<FQDN_or_IP_of_Exinda>:<Exind_Listen_Port>. Be sure to use the Listen Port number identified in Exinda’s Active Directory settings.

When finished, click “Save”. After saving, CIP will immediately begin publishing identity data to Exinda as new sessions begin.

## [Verify Integration](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda#verify-integration)

## [Check the Users & Groups Object in Exinda](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda#check-the-users--groups-object-in-exinda)

Before starting any troubleshooting, determine the state of the users in Exinda by checking the User & Groups objects to see if expected users and groups are being populated from CIP. To locate the Users & Groups objects, navigate to Configuration and choose “Users & Groups” under the “Objects” section.

The “Network Users” tab will display user names that have been populated by CIP. CIP will provide usernames for BYOD and Guest users in addition to Domain users. Domain users can be identified by the domain name in parenthesis, while BYOD and Guest users will not have a domain name in parenthesis.

The “Network Groups” tab will display group names in the same fashion as users.

## [Creating Identity-Based Policies in Exinda](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---exinda#creating-identity-based-policies-in-exinda)

Once all setup steps have been completed, policy in Exinda will need to be set up such that authenticated users have different policy rules than unauthenticated users.

For information on how to set up policy for this purpose, read Integrating Exinda with your Captive Portal available at <http://docs.exinda.com/ga-released/exos/7.0/help/Default.htm#ExOS/common-use-cases/captive-portal.htm>.
