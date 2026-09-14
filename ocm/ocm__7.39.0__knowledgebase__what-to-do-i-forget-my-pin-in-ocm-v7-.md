<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/what-to-do-i-forget-my-pin-in-ocm-v7- -->

# What to do if I forget my PIN in OCM v7?

This article applies to all OPSWAT Central Management V7. + releases deployed on Windows or Linux systems.

If you have forgotten your **PIN** in OPSWAT Central Management V7. + the recovery method depends on your account type. Follow the instructions below based on your user role.

### [**If you are not a regular user role**](/docs/ocm/7.39.0/knowledgebase/what-to-do-i-forget-my-pin-in-ocm-v7-#if-you-are-not-a-regular-user-role)

If you are a **non-primary admin user** and have forgotten your **PIN**, you can request a **temporary PIN** through your user profile.

Follow the instructions in this support article: [How do I add or change my PIN?](https://www.opswat.com/docs/ocm/knowledgebase/how-do-i-add-or-change-my-pin-#how-to-change-your-pin-administrative-accounts-created-subsequent-to-v730-only)

### [**If you are the primary admin role**](/docs/ocm/7.39.0/knowledgebase/what-to-do-i-forget-my-pin-in-ocm-v7-#if-you-are-the-primary-admin-role)

If you’re the primary admin, you can reset the PIN by answering the security question.

However, if you’ve forgotten both the PIN and the security question answer, the only remaining recovery option is a full clean uninstallation of OCM. This will completely reset the system and allow you to set up a new instance. Here the steps:

#### [**Steps**](/docs/ocm/7.39.0/knowledgebase/what-to-do-i-forget-my-pin-in-ocm-v7-#steps)

1. **Uninstall OCM** by following the instructions in this support article: [Uninstall OPSWAT Central Management](https://www.opswat.com/docs/ocm/installation/uninstall-opswat-central-management)
2. **Delete the OCM folders** before reinstalling. The folders are located at:

`C:\ProgramData\OPSWAT\Central`

`C:\Program Files\OPSWAT\Central`

⚠️ **Note:** If the OCM folder is not deleted, the login screen may continue to appear after reinstallation.

3. **Reinstall OCM.**

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
