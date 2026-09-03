<!-- source: https://www.opswat.com/docs/my/partner-guide/customer-organizations-licenses -->

# Customer License Management

> **Who can use this feature?**
>
> - **User type:** [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Organization type:** Partner Organization having assigned customer’s organizations.
> - **Role:** View Only/Full Access on [License Management - Customer Organizations](https://www.opswat.com/docs/my/my-organization/single-organization#role-objects-and-permissions)

**In this article:**

1. [Generating License Reports](https://www.opswat.com/docs/my/partner-guide/customer-organizations-licenses#generating-license-reports)
2. [Overview interactive charts](https://www.opswat.com/docs/my/partner-guide/customer-organizations-licenses#overview-interactive-charts)
3. [Detailed lists of product licenses](https://www.opswat.com/docs/my/partner-guide/customer-organizations-licenses#detailed-lists-of-product-licenses)
4. [Actions](https://www.opswat.com/docs/my/partner-guide/customer-organizations-licenses#actions)
5. [License Expiration Notifications](https://www.opswat.com/docs/my/partner-guide/customer-organizations-licenses#new-license-expiration-notifications)

Some customers purchase OPSWAT product licenses through Distributors or Resellers. The **Customer Organizations** tab lets Partners (Distributors and Resellers) view and manage the licenses they’ve sold to customers.

To access this page, navigate to **License Management > Customer Organizations.** You can only access this tab if the following conditions are met:

- You must belong to a **Partner organization** with assigned customers.
- You must have **View Only** or **Full Access** permission on the **License Management - Customer Organizations** role object. (Refer to [Roles](https://www.opswat.com/docs/my/partner-guide/partner-role-management#custom-roles) for details)

### Generating License Reports

![](https://uploads.developerhub.io/prod/JYvy/sow2bm79xrsbs38v5z61tffdutnp0lanqo7p7968caadppothrut3bsucu7sg065.png)

1. **Select Organizations:** Choose one or more customer organizations from the dropdown.
2. **Generate Report:** Click Generate Report.
3. The page is separated into **2 sections**:

- **Statistical charts:** Interactive charts and summary statistics.
- **Details** (including Cloud Services and On-premises product): Detailed list of licenses on each customer organization satisfied the prior selection.

### Statistical charts

![](https://uploads.developerhub.io/prod/JYvy/98w3bmj7ewat2gdd9no06gkap1vlbntbi61xs2lbw1wl765eotlxndgcvaszfh50.png)

- Hover over pie chart for details
- Click dashboard numbers or pie sections to filter data
- Page scrolls automatically to filtered results in the Details section

### Detailed Lists of Product Licenses

![](https://uploads.developerhub.io/prod/JYvy/a0uvcpecxpwr4oz9u1b0xx52lmoykeshtnfm14uom1dbkzt4iuf0zb9xyiwh3qmk.png)

The list are separated into 2 sections: **Cloud Services** and **On-Premises Products**

#### Cloud Services

- **MetaDefender Cloud:** Shows license expiration and scan limit info

#### On-Premises Products

Each license entry includes:

| Field | Description |
| ---- | ---- |
| Reseller Info | Name of the Reseller tied to that sub‑organization |
| Contract number | Contract number(s) tied to sub-organization (Activated/Expired). Click to view details in [Customer Contracts](https://www.opswat.com/docs/my/partner-guide/customer-contracts) tab. |
| Product Name | OPSWAT product name |
| License Key | Associated license key(s) |
| Status | Active, Expiring or Expired. |
| Start Date (UTC) | License effective date |
| Expiration Date (UTC) | License expiration date Please note License start and expiration dates are shown in UTC (UTC+0) for consistency across all environments and time zones. This may look different from other features of My OPSWAT Portal that use your local time zone. |
| Deployed / Purchased | Number of deployed instances versus purchased limit. |
| Type | Evaluation/Purchased - **Evaluated Licenses:** Temporary licenses used for evaluating a product. - **Purchased Licenses**: Licenses for on-premises products that have been purchased by the user account. |
| Customer Note | Notes from end customer (read-only) |
| Partner Note | Editable field for partner remarks (e.g., contract ID, location) |

> **License Display Rule:**
>
> Licenses assigned to both main and sub-organizations appear only under the sub-organization (to avoid duplication)

### Actions

Depending on your permission level on the **License Management – Customer Organizations** role object, you have access to different actions:

#### With *View Only* permission

- **Activate License** – Activate a license for the selected product. Please refer to [Activate License](https://www.opswat.com/docs/my/license-management/activate-license) for details.
- **Pin** – Move license to top for quick access
- **See Full License History** – View full history (expired hidden by default)
- **Filter** – By product name, status, type, availability, capacity
- **Search** – By license key, product name, contract number, reseller name

#### With *Full Access* permission

- **Edit partner note:** Add custom notes (e.g., location, identifiers, reseller references)
- **Download Active Deployment Report** – Export Excel file with license key info and active deployments (not applicable for Expired licenses)

## License Expiration Notifications

My OPSWAT Portal provides function which Partners can subscribe to receive automatic alerts for upcoming customer license expirations—**60 and 30 days in advance**, enabling better planning and prioritization.

**Settings:** Subscription settings available under ***License Management > Customer Organizations***

![](https://uploads.developerhub.io/prod/JYvy/qrhe5a0kj6uagohfl5hyjeovz3errgjx6jezdq8829lyy7vg49zw7fgpbhbxtcr3.png)

> **Info**
>
> In the email alert, Distributors will also see Resellers  info associated with each customer.

License details are displayed in a clean table format, including product name, license key, start date, expiration date, quantity, and license type (Evaluation or Purchased). Each customer’s licenses are organized into separate tables for easy reference.

![](https://uploads.developerhub.io/prod/JYvy/rjnroryorry1wmtisiyawsae0rdk7n5x8pcnhwid1np4u6gub7pgsi8tyukz3auh.png)
