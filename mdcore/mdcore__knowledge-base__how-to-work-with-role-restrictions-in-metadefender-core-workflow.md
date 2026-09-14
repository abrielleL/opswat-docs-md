<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-work-with-role-restrictions-in-metadefender-core-workflow -->

# How to Work with Role Restrictions in MetaDefender Core Workflows?

This article is applied to MetaDefender Core releases deployed on Windows and Linux systems.

**Understanding Role Restrictions in MetaDefender Core Workflows**

Role Restrictions in workflows function differently than you might expect. They do **not** control who can view or edit workflows in the GUI. Instead, Role Restrictions determine which workflows are available to specific roles when submitting files for scanning.

**How Role Restrictions Work**

Role Restrictions limit workflow availability during the file submission process. Users can only select workflows that include either:

- Their assigned role
- The "Everyone" role

**Testing Role Restrictions**

To verify role restrictions are working correctly:

1. Log in as a user with a specific role (e.g., restricted_user)
2. Navigate to the file scanning interface
3. Drag a file to the scan box at the top of the page
4. Click the workflow selector (located to the lower left of the "Process" button)
5. Review the available workflows—only those containing the user's role will appear

**Example Configuration**

In this example, we configured role restrictions as follows:

- Added the "restricted_role" role to the Email Gateway Security workflow
- Removed both "restricted_role" and "Everyone" roles from all other workflows

Result: When logged in as a user with the "restricted_role" role, only the Email Gateway Security workflow appears in the workflow selector (see screenshot).

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
