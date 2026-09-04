<!-- source: https://www.opswat.com/docs/manac/configuration/contextual-intelligence-publishing---procera-psm -->

# Contextual Intelligence Publishing - Procera PSM

Overview

Using CIP, a Procera PSM can be used to place rules on end-users on a per-user basis enabling more granular policies to be used. Once configured, user data will be passed transparently to the Procera PSM from CIP. The CIP integration currently provides the following values to the Procera PSM:

- Machine Current IP Address
- Machine Local IP Address (If a Policy Key is installed)
- Username
- Group Memberships (LDAP groups, or NAC specific groups)
- Machine Mac Address
- Machine Name (if available)
- Device Type
- Policy Group
- Domain Memberships (If NAC is set up to use Domain Single Sign-On)

The purpose of this guide is to walk through the configuration requirements for sending identity information from CIP to a Procera PSM.

Prior to working through this document, a Procera PSM and NAC must be installed and functional on the network. CIP must also be installed in the NAC system.

## Configure Procera PSM

On the Procera PSM, a JSON UDP bulk Source will need to be configured to receive the CIP messages and a new subscriber + session schema will need to be configured to store the values.

## Configure the Schema

Add the desired attributes you want to store on the subscriber.

The schema in the images below is configured to store the values received from CIP.

Subscriber Schema:

Session Schema:

## Configure the PSM Source

*NOTE: For more complete information on setting up a new source, please refer to the PSM documentation

Select Source > New JSON Bulk Source (UDP)

Configure listen host and port as shown in the image below. The listen host will be the IP address of the NAC appliance running CIP. In a cluster environment, this will be the manager node:

Enter the values that are being sent from CIP as shown in the image below:

Add a declaration which you can bind your rules to.

Define rules to create/update/delete subscriber/session objects. The rules have to be combined with a declaration (from above). This is where we the PSM is populated with CIP values.

Assign which Attributes (from the list of 'Variables' defined earlier) should be mapped to which subscriber/session object Attributes:

## Configure Contextual Intelligence Publisher

Once the Procera PSM has been configured, enter the following information:

- **Publisher:** Procera
- **Name:** Name to describe where CIP is publishing Data
- **Host:** IP address of the Procera PSM
- **Port:** Listen port that was entered when the JSON Bulk Source was configured.

Once finished, click “Submit” and continue to the next section to verify the integration.

## Verify Integration

If everything is configured correctly, subscribers and sessions will be created automatically when the PSM receives the UDP messages from CIP.

PSM logs can be used to verify that PSM is receiving updates:

Apr 9 05:15:38 pl2 psmd: INFO psm.statslogger UdpSource[3996]: 1337 requests/s
Apr 9 05:15:48 pl2 psmd: INFO psm.statslogger Model: 1337 transactions/s 1337 updates/s

Manual lookups on subscribers can also be done to verify the correct values are mapped.
