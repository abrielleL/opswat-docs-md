<!-- source: https://www.opswat.com/docs/my/release-notes/v2026-2-2 -->

# v2026.2.2 - May 5th

## My OPSWAT Portal v2026.2.2.1

| **Version** | v2026.2.2.1 |
| ---- | ---- |
| **Release date** | May 15th, 2026 |
| **Release Summary** | Security update: Applied security improvements and dependency updates |

## My OPSWAT Portal v2026.2.2.0

| Version | v2026.2.2.0 |
| ---- | ---- |
| **Release date** | May 5th, 2026 |
| **Release Summary** | This release introduces the new Trust Center - a central hub for security and compliance Information and brings OPSWAT webinars directly into My OPSWAT, so you can easily discover and register for events. Partners get a set of workflow improvements, a new Deal Registration qualification step for the METAPCIS region, and automated MDF status notifications. This release also fixes a profile update issue for SSO users and improves license visibility for users in organizations. |

## New Features

### OPSWAT Trust Center

The Trust Center provides a single place to access key trust resources and validate OPSWAT’s alignment with organizational and regulatory security requirements.

![](https://uploads.developerhub.io/prod/JYvy/uwj36m3to1xutg7d9qcwjc7thcj96q431pkzs9pt5dsje3uqy7zclcky0shpemt8.png)

Through the Trust Center, customers and partners can:

- Review OPSWAT’s security, privacy, and compliance posture in one centralized location
- Request access to compliance documentation such as SOC 2 reports, ISO certifications, and other security materials after NDA acceptance
- Submit and manage security questionnaires through a streamlined self-service workflow
- Validate OPSWAT’s alignment with internal policies, regulatory standards, and security requirements

**Access path:** Left menu > Trust Center

**Further reading:** [Trust Center](https://www.opswat.com/docs/my/trust-center/trust-center)

### Stay Updated on OPSWAT Upcoming Webinars

The Overview page now includes a Webinars section that displays upcoming OPSWAT webinars.

![](https://uploads.developerhub.io/prod/JYvy/tb2txpao48ewjieekses612ys1zeeijeujymaoy6x5ikfoxi6ff4pcginn6i985e.png)

Users can also opt in to receive webinar communications by updating their notification preferences in **My Information > Preferences**

### [For Partners] METAPCIS Deal Registration Qualification Flow

Partners in the METAPCIS region now see an additional qualification step when submitting a Deal Registration. Before submitting, partners are asked whether they have conducted or scheduled a meeting with the end customer. This helps ensure deals are properly qualified and gives partners clear guidance on next steps if a meeting has not yet taken place.

![](https://uploads.developerhub.io/prod/JYvy/yzqvcp767putp8r1q9d1kxxgn6miftphw7cpqc59s896wia56wpvkgaopo41b5ui.png)

### [For Partners] MDF Status Email Notifications

Partners now receive automated email notifications whenever an MDF request changes status. Notifications cover all key stages: New, Under Review, Approved, Completed, Denied and Aborted, Returned. This keeps partners informed of progress without needing to log in to check manually.

## Enhancements

### Personal License Visibility

Users who have joined an organization can now view both their personal MetaDefender Cloud & My OPSWAT Central Management (SaaS) license and their organization license side by side in License Management.

![](https://uploads.developerhub.io/prod/JYvy/fwr9dtefjlzrwfo4f7xg44pkpfk1pka1szemvwl90p7p8syidrkxziljxh8joumh.png)

## Bug Fixes

### IDP User Profile Update

Fixed an issue where users signed in through an Identity Provider (SSO) were unable to update their profile information, including Title, Company, Address, and Phone Number.
