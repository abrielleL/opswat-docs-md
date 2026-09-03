<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-do-i-log-into-opswat-central-management -->

# How do I log into OPSWAT Central Management

This article applies to all OPSWAT Central Management V7.5.0+ releases deployed on Windows or Linux systems.

OPSWAT Central Management allows administrators to manage users and groups under user directories, of which there are two default types, Local and Third Party, where:

- **LOCAL User Directories**: Manage users created locally.
- **Third Party User Directories**: Manage SSO users.

## [Standard login format](/docs/ocm/knowledgebase/how-do-i-log-into-opswat-central-management#standard-login-format)

## [Login format for the default Local user directories](/docs/ocm/knowledgebase/how-do-i-log-into-opswat-central-management#login-format-for-the-default-local-user-directories)

LOCAL directory users can log in using either of the formats displayed in the screenshots below, depending on the OPSWAT Central Management version via which each user was created.

Please Note:

Users that were created via any **OPSWAT Central Management V7+** instances must be logged in via their **User Emails**.

Please Note:

Users that were created via, and subsequently imported from, any **OPSWAT Central Management V5** instances must be logged in via their **Usernames**.

## [Login format for user defined / third party user directories](/docs/ocm/knowledgebase/how-do-i-log-into-opswat-central-management#login-format-for-user-defined--third-party-user-directories)

In the example displayed in the screenshot below, the user belongs to the **HCM CITY** user directory.

Please Note:

The format is similar for users belonging to an Active Directory group, i.e., **<Active Directory Group>< userPrincipalName>** or **<Active Directory Group>< sAMAccountName>**.

## [Login instructions for all users](/docs/ocm/knowledgebase/how-do-i-log-into-opswat-central-management#login-instructions-for-all-users)

1. Visit [This Link](http://localhost:9000/console/op/login) to access the OPSWAT Central Management Console **Login Page**.
2. Input your **Username** and/or **Email Address** in the relevant format as outlined above.
3. Input your **Password**.
4. Click **SIGN IN** or hit **Enter**.

Support:

If you have followed the instructions above but have been unable to **Log Into OPSWAT Central Management**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
