<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/sso-role-mapping -->

# User role mapping

### [Motivation](/docs/mdcore/v5.21.0/configuration/sso-role-mapping#motivation)

MetaDefender Core supports two types of role assignments for signed-in users. The first is `Default role`, which is the standard option and fits most simple use cases. If this option is selected, a fixed role is assigned to users when they successfully sign in to MetaDefender Core with their accounts. This role is specified when the SAML or OIDC directory is created. In the picture below, Administrators role will be assigned to every signed-in user.

However, in some organizations where employees are structured into groups with separate privileges, assigning the same role to all users in MetaDefender Core does not make sense. One common use case is that the Editor role is assigned to a group of system experts who can control and update MetaDefender Core configurations to meet the organization's needs, while the Viewer role is assigned to the team leaders who can only view the configurations. For all other user groups, they should only use MetaDefender Core features without the ability to log in, view, or update configurations. MetaDefender Core supports Role Mapping to help build flexible rules for assigning appropriate roles to groups of users based on attributes provided by the IdP when the user successfully signs in.

### [General idea](/docs/mdcore/v5.21.0/configuration/sso-role-mapping#general-idea)

Role Mapping consists of a series of rules that are checked one after another by MetaDefender Core until the first one matches the attribute values provided by the IdP or until none match, causing MetaDefender Core to refuse the user's sign-in. The following shows a sample plain rule.

Each rule includes a single key name from which to take the value, a list of conditions, and roles that will be assigned to the user if their conditions are satisfied. The key name is the attribute name which is defined by the IdP and can be modified or created by the system administrator on the IdP page. In the current version of MetaDefender Core, only Regular Expressions can be selected as the matching type. The input under `Condition` is a valid regular expression that MetaDefender Core will use to match against the value of the key. Multiple matching rules can be added by clicking `Add New` button. If multiple rules are defined, each rule is checked sequentially, following their defined order.

There should be a case where a single key can be used to match multiple conditions. The system administrator can click the plus button next to `VALUE` title to add more conditions. Conditions are checked in the order they are listed when the rule is evaluated by MetaDefender Core.

#### [How User Roles Are Assigned Based on Matched Conditions](/docs/mdcore/v5.21.0/configuration/sso-role-mapping#how-user-roles-are-assigned-based-on-matched-conditions)

Info

Starting from **MeteDefender Core 5.18.0**, user can decide how user roles are assigned during role mapping using the option `Combine roles from all matched rules instead of first match only`:

- **Disabled (default):** Roles from the first matching condition are assigned to the user.
- **Enabled:** If a user matches multiple conditions, roles from all matching rules are combined and assigned instead of only the first match.

### [Building rules](/docs/mdcore/v5.21.0/configuration/sso-role-mapping#building-rules)

We remind you of the use case mentioned in [Motivation](/docs/mdcore/v5.21.0/configuration/sso-role-mapping#motivation) section, in which the Editor role is assigned to the group of system experts, the Viewer role to the group of team leaders, and no role to other groups.

Info

You are advised to successfully set up SSO integration between your preferred IdP and MetaDefender Core using the default role option before attempting to apply role mapping.

Suppose the system administrator has already created an attribute named "group" in the preferred IdP and set its value either *expert*, *leader*, or *normal_user*. The new attribute must be configured to be returned in the authentication response from the IdP when a user signs in successfully. The following are steps to build role mapping rules based on "group" attribute in MetaDefender Core.

1. Sign in to MetaDefender Core.
2. From the dashboard, navigate to `User Management` > `Roles`.
3. Click `Add Role` to add Editor role and assign it appropriate rights.
4. Do the same for Viewer role.

5. Click `Add` to complete the assignment of rights to the role.

6. Create a new SAML or OIDC directory and follow steps to set up the SSO integration between your preferred IdP and MetaDefender Core. At the step of user role selection, choose `Role mapping` option.

7. Fill in `Key` field with "group".
8. Click the plus button to define an additional `VALUE 2`.
9. `VALUE 1` will attempt to match the value of "group" key against the regular expression ^expert$, while the second will do so against ^leader$. If the first matches perfectly, the user will be assigned the Editor role, while the latter will assign the Viewer role. We do not define a rule for *normal_user*, which means users in this group will always fail to sign in to MetaDefender Core.

10. Click `Add` to complete the settings.
11. In `User Management` screen of MetaDefender Core, toggle the new created directory. A dialog box appears to confirm the action. Once `Enable` is clicked, all sessions are expired immediately.
12. Click `Login` from the home screen of MetaDefender Core and sign in with your account registered in IdP. If everything goes right, the MetaDefender Core dashboard is displayed with the user identity set in the top right corner. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.

For the OIDC directory, as a key belongs to a specified scope, the system administrator must specify the key and its associated scope when defining the matching rules. Please refer to the IdP documentation to determine which key belongs to which scope.
