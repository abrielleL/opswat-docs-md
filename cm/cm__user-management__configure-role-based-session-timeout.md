<!-- source: https://www.opswat.com/docs/cm/user-management/configure-role-based-session-timeout -->

# Configure Role-Based Session Timeout

My OPSWAT Central Management provide capability to configure session timeout settings independently for each user role, enabling more flexible session management across different user types and use cases.

## Configure Session Timeout for a Role

1. Log in to My OPSWAT Central Management as an administrator
2. Navigate to **User Management** → **Roles**
3. Create a new role or edit an existing custom role
4. Enable **Custom Session Timeout**
5. Enter the desired session duration (in minutes)
6. Click **Save**

![](https://uploads.developerhub.io/prod/97qW/dturz94iz6nlzx5dz8nalsw85m4a5q17xo2ud79mc2f95bh7e50rg95lwkkh9v2d.png)

## **Assign the Role to a User**

1. Navigate to **User Management** → **Users and Groups**
2. Edit the target user
3. Assign the role configured with the desired session timeout

![](https://uploads.developerhub.io/prod/97qW/1odiltly1jqm82si9e8slx9n0csty17itldrpapgjobk5d7lajggsmfz2ne1n7iy.png)

4. Save the change
5. The new session duration will apply the next time the user signs in.

## **Session Behavior for User Roles**

**Default Roles**

- Continue to u*s*e the standard session timeout behavior.
- Sessions may be automatically refreshed while users remain active.
- Inactive users may be prompted to extend their session before being signed out.

**Roles with Custom Session Timeout**

- The configured session duration is applied to the user's login session.
- Session extension is not available.
- Users are automatically signed out when the configured session duration is reached, regardless of activity.
