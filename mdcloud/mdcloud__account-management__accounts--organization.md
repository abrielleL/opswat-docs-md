<!-- source: https://www.opswat.com/docs/mdcloud/account-management/accounts--organization -->

# Accounts' Organization

Feature available under professional and enterprise licensing plans only. MetaDefender Cloud license limits are controlled by the organization.

Info

Before adding a new user in the Organization, please make sure that the user is registered at https://id.opswat.com/register .

Accounts' Organization is a logical grouping of multiple user accounts of the same organization. Available features :

- Add users under an organization
- Allowlist IP addresses to MetaDefender Cloud APIs for the entire organization

OPSWAT currently supports two types of accounts:

- Individual users without an organization
- Individual users belonging to an organization (supports multiple roles with RBAC - role based access control)

## [How to Request to Create an Organization](/docs/mdcloud/account-management/accounts--organization#how-to-request-to-create-an-organization)

Organization requests need to be raised via Support Case from the [OPSWAT portal](https://id.opswat.com/login?app=appPortal0001&RelayState=https://id.opswat.com/login?app=appPortal0001&SAMLRequest=lVJNb9swDL3nVxQ67OZYloPGFeIMWbOPAFkaJOkOvRSKTLcCZEkT6XX993Psbu0GtMAICBDI9x7JJ81QNTbIRUv3bgffW0AanXXxs7EOZV8sWRud9AoNSqcaQEla7hdf11KMuQzRk9fesn9ob7MUIkQy3g201bJkV5uP66vPq82tEufVJDvWxSQv%2BAUXxYRzkU%2Bnx%2FNpkeccRAY1XOh6oH6DiJ1OyTpZNhrUEFtYOSTlqMtzkSW8SMTkIITMcimym4G67JY1TlFPvycKKNPUVGMf8EHRWPsmtf7OuPcqhLI7Wx9JWc559m4HVj3uSRGU%2F0UcGm%2BfPPtgXGXc3dtWHQcQyi%2BHwzbZQWUiaBqEFr9tvPQO2wbiHuIPo%2BF6t37eKPTdXw6nNCanN2LzXmV2usvetTh%2FQluvlZ2lLyvP2CA33Zir5dZbox%2F7%2FCk%2B%2Bdgoen2bbJz1GVMldQ%2BVrcMA2tQGKvZHZmGtf7iMcDKXUWyBnaXz0TDL3z91%2Fgs%3D&RelayState=https%3A%2F%2Fportal.opswat.com%2Flogin-saml). For it you need to be registered.

- Access the [OPSWAT Portal](https://portal.opswat.com/)
- Click on “Support” which will take you to the OPSWAT Support Portal

- Click on the "New" button to create a new case

- Select "OPSWAT Portal" as the record type

- In the subject field, type the words "New Organization"
- In the description, type the message saying "I would like to be first admin for this organization". Also state the organization name and your email address.
- Select "Severity 4"
- Click "Save"

After submitting the case to create an organization, our customer support team will create the organization.

## [How to Add a User to an Organization](/docs/mdcloud/account-management/accounts--organization#how-to-add-a-user-to-an-organization)

- Navigate to the profile page
- Click “+ Add User” button

- Include the user's email and the role:

  - User - Individual account that belongs to the organization
  - Admin - Administrator of the organization account

## [How to add IPs to the IP Allowlisting](/docs/mdcloud/account-management/accounts--organization#how-to-add-ips-to-the-ip-allowlisting)

Info

availability is subject to different licensing.

- Navigate to “Security Rules”
- Click “+ Add IP Range” - designating the Classless inter-domain routing (**CIDR**) allowed IP ranges.
