<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/changing-the-password-of-the-bind-user-in-the-ad-configuration-- -->

# Changing the Password of the Bind User in the AD Configuration — Will It Impact Actual User Logins?

Short answer is **No**.

This behavior is expected because OPSWAT Central Management (OCM) v7 manages Active Directory (AD) users and groups independently. Once a user or group has been added to OCM, the system does not continuously synchronize or update this information from the AD Server.

When a user logs in to OCM, the system directly verifies that user’s credentials against the AD Server. In the case of a group configuration, OCM checks whether the user is a member of the specified group and, if so, grants access.

Therefore, changing the bind user’s password will have no impact on user authentication. OCM does not rely on the bind user to resynchronize AD users or groups, nor to verify login credentials.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
