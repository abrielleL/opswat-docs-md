<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/supervisors-setup -->

# Default Supervisor Setup

Summarize Page    Connect to Cursor Connect to VS Code

Default Supervisors can be assigned by selecting from a list or by using filters. These supervisors are authorized to approve files uploaded by any user from any container (OU or group).

Warning

If "Group Supervision" is enabled along with "Disable Group Supervision for Default Supervisors," Default Supervisors can only approve files from users who do not belong to a supervised container or group.

Warning

Active Directory synchronization must be enabled to configure default supervisors using OU filters.

Files uploaded by local users can only be approved by supervisors defined in this section.

Step-Based Approval: Supervisors assigned to specific approval levels can only approve or revoke files at their assigned level.

Info

Guests and external users cannot be assigned as Supervisors.

Info

Active Directory configuration for groups:

1. Groups only: The "Setup Supervisors" page displays only the explicitly included groups.
2. Groups and OUs: The page displays all groups from the connected Active Directory. This ensures visibility for users who belong to an OU but are not part of an explicitly included group.
