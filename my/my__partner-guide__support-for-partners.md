<!-- source: https://www.opswat.com/docs/my/partner-guide/support-for-partners -->

# Support for Partners

> **Who can use this feature?**
>
> - **User type:** [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Organization type:** Partner Organization having at least one linked customer with a Partner relationship
> - **Role:** **Full Access** to **Support Service - Customer Cases**

The **Support** feature enables partners to submit and manage support cases on behalf of their customers. You can log issues, attach logs and evidence, add comments, escalate cases to OPSWAT, and track resolutions. This makes it easier to act as a single point of contact and help customers resolve issues faster.

This page covers partner-specific actions, prerequisites, and quick how-tos. For the full Support guide, see the main [Support](https://www.opswat.com/docs/my/support-services/support-services) page.

- [**Create cases**](https://www.opswat.com/docs/my/partner-guide/support-for-partners#log-a-case-on-behalf-of-a-customer) — capture customer details, product, severity, attachments.
- [**Customer cases list**](https://www.opswat.com/docs/my/partner-guide/support-for-partners#monitor-your-customer-cases) — filter by customer, status, severity, or date.

### Permissions

**Required to submit cases for customers**

- **Full access** on the **Support Service — Customer Organizations** role object.
- Your partner organization must have at least one linked customer with a **Partner** relationship

**To view customer cases submitted by other members in your partner organization**

- **View only** or **Full Access** on the **Support Service — Customer Cases** role object.

👉 For how to assign or request these roles, see [Roles & Permissions](https://www.opswat.com/docs/my/partner-guide/partner-role-management)

### Log a Case on Behalf of a Customer

**Path:** My OPSWAT Portal → Support (Left menu) → Submit Case button

![](https://uploads.developerhub.io/prod/JYvy/e5x3ebbjwc79dparh4jmu4apbdmnwyunpt4ufzncvuo9q1242pf2ni93fgpo63in.png)

| Step | Field | Description |
| ---- | ---- | ---- |
| 1 | Choose organization | Select the customer organization you’re submitting on behalf of. ![](https://uploads.developerhub.io/prod/JYvy/in7gj3gridrtas244jtmzt7i0y7dkhhlvuw4qduc5yhngidpaayu1cr411qifz7z.png) |
| 2 | Product | Choose the affected OPSWAT product. Click **More** to view the full product list. ![](https://uploads.developerhub.io/prod/JYvy/1osa7znsw9vagqmz253l5far26uei1tbg8hhxsbjc5ydloelg84c3lgab2erjkd3.png) |
| 3 | Platform (if applicable) | If the product supports multiple platforms, you’ll be prompted to select one (e.g., Windows, Linux). ![](https://uploads.developerhub.io/prod/JYvy/g5uog0arzu3eh8d97j7asul9ffa4msy76h1po0j4tabks458lta49doaolas6rk7.png) |
| 4 | Issue Type | Choose the nature of your issue, such as configuration, installation, or unexpected behavior, ensuring clear and consistent reporting. ![](https://uploads.developerhub.io/prod/JYvy/uijs82offk4ndsc9423a8aesoew2szts9q7dv7m3yelfid05kgh8z93j9naohvv1.png) |
| 5 | Severity | Indicate how critical the issue is ![](https://uploads.developerhub.io/prod/JYvy/xhpy3zxauu21ew2nra36kl0374wcpu1bh43as3542ml3eupoajm6ol3hv4s42vns.png) NoteBased on your org's support level and severity, you'll see an estimated initial response time. |
| 6 | Add License & Version | Select the license key and product version using dropdowns, or enter manually. |
| 7 | Subject & description | Provide a: - **Subject –** short, clear title (max 255 characters) - **Description** – detailed explanation of the issue (max 5000 characters) ![](https://uploads.developerhub.io/prod/JYvy/9q2n7z019dz1sp3iud9mu6ar8nwg5r5z7hexlboh9uoawwao0pcps4hv3kh1m9cv.png) |
| 8 | Review AI Suggestions (If Any) | Before submission, the AI assistant may suggest relevant knowledge base articles based on your input. If no relevant articles are found, users are directed to the next step. ![](https://uploads.developerhub.io/prod/JYvy/xsrhp9np7lj34yyxq60gevxl277zwggrh02b9d6ai46dfm87l4dn8pa6rxsllyr3.png)You can then choose **I resolved the issue** or **Continue to Submit Case**. |
| 9 | Upload Supporting Files | You can attach up to 5 files with a maximum total upload size of 2 GB. ![](https://uploads.developerhub.io/prod/JYvy/xrmuj8uxizasdcmat6p0tjtgghmbo52b9m9vq6gg80lqyzccs0ryt0v6eqfj7m2f.png) |
| 10 | Confirmation | After submitting all supporting files, you will be directed to a final screen displaying a list of successfully uploaded files. ![](https://uploads.developerhub.io/prod/JYvy/bsa6inwobxy253i05w7our11wee7eefofeb7ygbweawm2893rezddeh72kx052lg.png) You can now monitor and manage your case under the **Case summary list** section. |

### Monitor Your Customer Cases

**Path:** My OPSWAT Portal → Support (left menu) → Customer Cases list

![](https://uploads.developerhub.io/prod/JYvy/j547t2ery34urc4be8ulxyc8nvm6bn68n4oqfel21h5l3ku26g3r9smzqlcy7fsi.png)

This tab displays all cases submitted on behalf of customers by you or any other users within your organization. Please note that this tab is visible only if certain conditions are met.

- You have **View Only** or **Full Access** to **Support Service - Customer Cases** role object **AND** Your organization has at least one linked customer with a **Partner** relationship
- **OR** You have at least one customer case.

👉 For how to assign or request these roles, see [Roles & Permissions](https://www.opswat.com/docs/my/partner-guide/partner-role-management)

In this tab, you can

- Search by Case number, Product, or Subject
- Filter cases by **Product** or **Status** (Open/Closed/Waiting on me/Waiting on OPSWAT)
- Click case number to view [Case Details](https://www.opswat.com/docs/my/support-services/support-case-management#case-details)
- Export to CSV
- Access all cases with **View All**
