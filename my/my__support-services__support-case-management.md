<!-- source: https://www.opswat.com/docs/my/support-services/support-case-management -->

# Support Case Management

> **Who can use this feature?**
>
> **User type:** Both [Personal](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#personal-user) and [Organization](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user) users

Once you've submitted a case, you can monitor and manage it directly in the **Case Summary List.**

This guide helps you:

- View all submitted cases (yours, your organization’s, partner-submitted, and customer cases, based on your role).
- Track updates, upload files, respond to OPSWAT, escalate, close, or reopen cases.

The **Case Summary List** provides an organized view of your support cases, organized into five tabs: **My Cases, Organization Cases, Partner Cases, Customer Cases, and False Detection Submissions.**

You can view and manage support cases in the **Case Summary List**, organized into the following tabs

> **Tip**
>
> The tabs available to you depend on your **role and permissions**.

| Tab | Who can see | What it shows |
| ---- | ---- | ---- |
| My Cases | All users | Cases you personally submitted |
| Organization Cases | Organization members with permissions | All cases from your organization |
| Partner Cases | Customer organization members with permissions | Cases submitted by partners on behalf of your organization |
| Customer Cases | Partners with permissions | Cases submitted for customers |
| False Detection Submissions | All users | Auto-created cases from false detection reports |
| All cases | All users | A unified view of every case you have access to, across My Cases, Organization Cases, Partner Cases, Customer Cases, and False Detection Submissions |

> **PLEASE NOTE**
>
> **Organization Cases**, **Partner Cases**, and **Customer Cases** are displayed according to the organization you are currently viewing. Cases submitted under other organizations will not be visible unless you switch to that organization.
>
> **For example**, if you're viewing **Organization A**, you won’t see Organization Cases and Customer Cases submitted under **Organization B** unless you switch to **Organization B**.

## Case summary list

### My Cases

Available to:All users

![](https://uploads.developerhub.io/prod/JYvy/h6y9lu28tax4gcuwsn4j59c4ukit2ex90jvg58jn1atgydvorzkrdzhwopcmwl2l.png)

This tab lists all cases you've submitted. You can:

- Search by Case number, Product, or Subject
- Filter cases by **Product** or **Status** (Open/Closed/Waiting on me/Waiting on OPSWAT)
- Click case number to view case details
- Export to CSV
- Use the **Gear** icon to hide or unhide display columns.
- Access all cases with **View All**

### Organization Cases

Available toOrganization users with the **Support Service - Organization Cases** permission

Contact your admin and ask them to grant  the appropriate **Support Service - Organization Cases** permission for your account. Access can be controlled through RBAC: **My Organization > Roles**

![](https://uploads.developerhub.io/prod/JYvy/3ovizbes2qedreucbnywpppz3a4vxs4voqd45aer2fqhnbhmsxsabsc07w1q4htt.png)

This tab displays all cases submitted by members of your organization. You can search, filter, export, and customize columns the same way as [My Cases](https://www.opswat.com/docs/my/support-services/support-case-management#my-cases)

### Partner Cases

Available to  Customer organization members with the **Support Service - Partner Cases** permission

To see this list Contact your admin and ask them to grant the appropriate **Support Service -** **Partner Cases** permission for your account.

![](https://uploads.developerhub.io/prod/JYvy/3e3vi3vkxfuadqwo1qjrt5a1p29cp63b5jag3yw76bj4snihwy22e8ksrndik70x.png)

This tab shows cases that partners have submitted on behalf of your organization. It is available only to customer organizations and displays information including the Partner Name alongside standard case details. You can search, filter, export, and customize columns the same way as [My Cases](https://www.opswat.com/docs/my/support-services/support-case-management#my-cases)

### Customer Cases

Please refer to this guide: [Monitor Your Customer Cases](https://www.opswat.com/docs/my/partner-guide/support-for-partners#monitor-your-customer-cases)

![](https://uploads.developerhub.io/prod/JYvy/9bh40nx4j7n2nx22jxhrz21hbyc88t4x030r6xj9coqxsxuio3twp6ev4nf1xpos.png)

### False Detection Reports

Available to:All users

When you report a [false detection](https://www.opswat.com/docs/my/support-services/report-false-detection), the system automatically creates a support case here.

You can:

- Search by Case number and Subject
- Filter cases by **Status** (Open/Closed/Waiting on me/Waiting on OPSWAT)
- Click case number to view case details
- Click **View Detection** for more info
- Export to CSV
- Access all cases with **View All**

### RMA Cases

Available to: users with the Support Service - RMA Cases permission

![](https://uploads.developerhub.io/prod/JYvy/o9y4kun3zf3tb3bk0fbggg7ugyc7wdq1ivk3qri8ce180spl3xspk0f0aonm2wcs.png)

When you [submit a RMA case](https://www.opswat.com/docs/my/support-services/hardware-rma-requests), the system automatically creates a support case here.

You can:

- Search by Case number and Subject
- Filter cases by **Status** (Open/Closed/Waiting on me/Waiting on OPSWAT), Product or Customer name
- Click case number to view case details
- Click **View Detection** for more info
- Export to CSV
- Access all cases with **View All**

### All Cases

Available to:All users (the cases shown are scoped by your role and permissions)

This tab brings every case you have access to into one searchable list, combining **My Cases, Organization Cases, Partner Cases (for Customers), Customer Cases (for Partners), and False Detection Reports.**

Clicking any statistic on the Support dashboard (Open, Waiting on Me, Escalated, or Closed) opens this view filtered to those cases.

![](https://uploads.developerhub.io/prod/JYvy/fxr4muh9l7il5fkpxhu5wpjiat42yt0bkq3mmaf9rlch5wpx03lyqu5nljd9q6yh.png)

You can:

- Search by Case Number or Subject
- Filter by Case Type, status, and date range
- Export to CSV
- Use the Gear icon to hide or unhide display columns

## Case Details

When you click on a Case Number from any case list, you'll be taken to the **Case Detail Page,** giving full visibility into your case and lets you take follow-up actions, like uploading files, leaving comments, or escalating the issue.

![](https://uploads.developerhub.io/prod/JYvy/qtxd10ce6jxmerqyjm8r0mk2vv30qw3yqlmbc7k0wam5cfw20ffbmuye6l0d65h8.png)

| Item | Description |
| ---- | ---- |
| **Case name and description** |  |
| **Watch a Case (CC)** | Add email addresses to receive email notification on case updates ![](https://uploads.developerhub.io/prod/JYvy/1gaumt69gggl6voxnhhs3wmf5fj1ptu5jkpir3gpjrh3ablsdhskpwotwr7z45qz.png) |
| **Escalate** | Click if your case requires urgent attention. Reason for Escalation is required. |
| **Case information** | View case number, contact name, organization, assigned agent, product, platform, issue type, version, license, severity level, created date, and current status. |
| **Escalation** | Escalation status |
| **Attachments** | Upload relevant files (**up to 30 GB**) Note All uploaded files can be downloaded from this view, except for FDS files submitted during the False Detection Report process. These files are restricted due to potential security risks. Note To download a file, you must be signed in to My OPSWAT Portal as a user who can access the case. A download link on its own does not give access to the file. Warning Do not upload infected files or any files suspected of containing malware when submitting support cases. |
| **Close Case** (top-right corner) | Close case and submit ratings |
| **Reopen Case** | Click the **Reopen Case** button, provide a required comment explaining why you are reopening, and confirm. The case status changes back to Under Review. Only available to close date < 14 days |
| **Submitting a follow-up case** | This button is available for cases closed more than 14 days. Enter a short reason for the follow-up when prompted. The new case is pre-filled from the original case and is automatically linked to it, so the full history stays connected. If a follow-up case already exists for the closed case, My OPSWAT warns you so you can review it before creating another. |

## **Satisfaction Ratings**

Help improve support quality by rating your **closed cases**:

| Icon | Meaning | Action |
| ---- | ---- | ---- |
| ⭐ **Yellow Star** | Already rated | Click to update rating NoteRating can only be **updated** within **7 days** from Case Closed Date |
| Rate | Not yet rated | Click to provide feedback |
| "--" | For OPEN case (Not CLOSED status) | Rating is disabled |

> **Note**
>
> You can only rate your own **CLOSED** cases.

---

[All pages in this documentation](https://www.opswat.com/docs/my/llms.txt)
