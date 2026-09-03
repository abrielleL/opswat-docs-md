<!-- source: https://www.opswat.com/docs/manac/knowledge-base/what-policies-can-i-enforce-on-agentless-devices- -->

# What policies can I enforce on agentless devices?

For devices that cannot install the Policy Key agent, the NAC can still enforce policies based on device type, user identity and other attributes.

In order to make device type information for agentless devices available to the NAC, make sure that you have configured the relevant networking device(s) to relay DHCP requests to the NAC:

[Configuring DHCP Device Identification](https://docs.opswat.com/manac/installation/optional---configure-device-profiling-and-visibility#configure-dhcp-device-identification)

User identity information, including group membership, is loaded from an LDAP authentication source when a user authenticates. Find details on how to configure this here:

[Active Directory and LDAP Authentication Sources Setup](https://docs.opswat.com/manac/configuration/active-directory-and-ldap-authentication-sources-setup)

Other device attributes such as domain membership, connected SSID, or connected switch port, can be gathered from the [AD Connector Service](https://docs.opswat.com/manac/configuration/windows-services-setup-guide) or [RADIUS Accounting](https://docs.opswat.com/manac/knowledge-base/how-do-i-send-radius-accounting-to-nac-for-cisco-wlc).

To take advantages of any or all of these attributes in your NAC policy configuration, refer to the documentation for the corresponding "qualifier" type in the main Policy Manager Guide:

[Policy Manager Guide](https://docs.opswat.com/manac/operating/policy-manager-guide)
