<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/roles -->

# Roles

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Roles can be assigned to users. This simplifies controlling permissions. The Roles tab lists the existing roles in the system.

## [Default roles](/docs/mdcore/v5.22.1/configuration/roles#default-roles)

After installation the following default roles are created with the following parameters:

| Role name | Display name | Default member username | Permissions on functionality | Permissions on API level |
| --- | --- | --- | --- | --- |
| admin | Administrators | admin | Full on all functions | Be able to fetch scan result submitted by anyone Be able to download processed file where original file was submitted by anyone |
| security_admin | Security administrators |  | Full on Scan history, Update history, Security rules, Security zones, Analysis workflows, Scan nodes, Engines, Update settings, Scan settings functions | Be able to fetch scan result submitted by anyone Be able to download processed file where original file was submitted by anyone |
| security_auditor | Security auditor |  | Read-only on a ll except External settings functions | Be able to fetch scan result submitted by anyone Be able to download processed file where original file was submitted by anyone |
| help_desk | Help desk |  | Read-only on Scan history, Update history, Security rules, Security zones, Analysis workflows, Scan nodes, Engines, Scan settings functions | Be able to fetch scan result submitted by anyone Be able to download processed file where original file was submitted by anyone |

## [Permissions on functionality](/docs/mdcore/v5.22.1/configuration/roles#permissions-on-functionality)

Each role has a set of rights associated to it. Each of these rights represent the level of access to the appropriate function of Metadefender Core Web Management Console. A right can be set to one of three different states:

- **None:** users of this role have no right to access the given function of Metadefender Core Web Management Console. The menu belonging to the function is not displayed for the users of this role.
- **Read-only:** users of this role have right to access the given function for observation purposes only. Users of this role can, however, not effectuate any modification or any change to the function.
- **Full:** users of this role have full access to the given function, including viewing any data belonging to it and modifying its configuration.

## [Permissions on API level](/docs/mdcore/v5.22.1/configuration/roles#permissions-on-api-level)

Each role has a set of rights pertaining to REST API access level, including following REST endpoints:

**Processing result fetching:**

- GET /hash/<md5, sha1, sha256> ( [GET File Analysis](/docs/mdcore/v5.22.1/metadefender-core#fileanalysisget))
- GET /file/<data_id> ( [GET File Analysis](/docs/mdcore/v5.22.1/metadefender-core#fileanalysisget) )
- GET /file/batch/<batch_id> ( [GET Status of Batch Analysis](/docs/mdcore/v5.22.1/metadefender-core#batchstatus))
- GET /stat/log/scan (Leveraged by Core management console)
- GET /stat/log/scan/export (Leveraged by Core management console)

**Download processed file:**

- GET /file/converted/<data_id> ( [GET Download Sanitized Files](/docs/mdcore/v5.22.1/metadefender-core#sanitizedfile))
- GET /file/processed/<data_id> (Leveraged by Core management console)

A right can be set to one of three different states:

- **None:**

  - Users of this role have no right to access the given REST APIs (return "Access denied" error) and relevant functionalities on Metadefender Core Web Management Console
  - **Note:** When "NONE" is selected for "Processing result fetching", "Processing history" menu item under Dashboard will automatically switch to "READ-ONLY" right, and "FULL" right will instead be disabled for selection ("FULL" right can be only enabled for selection back when this option is switched to "ANYONE")

- **Self-only:**

  - Users of this role only have right to access the given REST APIs and relevant functionalities on Metadefender Core Web Management Console where the scan requests were submitted by themselves only
  - Users of this role have no right to access the given REST APIs (return "Access denied" error) where scan requests were submitted by anyone else
  - **Note:** When "SELF-ONLY" is selected for "Processing result fetching", "Processing history" menu item under Dashboard will automatically switch to "READ-ONLY" right, and "FULL" right will instead be disabled for selection ("FULL" right can be only enabled for selection back when this option is switched to "ANYONE")

- **Anyone:** Users of this role have full access to the given REST APIs and relevant functionalities on Metadefender Core Web Management Console where the scan requests were submitted by anyone

## [Functions](/docs/mdcore/v5.22.1/configuration/roles#functions)

Besides listing existing roles, the **Roles** tab provides the following functions:

- Add new role
- Modify (and view) existing role
- Delete existing role

Note

The default role **Administrators** cannot be deleted or modified.

## [Modify role](/docs/mdcore/v5.22.1/configuration/roles#modify-role)

Warning

The users' permissions won't be modified during the session, even if one of their roles are modified in the meantime.

For example:

1. A user is assigned to the role *security_admin* and has Full permissions on *Config history*
2. She can see *Config history* changes.
3. During her session the *Config history* permissions are set to *None* for the *security_admin* role.
4. The logged in user can still select the *Config history* menu and can see the configuration changes there.

Then new permissions will be effective only after a logout and new login.

## [Delete role](/docs/mdcore/v5.22.1/configuration/roles#delete-role)

Note

A role cannot be deleted as long as it is assigned to any user.

As a consequence, deleting a role cannot affect active sessions of users.
