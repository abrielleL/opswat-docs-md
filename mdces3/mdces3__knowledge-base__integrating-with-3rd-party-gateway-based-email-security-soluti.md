<!-- source: https://www.opswat.com/docs/mdces3/knowledge-base/integrating-with-3rd-party-gateway-based-email-security-soluti -->

# Integrating with 3rd Party Gateway/MX-Based Email Security Solutions

Summarize Page
## [Overview](/docs/mdces3/knowledge-base/integrating-with-3rd-party-gateway-based-email-security-soluti#overview)

When using **MetaDefender Cloud Email Security™ (MDCES)** alongside another SMTP gateway-based email security solution, it is important to configure the mail flow carefully. Improper routing can cause email loops or delivery issues, particularly when messages inspected by MDCES are returned to the first-line (MX) security gateway.

This article explains how to integrate MDCES with third-party email gateway security services and prevent mail loops by configuring MDCES to return processed messages directly to Microsoft 365.

## [**Problem**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-gateway-based-email-security-soluti#problem)

Email loops may occur when MDCES processes messages that have already passed through another email security gateway and then routes those messages back to the same gateway.

For example:

**Internet → Third-Party Email Gateway → Microsoft 365 -> MDCES → Third-Party Email Gateway → Microsoft 365 → ...**

This can result in:

- Duplicate email scanning
- Increased latency or delivery delays
- Potential delivery failures or message rejection
- Infinite mail loops in extreme cases

To prevent this, messages processed by MDCES should be routed to the final Microsoft 365 SMTP endpoint rather than back to the third-party gateway.

## [**Solution**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-gateway-based-email-security-soluti#solution)

### [**Step 1: Collect Microsoft 365 SMTP endpoints**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-gateway-based-email-security-soluti#step-1-collect-microsoft-365-smtp-endpoints)

Before modifying MDCES routing, identify the Microsoft 365 SMTP/MX endpoint for each domain that MDCES needs to deliver mail to.

To find the endpoint in the **Microsoft 365 admin center**:

1. Sign in to the **Microsoft 365 admin center**.
2. Select **Show all > Settings > Domains**.
3. Select the domain you want to configure.
4. Select **DNS records**.
5. Locate the **MX** record used by **Exchange / Exchange Online Protection**.
6. Copy the value displayed in the **Points to address**, **Target**, or equivalent field.

The endpoint can look similar to:

`contoso-com.mail.protection.outlook.com`

or, for domains using Microsoft's newer Exchange Online DNS infrastructure:

`contoso-com.<subdomain>.mx.microsoft`

Always use the exact MX target displayed by Microsoft 365 for the domain rather than constructing the hostname manually.

If multiple accepted domains are configured in Microsoft 365, repeat these steps for each domain that requires a separate routing destination.

### [**Step 2: Update Mail Routing in MetaDefender Cloud Email Security**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-gateway-based-email-security-soluti#step-2-update-mail-routing-in-metadefender-cloud-email-security)

Update the relevant MDCES integration routing:

1. Sign in to **MetaDefender Cloud Email Security**.
2. Navigate to **Settings > Integrations**.
3. Select the relevant integration.
4. Select **Edit Routing**.
5. For each protected domain, change the destination to the corresponding **Microsoft 365 SMTP/MX endpoint** collected in Step 1.
6. Verify that the destination does **not** point back to the third-party SMTP security gateway.
7. Save your changes.

The expected mail flow should now be:

**Internet → Third-Party Email Gateway → Microsoft 365 -> MDCES → Microsoft 365 -> Mailbox**

## [**Important Considerations**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-gateway-based-email-security-soluti#important-considerations)

- Always copy the Microsoft-provided MX target for the specific domain.
- If multiple Microsoft 365 domains are protected by the same MDCES integration, verify the routing configuration for each domain.
