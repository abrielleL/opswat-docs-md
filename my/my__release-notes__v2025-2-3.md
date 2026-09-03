<!-- source: https://www.opswat.com/docs/my/release-notes/v2025-2-3 -->

# v2025.2.3 - Jun 12th

| **Version** | 2025.2.3 |
| ---- | ---- |
| **Release date** | June 12th, 2025 |
| **Release Summary** | This release introduces an updated data retention policy, improved access controls, and enhanced case submission for a more efficient Portal experience. |

## New Features

### 1/ Updated Retention for False Detection Submission

My OPSWAT Portal now implements a new data retention policy for False Detection Submissions

- Submissions with statuses **CONFIRMED BENIGN, CONFIRMED MALICIOUS,** or **REJECTED** will have their associated files automatically removed 90 days after the submission date.
- Submissions with statuses **IN QUEUE, IN PROGRESS,** or **INCONCLUSIVE** will have their associated files removed after 365 days from the submission date.

## Bug Fixes and Enhancements

Bug Fixes **UI Fix for Smaller Screens**

Resolved an issue where users could not filter support ticket status due to UI overlap on 13-inch screens.

Enhancements **Rich Text Support in Case Descriptions**

The Description field in the Submit a Case form now supports bolding, bullets, and hyperlinks for more precise issue reporting.

![](https://uploads.developerhub.io/prod/JYvy/l5mwxehg890orudrs4yj3b2dzpcprq8xjixksm6gjwjgwoewx3bv7dgg9n5firal.png)

EnhancementsBlocking Generic Domains in Approved Email Domains

To prevent exposing your organization broadly, we now block the use of below **generic email domains** in the **Company Email Domain** field  under **My Organization > General Information**.

`"gmail.com", "yahoo.com", "hotmail.com", "outlook.com", "aol.com", "icloud.com", "mail.com", "protonmail.com", "facebook.com", "msn.com", "live.com", "gmx.com", "zoho.com"`

![](https://uploads.developerhub.io/prod/JYvy/q38vuy1rsg75bc6i94m9alcls9wte3w3dpgy0tq258yg7l73fpuo0mk7vvrwlsbw.png)

Other bug fixes and enhancements
