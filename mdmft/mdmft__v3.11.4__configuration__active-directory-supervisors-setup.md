<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/active-directory-supervisors-setup -->

# Active Directory Supervisors Setup

Summarize Page    Connect to Cursor Connect to VS Code

At the "Supervisor Approval" --> "Process Setup", supervisors can be edited individually for each container (OU/group).

Warning

Active Directory synchronization must be enabled to configure supervisor approval for OU containers using filters.

For step-based approval, one or multiple supervisors can be assigned to every level within every container (OU or group).

In Group Mode, step-based approval also allows assigning one or more supervisor groups to each level in addition to individual supervisors.

When saving new supervisor assignments using the "Save" button, the system validates that each container (OU or group) has the required number of supervisors. If the minimum requirement is not met, an error message will appear and the "Save" action will be blocked.

Info

Global Supervisors are not counted toward the required number of supervisors for step-based approval.

### [Supervisor Precedence](/docs/mdmft/v3.11.4/configuration/active-directory-supervisors-setup#supervisor-precedence)

Supervisor assignments can sometimes lead to conflicting or ambiguous configurations, especially when using step-based approval in Group mode. To address this, supervisor precedence has been introduced to ensure clarity and consistency.

Supervisor precedence ensures:

- No duplicate supervisors appear in a single supervision flow (e.g., due to overlapping groups)
- Each supervisor is assigned from only one source (e.g., a user cannot act as both a default supervisor and a group-assigned supervisor)
- Supervisors are not assigned to multiple levels within the same supervision flow

A supervision flow is defined as the approval process for a specific Group or OU.

Configurations that place a single supervisor on multiple approval levels within the same flow are not supported.

Supervisor Precedence Resolution Order

1. Default Supervisors override all other assignments, regardless of level.

   - If a user is a default supervisor and also part of a supervisor group or assigned individually, they are treated only as a default supervisor.
   - Supervisor groups are not overridden as a whole—only the overlapping member is excluded.
2. Supervisor Groups override individual supervisors, except default supervisors.

   - If a user is assigned individually and is also a member of a supervisor group, they are treated only as part of the group.
   - Saving this configuration retains only the group assignment.
3. Supervisor Groups override overlapping groups based on level precedence.

   - In the case of overlapping groups, the group assigned to the higher approval level takes precedence.
   - Overlapping members are resolved to this higher-level group.
   - However, both groups will still be saved, as group composition may change and require re-evaluation over time.

**Note:** Supervisor precedence also applies outside of step-based approval. In non-step-based scenarios, resolution strategies apply at a single level rather than across multiple levels.

### [Assign Supervisors Dynamically Using an Active Directory Filter](/docs/mdmft/v3.11.4/configuration/active-directory-supervisors-setup#assign-supervisors-dynamically-using-an-active-directory-filter)

Supervisors and OU-based supervisors can be assigned dynamically by specifying an "Active Directory" filter. A user is promoted to supervisor when they match the filter criteria.

An LDAP query checks if the specified LDAP attribute contains the expected value. If the attribute is missing or does not match, the user will not promoted to supervisor.

Info

The filter applies across all configured Active Directory sources.

Each supervisor can approve or reject files only for users within the same container. A container can have multiple supervisors, or none at all.

To learn how to include or exclude containers, see [Role Mapping for Groups](/docs/mdmft/v3.11.4/configuration/role-mapping-for-groups).

Info

Step-based approval: Adding supervisors from filter is not yet available.

### [Setting Up Group File Approval](/docs/mdmft/v3.11.4/configuration/active-directory-supervisors-setup#setting-up-group-file-approval)

When group supervision is enabled, users who belong to multiple groups can restrict which group's supervisors are allowed to approve their uploaded files. This restriction applies only to group supervisors—Global Supervisors can approve files regardless of this setting.

Note

If the approval process configuration is changed, any group supervision restrictions are automatically removed.

To configure special supervisor settings for a specific group, use the dropdown menu in the AD Groups list.

Unlike OU-based settings, group supervisors cannot be assigned using an Active Directory filter.

In one-stage or multi-stage group approval, you can select an AD group as the supervisor..If "Allow Supervision Between Groups" is enabled, supervisors from other groups can be selected. If not, only the current group can be assigned as supervisor.

Any member of a supervisor-designated AD group can approve files uploaded by users in that group.

Info

Users belonging to multiple AD groups can choose the target group for their file uploads in the "Upload File" modal ([click here](/docs/mdmft/v3.11.4/operating/upload-files) for more details).

Supervisor rights for any assigned Active Directory group can be revoked at any time.
