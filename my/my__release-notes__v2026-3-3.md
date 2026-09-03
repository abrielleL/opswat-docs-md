<!-- source: https://www.opswat.com/docs/my/release-notes/v2026-3-3 -->

# v2026.3.3 - Aug 10th

## My OPSWAT Portal v2026.3.3.1

| **Version** | v2026.3.3.1 |
| ---- | ---- |
| **Release date** | August 14th, 2026 |

Enhancements** **Improved the password reset process to fully support users with Email Multi-Factor Authentication (MFA) enabled.

Bug fixes Other Bug Fixes and Enhancements

## My OPSWAT Portal v2026.3.3.0

| **Version** | v2026.3.3.0 |
| ---- | ---- |
| **Release date** | August 10th, 2026 |
| **Release Summary** | This release introduces **Organization-Level Conditional Access**, support for Academy case submissions, plus general bug fixes and enhancements. |

### **New Features**

#### **Organization-Level Conditional Access**

![](https://uploads.developerhub.io/prod/JYvy/0fkr3iy7ajm3tj0c9g154roffuea7at7lq0q5tae7jaun443q8kpyxs9k072py90.png)

Administrators can now control where their organization's users are allowed to access the organization from, using Allow or Block policies based on IP address, IP range (CIDR), or country. Policies apply to both users entering the organization and API or integration calls made on the organization's behalf, including OAuth applications.

Policies can also run in **Monitor** mode to observe impact before enforcing, and each access attempt is recorded in the event logs. This adds an organization-level layer of protection on top of existing controls such as Multi-Factor Authentication and account lockout.

**Access path: **My Organization > Conditional Access

**Further reading:** [Conditional Access](https://www.opswat.com/docs/my/my-organization/conditional-access)

---

### **Enhancements**

#### **Access to Archived Product Versions**

![](https://uploads.developerhub.io/prod/JYvy/0z9qusjt2a9br87td0y1sfsici1bkjyvdbe0qfce94z8obhre591cplczzc6r5j4.png)

The production download section for each product now shows the latest version by default. You shall enable the Archived toggle to see older, still-supported versions.

#### **Academy Support Access**

![](https://uploads.developerhub.io/prod/JYvy/zeqdd0fiqx508yo7eyh8dpo1exa3xj2vi5qysz06fbjy1bgkvshkdx24j3e59dcp.png)

You can now open a support case for OPSWAT Academy directly from the Portal. Academy appears as a product option in the case submission form, and the Need help? entry point is available in the Academy overview.
