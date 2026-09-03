<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with -->

# How to configure Role Mapping per groups in SSO Integration with Entra ID

### [Overview](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#overview)

When integrating **MetaDefender Core** with **Microsoft Entra ID** for Single Sign-On (SSO) authentication over SAML, user roles can be mapped in two primary ways:

1. Assigning a default role to all users
2. Configuring custom role mappings to support multiple roles across various user groups

This guide demonstrates how to assign specific MetaDefender Core roles to Entra ID groups.

### [Prerequisites](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#prerequisites)

Before proceeding, ensure the following configurations are in place:

- Entra ID user-group mappings are already configured
- Groups are assigned to the SSO application
- MetaDefender Core SAML integration is completed

### [**Step-by-Step Instructions**](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#step-by-step-instructions)

#### [**Step 1: Add a Group Claim in the SSO Application**](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#step-1-add-a-group-claim-in-the-sso-application)

**Go to:**

**SAML Application → Single sign-on → Attributes & Claims → Edit**

Then:

1. Click **Add a group claim**
2. Select **All groups**
3. Click **Save**

This creates the `user.groups [All]` claim, which provides a **Claim URL**. This URL will be used as the **Key** in the MetaDefender Core configuration.

#### [Step 2: Retrieve the Group’s Object ID](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#step-2-retrieve-the-groups-object-id)

Return to the configured SAML application and select one of the assigned groups to view its details. This displays the group’s **Object ID**, which is needed to map roles in MetaDefender Core.

Use the following format in the **Condition** field to match the group by its Object ID:

HtmlCopy^object_id$

This pattern ensures only users from that specific group are matched.

### [Role Assignment Example](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#role-assignment-example)

If a user belongs to multiple groups and multiple role-mapping rules are configured:

- By default, MetaDefender Core applies **only the first matching rule**
- If **“Combine roles from all matched rules instead of first match only”** is enabled, **all matching roles will be assigned to the user**

#### [Combine Roles from Multiple Matching Rules](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#combine-roles-from-multiple-matching-rules)

#### [How to enable](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#how-to-enable)

1. Go to: **Configuration → Role Matching → Role Mapping**
2. Enable: **Combine roles from all matched rules instead of first match only**
3. Click **Save**

#### [**Example**](/docs/mdcore/knowledge-base/how-to-configure-role-mapping-per-groups-in-sso-integration-with#example)

- Group A → Administrator role
- Group B → Read-only role

If a user belongs to both groups:

- **Disabled:** User gets *Administrator only* (first match)
- **Enabled:** User gets *Administrator + Read-only*

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
