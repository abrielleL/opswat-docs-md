<!-- source: https://www.opswat.com/docs/manac/configuration/roles-for-use-with-radius -->

# Roles for use with RADIUS

This section includes information that is entirely optional. If there is a desire to return different attributes such as VLAN assignments or any other specific RADIUS attributes such as those needed to perform enforcement, this section describes the steps required to configure this based on a user’s LDAP group memberships. If this functionality is not desired, please skip to the next section.

## [Step-by-step guide](/docs/manac/configuration/roles-for-use-with-radius#step-by-step-guide)

NAC uses the concept of *Roles* to create sets of RADIUS attributes that can be used assign different access levels, VLANs, etc. *Enforcement Roles* are used any time attributes must be specified and are not limited to policy enforcement actions.

To access *Roles*, choose “Roles” from the top navigation.

The system will auto-configure a set of default attributes based on the Vendor(s) chosen in section 3. In most cases, the default roles will be sufficient and no further changes will need to be made. If additional enforcement roles are desired, click the “New Enforcement Role” button. To modify an existing role, click the “Edit” button.

A sample role that will assign a specific VLAN is provided below. This example with work for VLAN assignment on most Vendors. For more details on the types of information that should be included in each enforcement role, please consult your vendor’s documentation, or the NAC RADIUS-based Enforcement setup document for your specific vendor.

### [Next Step (Optional): Configure LDAP authentication](/docs/manac/configuration/roles-for-use-with-radius#next-step-optional-configure-ldap-authentication)

### [Next Steps (Required): Map Roles to NAC Policy Groups](/docs/manac/configuration/roles-for-use-with-radius#next-steps-required-map-roles-to-nac-policy-groups)

### [Related articles](/docs/manac/configuration/roles-for-use-with-radius#related-articles)

Error rendering macro 'contentbylabel' : parameters should not be empty

## [Map Roles to NAC Policy Groups](/docs/manac/configuration/roles-for-use-with-radius#map-roles-to-nac-policy-groups)

## [Step-by-step guide](/docs/manac/configuration/roles-for-use-with-radius#step-by-step-guide)

*Policy Group Mappings* are used exclusively for enforcing NAC policies. In a standalone RADIUS server configuration, *Policy Group Mappings* are not required and this section can be skipped.

To access *Policy Group Mappings*, choose “Policy Group Mappings” from the left navigation and then select the “Policy Group Mappings” tab from the top of the page.

The system will auto-configure a set of mappings based on the most common use cases. In most cases, the defaults will be sufficient and there is no need to make further modifications. Any Policy Groups that are not explicitly mapped will default to using the default *Enforcement Roles* specified on the last row.

If a new *Policy Group Mapping* is required, click the “New Mapping” button and choose the required options:

- **Policy Group:** the name of the NAC Policy Group. Only one mapping can exist for each Policy Group.
- **Quarantine Role:** The enforcement role to be used when a device is out of compliance.
- **Compliant Role:** The enforcement role to be used when a device is compliant.
