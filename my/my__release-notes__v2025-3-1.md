<!-- source: https://www.opswat.com/docs/my/release-notes/v2025-3-1 -->

# v2025.3.1 - Jul 10th

| **Version** | 2025.3.1 |
| ---- | ---- |
| **Release date** | July 10th, 2025 |
| **Release Summary** | This release brings **homepage dashboard enhancements** for greater visibility and **configurable event history retention settings** to support compliance and data management. |

## New Features

### 1. Upgraded Homepage Status Dashboard

![](https://uploads.developerhub.io/prod/JYvy/sa280wvvu4pcp7t0gaz6uuoojv047zqo25metk3593apoynn6q6zttvomvvvjyv5.png)

The Homepage Status Dashboard has been enhanced to display two new sections

- **System & Account Notifications**: Quickly spot important system updates and account notices, such as product lifecycle notifications, password expiration reminders, and prompts to enable MFA or review organization access right at the top of your homepage.
- **Learning Progress:** Track your current tier, level, course enrollment, and course completion status.

**Further reading:**

- [System & Account Notifications](https://www.opswat.com/docs/my/overview/overview#a-system--account-notifications)
- [Learning Progress](https://www.opswat.com/docs/my/overview/overview#c-learning-progress)

### 2. Configurable Data Retention for Event History

![](https://uploads.developerhub.io/prod/JYvy/5m2ndsgquvclcadbyl5dx5bsbyeeg2pogzebk5816p1ap05yzch7yrjf0zzc7ibh.png)

Organization Admins can now configure how long event history is retained for their organization. By default, event history will be kept for **30 days**. Admins can adjust the retention period to any value between **1 and 365 days** to meet their organizational data needs.

> **Warning**
>
> This policy takes effect immediately. All existing event history will expire **30 days** after this release date unless the retention setting is updated.

**Access path**: My Organization > Security > Data Retention

**Further reading:** [Data Retention](https://www.opswat.com/docs/my/my-organization/security#data-retention)

## Bug Fixes and Enhancements

Enhancements **Remove "My Tagged Products", "Cloud Services" and "On-premises Products" from Overview page**

The list of OPSWAT products previously shown on the Overview page has been removed. You can still access Product details page either from **Product Downloads** or **License Management** page.

Enhancements **Navigation Update: Default Organization Section Moved**

The **Default Organizations** section previously located under *My Information > Personal Information* has been renamed to **My Current Organizations** and moved to *My Information > Organizations*

Other bug fixes and enhancements
