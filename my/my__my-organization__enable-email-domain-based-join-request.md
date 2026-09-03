<!-- source: https://www.opswat.com/docs/my/my-organization/enable-email-domain-based-join-request -->

# Enable email domain-based join requests for my organization

> **Who can use this feature?**
>
> - **User type:** [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Role:** Full Access on [Organization General Information](https://www.opswat.com/docs/my/my-organization/single-organization#role-objects-and-permissions)

As an organization admin or user with **Full Access** on **Organization General Information** (See [Roles](https://www.opswat.com/docs/my/my-organization/single-organization#custom-roles) for details), you can allow users who share the same email domain(s)—such as your organization's domain(s)—to find and request to join your organization by **setting up an approved email domain** in your General Information settings.

> **Tip**
>
> Your email domain is the part of your email address that comes after the @ symbol and is usually shared by all members of a given organization. If your email address were [abc@opswat.com,](mailto:janesmith@acmecorp.com,) your email domain would be *opswat.com*.

### How It Works

When you set up an approved email domain for your organization, anyone with this email domain will be informed about your organization and prompted to submit a request to join it.

The first time a user logs in after you set up your approved email domain, **a notification banner** will appear on the **Overview** page after a few seconds of activity, informing the user that they are eligible to join your organization.

![](https://uploads.developerhub.io/prod/JYvy/hgktc2i0kb3nzimio4p2s8t22202jw9w99nd5ss9gkukhdfjvm9pgqnvmq7lezoj.png)

If the user clicks **Request access**, they will be taken to the **Organizations** page to submit their request.

![](https://uploads.developerhub.io/prod/JYvy/si9zrn36amyoaxn47jcx77x50oeo5w7bobtu7k35oqlcn62swymbkrxspibq36jg.png)

If the user clicks **Request to Join**, you and any other authorized users in your organization will receive an email notifying you of their request. See [Manage Join Requests](https://www.opswat.com/docs/my/my-organization/enable-email-domain-based-join-request#manage-join-requests)  below for next steps.

### Add an Approved Email Domain

![](https://uploads.developerhub.io/prod/JYvy/vybqxt907t74ilm8d6nqafytel19ifa4m515s7xxxp31e7x55qntux319mz5wgiy.png)

To add an email domain for organization, take the following steps:

1. [Log in](https://my.opswat.com/) to My OPSWAT Portal
2. Navigate to **My Organization > General Information > Email Domains**
3. Click **Add my domain** (available if your domain hasn't been added yet).
4. Your domain will be added to the list.

> **Note**
>
> For security reasons, only your company domain can be added. For example, if your My OPSWAT account uses an email like [abc@opswat.com](abc@opswat.com), only **opswat.com** will be added.

When you set up an approved email domain for your organization, anyone with this email domain will be informed about your organization and prompted to submit a request to join it.

#### Blocking Generic Domains

Adding generic email domain as Company email domain may expose your organization broadly. To ensure security, we block below generic email domains.

`"gmail.com", "yahoo.com", "hotmail.com", "outlook.com", "aol.com", "icloud.com", "mail.com", "protonmail.com", "facebook.com", "msn.com", "live.com", "gmx.com", "zoho.com"`

Recommendation We recommend using the **Invite User** feature instead to maintain control over who can join your organization.

### Remove an Approved Email Domain

You can remove any email domain (s) at any time by clicking the **cross mark** icon next to the email domain.

![](https://uploads.developerhub.io/prod/JYvy/ea8tnlxfi3x38g3k0z2delipkqs6n8f6xruspzfzpeo8yagmhey800cvwn4m1td6.png)

> **Warning**
>
> Once you remove an email domain (except your account email domain), you will need to contact [OPSWAT Support](https://my.opswat.com/support) if you want to re-add it.

### Manage Join Requests

If a user submits a request to join your organization, you and any other Administrators with **Full Access to the User Management** in your organization will receive

- An email informing you of the new join request
- **AND** a notification in the    icon in the top-right corner

**To approve or decline a join request:** Please follow guideline outline at [**Accept User Request to Join Organization**](https://www.opswat.com/docs/my/my-organization/single-organization#accept-user-request-to-join-organization)
