<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-access-metadefender-core-when-sso-fails- -->

# How to access MetaDefender Core when SSO fails?

This article applies to all MetaDefender Core version 5.0 and newer releases deployed on Windows and Linux systems.

📄 **Overview**

When Single Sign-On (SSO) is configured in **MetaDefender Core**, there may be situations where login attempts using SSO fail due to configuration errors, identity provider issues, or connectivity problems. To ensure continued access to the system for administrative purposes, MetaDefender Core provides a **backup login page** that bypasses the SSO flow.

This article outlines the issue and provides instructions for accessing the backup login page to perform diagnostics or disable SSO if needed.

🚨 **Problem Description**

Users are unable to access MetaDefender Core via SSO authentication. The following symptoms may be observed:

- Redirect loops or timeouts when attempting to log in
- HTTP 500 Internal Server Errors
- Login page not loading
- No access to UI for corrective actions

✅ **Solution: Access the Backup Login Page**

MetaDefender Core includes a **backup login page** which allows direct access using local credentials (i.e., those stored in the Core database) — bypassing the SSO mechanism.

🔗 **How to Access:**

Replace <mdcore-host> with your actual MetaDefender Core hostname or IP:

https://<mdcore-host>:8008/#/public/backuplogin

For example: https://localhost:8008/#/public/backuplogin

📥 **Use This Page To:**

- Log in with a local administrator account
- Access system settings
- Review or modify SSO configuration
- Revert to local authentication if needed

🛠️ **How to Disable SSO (If required)**

Once logged in via the backup login page:

1. Go to **User Management → Directories**.
2. Disable SSO temporarily by toggling the SSO name off.
3. Save the changes.

📌 **Best Practices**

- Test SSO settings in a staging environment before production deployment.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
