<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/configuration/roles -->

# Roles

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Roles can be assigned to users. This simplifies controlling permissions. The Roles tab lists the existing roles in the system.

## Default roles

After installation the following default roles are created with the following parameters:

| Rolename | Display name | Default member username | Permissions |
| --- | --- | --- | --- |
| admin | Administrators | admin | Full on all functions |
| security_admin | Security administrators |  | Full on Update history, Engines, Update settings functions |
| security_auditor | Security auditor |  | Read-only on all functions |
| help_desk | Help desk |  | Read-only on Update history and Engines functions |

## Permissions

Each role has a set of rights associated to it. Each of these rights represent the level of access to the appropriate function of Metadefender Update Downloader Web Management Console.A right can be set to one of three different states:

- **None:** users of this role have no right to access the given function of Metadefender Update Downloader Web Management Console. The menu belonging to the function is not displayed for the users of this role.
- **Read-only:** users of this role have right to access the given function for observation purposes only. Users of this role can, however, not effectuate any modifications or any change to the function.
- **Full:** users of this role have full access to the given function, including viewing any data belonging to it and modifying its configuration.

## Functions

Besides listing existing roles the **Roles** tab provides the following functions:

- Add new role
- Modify (and view) existing role
- Delete existing role

Note

The default role **Administrators** can not be deleted or modified.

## Modify role

Warning

The users' permissions won't be modified during the session, even if one of their roles are modified in the meantime.

For example:

1. A user is assigned to the role *security_admin* and has Full permissions on C_onfig history_
2. She can see *Config history* changes
3. During her session the *Config history* permissions are set to *None* for the *security_admin* role.
4. The logged in user can still select the *Config history* menu and can see the configuration changes there.

Then new permissions will be effective only after a logout and new login.

## Delete role

Note

A role can not be deleted as long as it is assigned to any user.

As a consequence deleting a role can not affect active sessions of users.
