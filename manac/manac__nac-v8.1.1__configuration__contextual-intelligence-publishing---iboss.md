<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---iboss -->

# Contextual Intelligence Publishing - iBoss

## [Overview](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---iboss#overview)

Using Contextual Intelligence Publisher (CIP), Single Sign-On can be enabled for iboss and non-managed devices. Once configured, end users will no longer need to authenticate to iboss since the user credentials will be passed transparently from CIP. This integration provides the following values to iboss:

- Machine IP Address
- Username
- Machine Name
- Group Memberships (Active Directory or NAC specific)

The purpose of this guide is to walk through the configuration requirements for sending identity information from CIP to iboss.

Prior to working through this document, iboss and NAC must be installed and functional on the network. CIP must also be installed in the NAC system.

## [Configure iBoss](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---iboss#configure-iboss)

Prior to configuring CIP, iboss must be configured to allow API access. When enabling API access, a 'NAC Name' and key will be generated for use by CIP.

From the iboss home screen, click on the “Network > AD Plugin” item from the navigation pane.

Note the Security Key and the Port number on this screen. These values will be used with CIP.

Toggle the Enable to "Yes" and click "Save".

Under the Registered AD Servers/NAC Agents, click "Add" to create a new entry. Enter the desired 'NAC Name' in the name field and the IP address of the NAC appliance. In a cluster, this will be the manager node. The 'NAC Name' will be used with Contextual Intelligence Publisher.

When finished, click the 'Save' button.

To validate the iboss configuration, create a second nac agent following the steps above. For the second nac agent, use the IP address of your local workstation. From your local workstation, the configuration can be validated by entering the following URL in a web browser:

<http://IBOSS_IP_ADDRESS:8015/nacAgent?action=clientInfo&dc=NACNAME&key=IBOSS_API_KEY&ip=VALID_ENDPOINT_IP>

Replace the following:

- **IBOSS_IP_ADDRESS:** The IP address of the iboss appliance
- **NACNAME:** the Nac Name that was used to add NAC as a Nac agent in iboss
- **IBOSS_API_KEY:** The iboss security key
- **VALID_ENDPOINT_IP:** The IP address of an active endpoint

If everything is configured correctly, a "SUCCESS" response will be returned with details of the client associated with the specified endpoint IP address.

## [Configure Contextual Intelligence Publisher](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---iboss#configure-contextual-intelligence-publisher)

Once API Access has been configured on iBoss, navigate to the NAC Configuration at <https://portal.myweblogon.com:8443/manage> ([portal.myweblogon.com](http://portal.myweblogon.com/) can be replaced by the manager IP or a branded URL) and choose “Contextual Intelligence.” Click on “Add” and enter the following information:

- **Publisher:** iBoss
- **Name:** A name to describe where CIP is publishing Data.
- **NAC Name:** the Nac Name that was used to add NAC as a Nac agent in iboss
- **Key:** The iBoss security key
- **Hostname:** iBoss IP address
- **Port**: iBoss listen port

All other options should be left at their defaults unless requested by OPSWAT Support. Once finished, click “Submit” and continue to the next section to verify the integration.

## [Troubleshooting](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---iboss#troubleshooting)

## [Check the Users page of iboss](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---iboss#check-the-users-page-of-iboss)

Before starting any troubleshooting, determine the state of the user in iboss by checking the user page to see the status of the user and determine if the user is assigned to the correct iboss profile.

## [Determine if the information provided in NAC is correct](/docs/manac/nac-v8.1.1/configuration/contextual-intelligence-publishing---iboss#determine-if-the-information-provided-in-nac-is-correct)

If iboss is not automatically changing the filtering groups based on the data received from NAC, the next step is to determine if iboss can correctly receive the data. In a web browser, navigate to the following URL:

<http://IBOSS_IP_ADDRESS:8015/nacAgent?action=logon&user=VALID_USERNAME&dc=NACNAME&key=IBOSS_API_KEY&ip=VALID_ENDPOINT_IP&g=>

Replace the following:

- **IBOSS_IP_ADDRESS:** The IP address of the iboss appliance
- **VALID_USERNAME:** The username of a user that should be moved out of the default profile
- **IBOSS_API_KEY:** The iboss security key
- **NACNAME:** the Nac Name that was used to add NAC as a Nac agent in iboss
- **VALID_ENDPOINT_IP:** The IP address of the machine that iboss should associate with the VALID_USERNAME

If the request times out, then the iboss appliance is either not reachable, or not properly configured for API access. If iboss is configured correctly, a single line of “SUCCESS” or “FAIL” will be returned in the web browser. If “SUCCESS” is returned, iboss has received and processed the request. If “FAIL” is returned, one or more of the values above is incorrect. Double-check the configuration and try again. Since the URL is case sensitive, ensure that the ‘A’ in the ‘nacAgent’ portion of the URL is capitalized.

Ensure iboss can perform group lookups

If iboss is returning a “SUCCESS” response and the user is still not assigned the correct profile, ensure that iBoss is configured for Active Directory/LDAP Group Matching.
