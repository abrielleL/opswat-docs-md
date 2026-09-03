<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/operating/RBAC-role-base-access-control-permissions -->

# Roles

Summarize Page    Connect to Cursor Connect to VS Code
## [Overview](/docs/mdmft/v3.11.4/operating/RBAC-role-base-access-control-permissions#overview)

MetaDefender Managed File Transfer™ includes several predefined roles, also referred to as "User Types." When MetaDefender Managed File Transfer™ is first accessed, the initial user is created as an Administrator. Any local user created afterward must have their role defined during the creation process.

Info

The first Administrator account can be deleted, as long as there is at least one other Administrator remaining in the system.

## [Roles and Permissions](/docs/mdmft/v3.11.4/operating/RBAC-role-base-access-control-permissions#roles-and-permissions)

**Administrator**

- Has full system access and can perform all configuration tasks
- Can release files, but cannot approve files unless also assigned the Supervisor role
- Can download and preview files uploaded by other users
- Can unblock a file blocked by MetaDefender Core™ and restore blocked status

**Restricted Administrator**

- Has access to the Processing History, but cannot preview or download files belonging to other users
- Cannot create or fetch API keys, and cannot import or export MFT settings
- Can unblock a file blocked by MetaDefender Core™ and restore blocked status

**Helpdesk Administrator**

- Can manage users (add, remove, edit) and perform general administrative tasks
- Has access only to their own files

**Auditor**

- Has view access to all files processed by the system
- Can access the following sections: Processing History, Outbreak Prevention, Audit, Recycle Bin, and Archive
- Can also view the Supervisor History for files under supervision

**Global Supervisor**

- A regular user role with elevated permissions
- Can see all files in the pending approval state and approve them, making the files immediately available
- Cannot assign or delegate supervisory roles

**Verdict Supervisor**

- A Global Supervisor with more accessibility for files
- Has access to the Processing History, and the ability to Override Blocked Status or Restore Blocked Status of user files.

**User**

- Can manage the files they upload
- Can share files with internal and guest users
- Can create guest users
- For detailed capabilities, refer to the [End User Guide](https://app.developerhub.io/metadefender-managed-file-transfer/v3.9.3/end-user-guide/access-md-mft)

**Automation Coordinator**:

- Can create and manage Automated Jobs

|  | Admin | Read Only Administrator | Restricted Administrator | IT Helpdesk | Auditor | User | Global Supervisor | Verdict Supervisor | Automation Coordinator |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Processing History | Full | Filename and tag | Full **[6]** | N/A | Full **[1]** | N/A | N/A | Full**[8]** | N/A |
| Users | Full | View | Create / Remove / Edit | Create / Remove / Edit | Self created External / Guest | Self created External / Guest | Self created External / Guest | Self created External / Guest | N/A |
| Supervisor | Full | View | Full | Process Setup | N/A | When Supervisor | Full **[5]** | Full **[5]** | When Supervisor |
| Outbreak Prevention | Full | View | Full | Full | Full **[2]** | N/A | N/A | N/A | N/A |
| Trusted Network | Full | View | Full | Full | N/A | N/A | N/A | N/A | N/A |
| Notifications | Full | View | Full | Full | N/A | N/A | N/A | N/A | N/A |
| Audit | Full | View | Full | Full | Full **[2]** | N/A | N/A | N/A | N/A |
| Recycle Bin / Archive | Full | View | Own files in trash | Own files | Full **[3]** | Own files | Own files | Own files | Own files |
| Settings | Full | View | Full **[7][4]** | Full **[4]** | N/A | N/A | N/A | N/A | N/A |
| SFTP Integrations | Full | View | Full | Full | N/A | N/A | N/A | N/A | View them at Jobs |
| MFT Integrations | Full | View | Full | Full | N/A | N/A | N/A | N/A | View them at Jobs |
| Jobs | Full | N/A | Full | Full | N/A | N/A | N/A | N/A | Full |
| My Credentials | Full | N/A | Full | Full | N/A | Local MFT API key | N/A | N/A | Full |
| Dashboard | Full | Full | N/A | Full | N/A | N/A | N/A | N/A | N/A |

**[1]** Full - But without Revoke/Approve/Delete/Permanently Delete/Archive File

**[2]** Full - But without Settings

**[3]** Full - But without Restore/Delete/Permanently Delete

**[4]** Full - But without API keys

**[5]** Full - Without the ability to delegate other supervisors

**[6]** Full - Without the ability to preview of download other user's files

**[7]** Full - Without settings import/export

**[8]** Full - Without the ability to Archive/Delete/Permanently Delete

Info

The last-created local administrator's role cannot be changed.

Warning

When an existing user's role is changed to Automation Coordinator, they will lose access to manage any guest or external users they previously created.
