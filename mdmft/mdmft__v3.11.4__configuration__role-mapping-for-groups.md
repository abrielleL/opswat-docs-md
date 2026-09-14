<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/role-mapping-for-groups -->

# Role Mapping for Groups

Summarize Page    Connect to Cursor Connect to VS Code

User role mapping allows fine-tuning of how active directory synchronization is performed. Administrators and read-only administrators are synchronized according to your user directory structure.

Role Mapping Options:

| Role | Description |
| --- | --- |
| Auditor | Users in specified groups will be licensed as Auditors |
| Global Supervisor | Users in specified groups will be licensed as Global Supervisors |
| Administrator | Users in specified groups will be licensed as Administrators |
| Readonly Administrator | Users in specified groups will be licensed as Readonly Administrators |
| Helpdesk Administrator | Users in specified groups will be licensed as Helpdesk Administrators |
| Automation Coordinator | Users in specified groups will be licensed as Automation Coordinator |
| Restricted Administartor | Users in specified groups will be licensed as Restricted Administrator |

Info

The Local Administrator account is also Supervisor to ensure one active supervisor at all times.

If a user belongs to multiple groups mapped to different roles, the following precedence is applied:

- Administrator
- Readonly Administrator
- Restricted Administrator
- Helpdesk Administrator
- Auditor
- Global Supervisor
- Automation Coordinator

Example: Active directory group A is mapped to the administrator role while group B is mapped to the auditor role. An active directory user who is member of both groups will have the assigned MetaDefender Managed File Transfer role of Administrator.

---

Click "Continue" to [Organizational Unit, Security Group and User Filtering Configuration](/docs/mdmft/v3.11.4/configuration/organizational-units-and-groups-configuration) after customizing the information as required.
