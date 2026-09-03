<!-- source: https://www.opswat.com/docs/my/release-notes/v2026-2-3 -->

# v2026.2.3 - May 28th

## My OPSWAT Portal v2026.2.3.5

| **Version** | v2026.2.3.5 |
| ---- | ---- |
| **Release date** | Jun 23rd, 2026 |
| **Release Summary** | This release includes bug fixes for MFA setup. |

Bug fixes Fixed an issue that prevented some users from completing MFA setup and signing in.

Further reading at [Why can't I download my MFA recovery code?](https://www.opswat.com/docs/my/faqs/why-can-t-i-download-my-recovery-code)

## My OPSWAT Portal v2026.2.3.4

| **Version** | v2026.2.3.4 |
| ---- | ---- |
| **Release date** | Jun 17th, 2026 |
| **Release Summary** | To strengthen security, this release introduces mandatory Multi-Factor Authentication (MFA) when accessing My OPSWAT Portal and other OPSWAT Cloud products/ services. |

### Mandatory MFA for all users

Starting **June 17th, 2026**, Multi-Factor Authentication (MFA) will be required for accessing OPSWAT Cloud products and services, except for those who sign in through your organization’s own identity provider (IdP).

List of OPSWAT Cloud products and services that requires MFA:

- My OPSWAT Portal
- MetaDefender Cloud
- MetaDefender Cloud Email Security
- Filescan.IO
- My OPSWAT Central Management
- OPSWAT Academy

If MFA is not enabled on your account when accessing the products listed below, you will be prompted to complete MFA setup after signing in. To set up MFA, follow [Set up Multi-Factor Authentication](https://www.opswat.com/docs/my/my-information/set-up-multi-factor-authentication) guide.

Further reading at [Multi-Factor Authentication](https://www.opswat.com/docs/my/my-information/my-security#multi-factor-authentication)

## My OPSWAT Portal v2026.2.3.0

| **Version** | v2026.2.3.0 |
| ---- | ---- |
| **Release date** | May 28th, 2026 |
| **Release Summary** | This release introduces the capability to view active deployments for all your active license keys right in the Portal, and deactivate MetaDefender Core license deployments without contacting Support. Hardware Orders gain new filters and email notifications for customers, plus a Customer Hardware tab for partners. |

### New Features

#### Self-Service MetaDefender Core License Deactivation

Administrators can now deactivate MetaDefender Core deployment IDs directly from My OPSWAT Portal, without opening a support ticket and waiting for a response.

![](https://uploads.developerhub.io/prod/JYvy/tk05tm2c8mk90hnmqqjws7a8rz15mmggg3l7pxfnx76q59ul7hp35loxeilq6614.png)

From License Management page, you can now view all active Deployment IDs associated with a license key, then select one or multiple deployment IDs to deactivate.

![Click three dots icon next a specific license key and select **Manage Active Deployments**](https://uploads.developerhub.io/prod/JYvy/7o2r46gn01qo9nl9wxokcg4qune090tpn1fw5zedwai9j6dl9xkwi003rtobn4cv.png)

---

### Enhancements

#### View Active License Deployments in License Management

You can now view the active Deployment IDs for any license key in License Management, without downloading a deployment report.

![](https://uploads.developerhub.io/prod/JYvy/k2g168hiu62ldtkddo0orhxn9mr0n3uor58dioouakt4xtugpk0zpbi551402r52.png)

#### Enhanced Hardware Order Management

- **New filtering options:** ship date, delivery date, and shipping carrier ![](https://uploads.developerhub.io/prod/JYvy/1qei7fcufbg59upbhuhzwjckwc7b7axmrldeuoex4v33icc95jn63ecohimcwepd.png)
- **Automated email notifications for Customers** when the order is confirmed, shipped, delivered, or when the status changes, each with a direct link back to My OPSWAT Portal for full details.
- **New Customer Hardware tab for Partners** all hardware orders and inventory tied to the customers you serve.![](https://uploads.developerhub.io/prod/JYvy/npa9nm1i0wa1ki6lipezn8823vnl08yjeep7kieodm6el77u7few0uvklaa91pez.png)

---

#### Unified All Cases View in Support

A new **All Cases** tab on the **Support** page combines My Cases, Organization Cases, Partner Cases *(for Customers),* Customer Cases *(for Partners),* and False Detection Reports into one searchable list. Clicking any statistics - **Open, Waiting On Me, Escalated** or **Closed** - now opens this view with the matching filter applied.

![](https://uploads.developerhub.io/prod/JYvy/u5zg95w4ttfsa2fb5jnz14yhr871cu61zowahomxx1uo58cw25q1h7m6jc52g56o.png)

---

#### [For Partners] Bulk Resource Download in the Partner Portal

Partners can now multi-select files inside any playbook or across the **All Resources** tab and download them in a single action, making it easier to grab full kits of enablement materials.
