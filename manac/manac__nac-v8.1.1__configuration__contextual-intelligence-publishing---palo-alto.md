<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto -->

# Contextual Intelligence Publishing - Palo Alto

## [**Overview**](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#overview)

Using Contextual Intelligence Publisher (CIP), Single Sign-On can be enabled for Palo Alto and non-managed devices. Once configured, end users will no longer need to authenticate to Palo Alto since the user credentials will be passed transparently from CIP. Integrating the two allows seamless identity-aware firewalling and greater ease of use for matching firewall traffic to individual users. The CIP integration currently provides the following values to Palo Alto:

- Machine IP Address
- Username
- Domain (If user is on a Domain machine AND NAC is set up for Domain Member single sign-on)

The purpose of this guide is to walk through the configuration requirements for sending identity information from CIP to Palo Alto.

Prior to working through this document, Palo Alto and NAC must be installed and functional on the network. CIP must also be installed in the NAC system.

## [Configure Palo Alto](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#configure-palo-alto)

## [Create a Role for NAC](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#create-a-role-for-nac)

In the Palo Alto Console navigate to “Device Tab[Symbol]Administrative Roles” and create a new Admin Role with then name “SCAPI” and a description. The new profile needs only “User-ID Agent” enabled in the XML API tab as shown in the screenshots below:

Once the Role is created, it will appear in the list as shown below:

## [Create a User for NAC](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#create-a-user-for-nac)

The next step is to create a new user with the name “ NAC ” and ensure that the password is recorded. Navigate to “Device Tab > Administrators” and create a new administrator. Change the “Role” radio button to “Role Based and then assigned the “SCAPI” profile that was just created as seen in the screenshot below.

Once the user is created, it will be displayed in the Administrators list as show below. Ensure that the change is committed before moving to the next section.

## [Enable User-ID for network Zones](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#enable-user-id-for-network-zones)

Before Palo Alto will accept identity information, “User Identification” must be enabled for the zones where it will be used. To enable “User Identification”, navigate to “Network > Zones” and choose the interface(s) to enable. After choosing the zone, select the “Enable User Identification” checkbox.

Click on “Commit” to save all changes to the running configuration

## [Generate the XML API key](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#generate-the-xml-api-key)

In a web browser navigate to the URL (Substitute <PALO_ALTO_IP> with the actual IP address of the Palo Alto appliance and substitute <PASSWORD> with the password created above):

https://<PALO_ALTO_IP>/api/?type=keygen&user=SafeConnect&password=<PASSWORD >

The results will look similar to this:

Record the API key for use in the next section. Page Break

## [Configure Contextual Intelligence Publisher](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#configure-contextual-intelligence-publisher)

Once API access has been configured on Palo Alto, navigate to the NAC Configuration at <https://portal.myweblogon.com:8443/manage> ([portal.myweblogon.com](http://portal.myweblogon.com/) can be replaced by the manager IP or a branded URL) and choose “Contextual Intelligence.” Click on “Add” and enter the following information:

- **Publisher:** Palo Alto
- **Name:** A name to describe where CIP is publishing Data.
- **URL:** The URL of the Palo Alto appliance ( https://<PALO_ALTO_IP>/api/ ?)
- **Publish Interval:** 1000ms is sufficient for most deployments
- **API Key:** The API key from the previous section
- **Include HIP Report:** This includes additional information, such as device type, in the export. Some Palo Alto license levels will cause the API message to be completely dropped if this is the case. This checkbox can be unchecked if only basic identity is needed or if there are problems receiving the API messages on the Palo Alto side.

Once everything is entered, click “Save”. Once save, data will start being published to Palo Alto.

## [Verify Integration](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#verify-integration)

The integration can be validated by navigating to “Monitor > Logs > Traffic” from the Palo Alto interface. In the search field, search for “user.src neq ‘’”. The results will show all log entries that include a username.

Once the integration is complete, the username will be populated in all the logs, including Traffic, Threat, URL Filtering, and WildFire subscriptions. Logs will only be present for a module if there is a valid license.

***Note:** For the purposes of validating the integration, “null” is considered a username. If no username is present the username column will simply be blank.

## [Troubleshooting](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#troubleshooting)

## [Not receiving updates](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---palo-alto#not-receiving-updates)

If Contextual Intelligence Publisher does not appear to be updating username information after following the steps above, the NAC appliance may need to be added as a permitted IP for the management interface. To add NAC as a permitted IP, navigate to “Device > Setup > Management > Management Interface Settings”. Once open, ensure the following items are present:

- HTTPS is checked
- All three User-ID flags are checked
- The NAC IP (Manager node in a cluster environment) is in the list of permitted IP addresses.
