<!-- source: https://www.opswat.com/docs/mdcloud/operation/secure-configuration-guide--metadefender-cloud -->

# Secure Configuration Guide

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This page lists the settings and practices that keep your MetaDefender Cloud account and data secure. Each section gives our recommendations, with a link at the end to the detailed page.

MetaDefender Cloud is a shared service: OPSWAT secures the platform, and you are responsible for your account settings, users, API keys and the files you submit. See the [Responsibility Matrix](https://www.opswat.com/docs/mdcloud/compliance/responsibility-matrix) for the full split.

**1. Sign-in and multi-factor authentication**

- Multi-factor authentication (MFA) is required for every user; there is nothing to turn on.

- If your users sign in through your own identity provider (single sign-on), OPSWAT's MFA is turned off for them. Enforce MFA in your identity provider.

- To set up single sign-on, open a support case and provide your identity provider's SAML metadata and attributes.

**More:** [Bring Your Own Identity (BYOI) integration](https://www.opswat.com/docs/mdcloud/account-management/bring-your-own-identity--byoi--integration)

**2. Users and roles**

- Give each person the lowest role they need: **Analyst** (view scan results only), **User** (scan files and view results) or **Administrator** (manage users, sub-organisations and security policies). Keep the number of Administrators small.

- Remove users as soon as they leave or no longer need access, and review your user list regularly.

- Disabling a user in your identity provider does not remove them from MetaDefender Cloud. Remove them here as well and request revocation of their API key.

**More:** [Customer User Lifecycle Policy](https://www.opswat.com/docs/mdcloud/compliance/customer-user-lifecycle-policy)

**3. API keys**

- Keep API keys secret. Store them in a secrets manager or vault, never in source code, scripts, tickets or emails.

- Keys do not expire. Request rotation on your own schedule, when the person who created a key leaves, and immediately if you suspect a key has been exposed. OPSWAT Support rotates and revokes keys at your request.

- Removing a user does not revoke their key. Request revocation separately.

- After a revocation, confirm the key no longer works: the API key information endpoint must return 401 Unauthorized.

**More:** [Customer User Lifecycle Policy](https://www.opswat.com/docs/mdcloud/compliance/customer-user-lifecycle-policy) · [MetaDefender Cloud API reference](https://www.opswat.com/docs/mdcloud/metadefender-cloud-api-v4)

**4. File privacy, sharing and location**

- **Private processing** is off by default. Use it for confidential files: the file is deleted after analysis and results are visible only to you or your organisation. Paying customers can ask Support to enforce it for all scans.

- **Sample sharing** is on by default. Paying customers can turn it off per scan. With private processing, files are never shared.

- **Location:** to control where files are processed, send requests to a regional endpoint. Otherwise requests go to your nearest region, or to US West if there is none.

- **Contract end:** export the data you need (scan history and results, and sanitized files from the last 24 hours, as JSON through the API), then request account closure through the Data Subject Request form. Without a deletion request, files and results are kept for up to 10 years.

**More:** [Responsibility Matrix](https://www.opswat.com/docs/mdcloud/compliance/responsibility-matrix) · [Locations](https://www.opswat.com/docs/mdcloud/compliance/locations) · [Customer Data Offloading Policy](https://www.opswat.com/docs/mdcloud/compliance/customer-data-offloading-policy)

**5. Network restrictions and monitoring**

- **IP allowlisting:** your administrator can limit API access to your own IP ranges under Security Rules (depends on your licence).

- **Mutual TLS** (enterprise licence): requests are accepted on your dedicated endpoint only with your certificate and private key.

- **Monitoring:** check API usage on your account page regularly. Unexpected usage can mean a key has been exposed.

**More:** [Responsibility Matrix](https://www.opswat.com/docs/mdcloud/compliance/responsibility-matrix)

**6. Getting help and reporting security issues**

If you suspect a key has been exposed or see activity you don't recognise, contact OPSWAT Support straight away so the key can be revoked.

**More:** [Contact Support](https://www.opswat.com/support/contact-support) · [Tenant Isolation Policy](https://www.opswat.com/docs/mdcloud/compliance/tenant-isolation-policy) · [Secondary Use of Customer Data Policy](https://www.opswat.com/docs/mdcloud/compliance/secondary-use-of-customer-data-policy)
