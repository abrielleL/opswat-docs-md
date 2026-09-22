<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/is-kiosk-active-directory-integration-possible- -->

# Is Kiosk Active Directory integration possible?

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows or Linux systems.

In order to perform a successful Kiosk Active Directory (AD) integration, the following steps must be followed:

1. Navigate to the Kiosk console to **User Management** > **Add new directory**

2. Select **Type of directory** > **Active Directory (AD)**

3. Fill in the correct credentials and select **Test connection** to make sure the AD server is reachable from the Kiosk side)

Tip:

Instead of entering a fixed password for the directory's service account, you can set **Privileged access management manager** to **BeyondTrust Password Safe** and provide your BeyondTrust host, API key, and the managed system/account that holds this credential. MetaDefender Kiosk will then retrieve the current password from BeyondTrust automatically each time it connects to Active Directory, so logins keep working through your normal BeyondTrust password-rotation schedule without any changes on the Kiosk side.

4. The next page allows you to assign users to either the **Administrator** or **Auditor** role.

5. The next page you can see the **Summary**, and click **Submit**

6. After completing the steps mentioned above you should get the following confirmation of the **Directory saved successfully**.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
