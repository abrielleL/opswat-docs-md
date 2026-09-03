<!-- source: https://www.opswat.com/docs/my/others/oauth-application -->

# OAuth Application

> **Who can use this feature**
>
> - **User type:** [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Role:** Super Admin and Admin

**OAuth Application** allows you to create and manage OAuth applications in My OPSWAT Portal. You use these applications to generate Client Credentials (Client Key and Client Secret) and authenticate your server-to-server integrations with the Portal.

## Overview

To access the **OAuth Application** feature:

- Open **My OPSWAT Portal**
- Click your **Account menu** at the top-right corner.
- Select **OAuth Application**.

![](https://uploads.developerhub.io/prod/JYvy/ik8llnrqb86gtbyp4ucn60rxtxy4k2zvf2mhm7rbg3le9wb823xar9rqhvcj11wj.png)

Each application will have **App Name,** **Description,** **Created By,** **Last Updated**

You can:

- **Search** by **App Name**.
- **Sort** by **Name** or **Created Date**.

For each application, you can:

- **Update** Name and description
- **Delete** the application ![](https://uploads.developerhub.io/prod/JYvy/0k13bg8ykjb2mzid13xh6x75pxmpu5h5nd5q1rzoqi0cbhr9uoefplidi756sm71.png)

> **Info**
>
> This list shows all OAuth applications created by authorized users who has full access on OAuth applications in the organization.

## Register New Application

To create a new OAuth application:

![](https://uploads.developerhub.io/prod/JYvy/zfo7uabi0mltuigl4i40j0r8bx9lb4vv7l98cirh4vpbedapn309w196kzqz2hlj.png)

1. On the **OAuth Applications** page, click the **Register New Application** button.
2. In the creation form, enter:
   - **App Name** (required, must be unique)
   - **Description** (optional)
3. Click **Register** to create the application.

When you confirm, the system:

![](https://uploads.developerhub.io/prod/JYvy/ng23nvtl3mk7fwfyhwowvtbawyqoebn9ituzoaic2ay7c6ytwckkqsklctxx630p.png)

1. Creates a new OAuth application.
2. Generates a unique **Client Key** and **Client Secret**.
3. Encrypts the **Client Key** and **Client Secret** at rest.
4. Displays the details of the new application.

## Using OAuth credentials to call OAuth APIs

After you create an OAuth application and obtain its **Client Key** and **Client Secret**, you can use them to call OAuth APIs.

[Developer Guide](https://www.opswat.com/docs/my/2026.3.1/developer-guide/ref)
