<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/threat-enforcement-configuration---juniper-srx -->

# Threat Enforcement Configuration - Juniper SRX

## [Overview](/docs/manac/nac-v8.1.1/configuration/threat-enforcement-configuration---juniper-srx#overview)

The NAC threat enforcement module allows for the ability to configure enforcement policies based on threats that are detected in a system external from NAC. These policies can then be used with any device type and do not require the use of an agent running on the end-user device.

Once configured policies can be set to either audit or quarantine. With any quarantine policy, end-users will receive a browser-based message informing them of the issue. These messages can be customized with instructions on how to remediate and how long they will need to wait before the quarantine will be re-evaluated.

## [Configure Juniper SRX](/docs/manac/nac-v8.1.1/configuration/threat-enforcement-configuration---juniper-srx#configure-juniper-srx)

In the firewall, the following commands should be run from the cli to enable IDP event syslog.

## [Enable the IDP even logging to syslog](/docs/manac/nac-v8.1.1/configuration/threat-enforcement-configuration---juniper-srx#enable-the-idp-even-logging-to-syslog)

configure
set security log mode event
set security log source-address 10.100.18.12
set system syslog host 10.100.210.200 port 30514 any any
set system syslog host 10.100.210.200 port 30514 match RT_IDP
set system syslog host 10.100.210.200 port 30514 structured-data
set system syslog file idp any any
set system syslog file idp match RT_IDP
set system syslog file idp structured-data
commit

Note: The source-address should be an interface IP of the firewall. The syslog host will be the NAC appliance (In a cluster environment, this will be the manager IP).

## [Verify the configurations are in place](/docs/manac/nac-v8.1.1/configuration/threat-enforcement-configuration---juniper-srx#verify-the-configurations-are-in-place)

show security log
## [Configure Threat Enforcement Input](/docs/manac/nac-v8.1.1/configuration/threat-enforcement-configuration---juniper-srx#configure-threat-enforcement-input)

After the threat detection system is configured, open the NAC Configuration at <https://portal.myweblogon.com:8443/manage> ([portal.myweblogon.com](http://portal.myweblogon.com) can be replaced by the manager IP or a branded URL) and choose “Configuration Manager > Threat Enforcement”.

**Enable the webapi:**

From the dropdown, choose Juniper SRX and click ‘Add’.

After choosing the Vendor, at least one source must be defined. A source is simply the IP address of the threat detection system. If the threat detection system has multiple interfaces, the IP specified must be the IP that appears as the source address of the alerts. The name can be any descriptive name that is needed.

After clicking ‘Submit’, the Threat Detection source will appear in the list.

## [Configure Threat Enforcement Policies](/docs/manac/nac-v8.1.1/configuration/threat-enforcement-configuration---juniper-srx#configure-threat-enforcement-policies)

After at least one source has been defined, Threat Detection policies can now be created. To create a policy, click the ‘Add’ button.

The first section is used to define what alerts NAC will listen for. If alert details are not configured, NAC will ignore the alert. The following values are applicable for Juniper SRX and will be joined via 'AND' to find matching packets.

- **Threat Severity:** A textual value indicating LOW, MEDIUM or HIGH
- **Attack Name:** This field will always be a text value and also support regex matching. This field can be left blank to match all values.
- **Policy Name:** This field will always be a text value and also support regex matching. This field can be left blank to match all values.

The next section defines how NAC will react to the defined alert. Once configured, the policies will be available in the NAC Policy Manager.

- **Policy Name:** The name of the NAC Policy. This value will be used to represent this policy in the Policy Manager and in the Device Manager.
- **Policy Duration:** Defines how long NAC will enforce the policy when an alert is received. Once this time expires, the policy will no longer be enforced unless a follow-up alert is received for the device.
- **Enforcement:** Defines whether NAC will block a device or simply report on the alert.
- **Web Message:** The web message that will be displayed to blocked devices for the duration of the enforcement.

Once configured, click ‘Save’.

The resulting Threat Enforcement Policy will now appear in the list and will be available in the Policy Manger.

## [Add Policies to existing Policy Groups](/docs/manac/nac-v8.1.1/configuration/threat-enforcement-configuration---juniper-srx#add-policies-to-existing-policy-groups)

After Threat Enforcement policies have been defined, they will be available in the Policy Manager. Threat Enforcement policies can be added to a Policy Container just like all other NAC policies.
