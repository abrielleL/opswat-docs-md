<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/user-management/managing-roles -->

# Managing Roles

To manage roles in **MetaDefender OT Security**, navigate to: **User Management → Roles** in the Web Management interface.

## [Default Roles](/docs/md-ot-security/v4.0.0/user-management/managing-roles#default-roles)

User Roles & Permissions in MetaDefender OT Security

| **Role** | **Description** |
| --- | --- |
| Super Admin | Has **full permissions** within the application, including **user management**. |
| Admin | Has **full permissions**, except for **user management**. |
| Operator | Has **full permissions**, except for **user management, network settings, and general settings**. |
| APIClient | Has **specific API permissions** as defined. |

Can create roles manually in **MetaDefender OT Security** by following these steps:

## [Steps to Create a Custom Role](/docs/md-ot-security/v4.0.0/user-management/managing-roles#steps-to-create-a-custom-role)

1. **Navigate to User Management** Go to **User Management > Roles** in the Web Management interface.
2. **Create a New Role** Click on the **"Create Role"** button. Enter a **Role Name** (e.g., "Custom Operator"). Provide a **Description** (optional).
3. **Assign Permissions** Select the specific **permissions** for the role. You can allow or restrict access to features like **User Management, Network Settings, API Access, and General Settings**.
4. **Confirm** Click **"Confirm"** to create the role. The new role can now be **assigned to users**.

#**Note:** Only **Super Admins** can create and manage roles manually.
