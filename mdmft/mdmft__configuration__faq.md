<!-- source: https://www.opswat.com/docs/mdmft/configuration/faq -->

# FAQ

Summarize Page    Connect to Cursor Connect to VS Code
### [Are supervisors able to approve their own files?](/docs/mdmft/configuration/faq#are-supervisors-able-to-approve-their-own-files)

This functionality is currently not available with no plans to reinstate it.

### [Is it possible to make certain users exempt from the supervision flow?](/docs/mdmft/configuration/faq#is-it-possible-to-make-certain-users-exempt-from-the-supervision-flow)

In the current version of MetaDefender Managed File Transfer™ this may be resolved in the following ways:

1. Local Users: Local user accounts can be designated as exempt from supervision at the time of user creation or in the [user management settings](https://www.opswat.com/docs/mdmft/configuration/supervisor-approval-details#excluding-users-from-the-supervisor-flow).
2. Active Directory (AD) individual users: Specific AD users can be configured to be exempt from supervision in the [user management settings](https://www.opswat.com/docs/mdmft/configuration/supervisor-approval-details#excluding-users-from-the-supervisor-flow).
3. Active Directory Groups: If the users belong to an AD group, the entire group can be marked as exempt during [supervisor configuration](https://www.opswat.com/docs/mdmft/configuration/supervisor-approval-details#supervision-between-groupsorganizational-units).

### [Can the supervisor approval be skipped?](/docs/mdmft/configuration/faq#can-the-supervisor-approval-be-skipped)

Skipping of a supervisor approval is [configurable to happen](https://www.opswat.com/docs/mdmft/configuration/supervisor-approval-details#skip-supervisor-approval):

- Never (default)
- Upon sanitization
- After a specified timespan

In any of these scenarios the respective file will be marked as 'Skipped'. The 'Skipped' is equal to 'Approved' in terms of functionality.

### [What is the purpose of the Default Supervisor?](/docs/mdmft/configuration/faq#what-is-the-purpose-of-the-default-supervisor)

[Default Supervisors](https://www.opswat.com/docs/mdmft/configuration/supervisors-setup) can be assigned by selecting from a list or by using filters. These supervisors are authorized to approve files uploaded by any user from any container (Organizational Unit or Active Directory Group).

### [What is the purpose of the Global Supervisor?](/docs/mdmft/configuration/faq#what-is-the-purpose-of-the-global-supervisor)

[Global Supervisors](https://www.opswat.com/docs/mdmft/operating/RBAC-role-base-access-control-permissions) are able issue one approval to fully cover any and all types of supervision flows.

### [What is the purpose of the Restricted Supervisor?](/docs/mdmft/configuration/faq#what-is-the-purpose-of-the-restricted-supervisor)

[Restricted Supervisors](https://www.opswat.com/docs/mdmft/configuration/restricted-supervisors) cannot download or preview the supervised files.

### [What is the purpose of Supervisor Delegates?](/docs/mdmft/configuration/faq#what-is-the-purpose-of-supervisor-delegates)

Supervisors can temporarily [delegate](https://www.opswat.com/docs/mdmft/configuration/supervisor-approval-details#supervisor-delegate) their approval responsibilities to another Active Directory users.
