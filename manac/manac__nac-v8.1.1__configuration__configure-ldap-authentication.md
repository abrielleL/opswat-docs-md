<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/configure-ldap-authentication -->

# Configure LDAP authentication

Authentication sources are used to determine valid user credentials and collect group memberships. Configuring an LDAP sources is required if there is a need to assign RADIUS attributes, such as VLAN assignment, outside of the NAC Policy engine. If the RADIUS server is integrated with AD for EAP-PEAP authentication, a separate LDAP connection must still be defined for this functionality to work. This requirement is present as the Direct Active Directory integration is not able to perform the level of group lookups required for this functionality.

For instructions on configuration of LDAP authentication [click here](/docs/manac/nac-v8.1.1/configuration/configure-ldap-authentication)

## [Step-by-step guide](/docs/manac/nac-v8.1.1/configuration/configure-ldap-authentication#step-by-step-guide)

## [Map RADIUS Enforcement Roles to LDAP Groups](/docs/manac/nac-v8.1.1/configuration/configure-ldap-authentication#map-radius-enforcement-roles-to-ldap-groups)

NAC provides the ability to return specific RADIUS attributes at the time a device associates to a network. This can be useful in scenarios where NAC is a standalone RADIUS server as well as scenarios where a specific set of attributes is required prior to NAC assessing any security policies.

To map *Enforcement Roles* to LDAP groups, choose “Policy Group Mappings” from the left navigation.

By default, the “SC_Initial_Role” is always returned to devices associating with the network. If no attributes are required at the initial association, this value can be set to “None”.

To create an *Enforcement Role* to *LDAP Group* association, choose an Authentication source from the dropdown and click the green add (+) icon. Ensure the any LDAP groups you are defining are contained within the baseDN of the LDAP source. If baseDN is searching in a different OU from where LDAP group objects exist, an additional LDAP source will need to be created.

One or more *LDAP groups* can be added and assigned to *Enforcement Roles* as needed. Any users that do not match a specified role will be associated with the default _Enforcement Role._*LDAP Groups* can be entered in one of the following formats:

- **Group Name Only:** example: “Staff”
- **Distinguished Name:** example: “CN=Staff,DC=Domain,DC=Com”

If multiple LDAP servers are configured, NAC can be configured to perform group lookups against as many LDAP servers as needed.

Info

Only LDAP Groups are supported for initial role assignment. Other objects such as OU’s cannot be used for this feature.

##
