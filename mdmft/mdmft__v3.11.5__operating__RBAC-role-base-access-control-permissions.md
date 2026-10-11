<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/operating/RBAC-role-base-access-control-permissions -->

# Roles

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Overview](/docs/mdmft/v3.11.5/operating/RBAC-role-base-access-control-permissions#overview)

MetaDefender Managed File Transfer™ includes several predefined roles, also referred to as "User Types." When MetaDefender Managed File Transfer™ is first accessed, the initial user is created as an Administrator. Any local user created afterward must have their role defined during the creation process.

Info

The first Administrator account can be deleted, as long as there is at least one other Administrator remaining in the system.

## [Roles and Permissions](/docs/mdmft/v3.11.5/operating/RBAC-role-base-access-control-permissions#roles-and-permissions)

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

**User Manager**:

- A read-only user administration role: can view Local, Active Directory, External and Guest users, and the Groups page, but cannot create, edit, delete, enable or disable any account
- Can view the User Mapping of users, without changing it
- Has access to General Audit, including CSV export, but not to File Audit, and cannot change the audit settings
- Can manage their own files in My Files and access Shared With Me, but has no access to Trash
- Has no access to Processing History, Dashboard, Supervisor Approval, Outbreak Prevention, Trusted Network List, Notifications, Automation or Settings
- Can be assigned by an Administrator, or automatically through an Active Directory group or a Single Sign-On user mapping

|  | Admin | Read Only Administrator | Restricted Administrator | IT Helpdesk | Auditor | User | Global Supervisor | Verdict Supervisor | Automation Coordinator | User Manager |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Processing History | Full | Filename and tag | Full **[6]** | N/A | Full **[1]** | N/A | N/A | Full**[8]** | N/A | N/A |
| Users | Full | View | Create / Remove / Edit | Create / Remove / Edit | Self created External / Guest | Self created External / Guest | Self created External / Guest | Self created External / Guest | N/A | View **[9]** |
| Supervisor | Full | View | Full | Process Setup | N/A | When Supervisor | Full **[5]** | Full **[5]** | When Supervisor | N/A |
| Outbreak Prevention | Full | View | Full | Full | Full **[2]** | N/A | N/A | N/A | N/A | N/A |
| Trusted Network | Full | View | Full | Full | N/A | N/A | N/A | N/A | N/A | N/A |
| Notifications | Full | View | Full | Full | N/A | N/A | N/A | N/A | N/A | N/A |
| Audit | Full | View | Full | Full | Full **[2]** | N/A | N/A | N/A | N/A | General Audit **[10]** |
| Recycle Bin / Archive | Full | View | Own files in trash | Own files | Full **[3]** | Own files | Own files | Own files | Own files | N/A |
| Settings | Full | View | Full **[7][4]** | Full **[4]** | N/A | N/A | N/A | N/A | N/A | N/A |
| SFTP Integrations | Full | View | Full | Full | N/A | N/A | N/A | N/A | View them at Jobs | N/A |
| MFT Integrations | Full | View | Full | Full | N/A | N/A | N/A | N/A | View them at Jobs | N/A |
| Jobs | Full | N/A | Full | Full | N/A | N/A | N/A | N/A | Full | N/A |
| My Credentials | Full | N/A | Full | Full | N/A | Local MFT API key | N/A | N/A | Full | N/A |
| Dashboard | Full | Full | N/A | Full | N/A | N/A | N/A | N/A | N/A | N/A |

**[1]** Full - But without Revoke/Approve/Delete/Permanently Delete/Archive File

**[2]** Full - But without Settings

**[3]** Full - But without Restore/Delete/Permanently Delete

**[4]** Full - But without API keys

**[5]** Full - Without the ability to delegate other supervisors

**[6]** Full - Without the ability to preview of download other user's files

**[7]** Full - Without settings import/export

**[8]** Full - Without the ability to Archive/Delete/Permanently Delete

**[9]** View - All user types and Groups, without the ability to create, edit, delete, enable or disable accounts

**[10]** General Audit - Without File Audit, and without the ability to change the audit settings

Info

The last-created local administrator's role cannot be changed.

Only Administrators can assign the User Manager role. Its access to User Management and Shared With Me cannot be removed by group File Policies, while the file-related policies (sharing, folder creation, folder renaming, Trash) apply to it as they do to a regular user.

Warning

When an existing user's role is changed to Automation Coordinator, they will lose access to manage any guest or external users they previously created.
