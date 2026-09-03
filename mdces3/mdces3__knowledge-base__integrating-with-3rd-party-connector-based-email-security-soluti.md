<!-- source: https://www.opswat.com/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti -->

# Integrating with 3rd Party Connector-Based Email Security Solutions

Summarize Page
## [**Overview**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti#overview)

When using **MetaDefender Cloud Email Security ™** (MDCES) alongside other SMTP connector-based email security solutions, it's important to configure your mail flow rules carefully. Improper configuration can cause email loops or delivery issues, especially when emails are routed back to Microsoft 365 after inspection.

This article explains how to integrate MDCES with 3rd party email security services and prevent mail looping by properly adjusting MDCES mail flow rule exceptions.

## [**Problem**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti#problem)

Email loops may occur if MDCES processes emails that have already passed through another email security gateway and are then routed back into Microsoft 365. This can lead to:

- Duplicate email scanning
- Increased latency or delivery delays
- Potential delivery failures or message rejection
- Infinite mail loops in extreme cases

## [**Solution**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti#solution)

### [**Step 1: Collect IP Ranges from 3rd Party Service**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti#step-1-collect-ip-ranges-from-3rd-party-service)

Before modifying MDCES rules, obtain the public IP ranges used by your 3rd party security service to send emails back into Microsoft 365. These are typically documented by the vendor or available through their admin console.

Info

MDCES IP ranges can be found here [Service IP ranges](/docs/mdces3/compliance/locations#service-ip-ranges)

### [**Step 2: Update Mail Flow Rules in Microsoft 365**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti#step-2-update-mail-flow-rules-in-microsoft-365)

Update the relevant MDCES rules below. (Note: Only modify the rules that are present in your environment.)

- **OPSWAT MDCES - Inbound emails**
- **OPSWAT MDCES - Outbound emails**

**Action:**

- Add an **exception** to the rule based on **Sender IP address**.
- Specify the collected 3rd party IP ranges.

## [**Example: Adding an Exception to a Rule**](/docs/mdces3/knowledge-base/integrating-with-3rd-party-connector-based-email-security-soluti#example-adding-an-exception-to-a-rule)

1. Go to **Microsoft 365 Admin Center** > **Exchange Admin Center**.
2. Navigate to **Mail flow** > **Rules**.
3. Select the rule, e.g., *OPSWAT MDCES - Inbound emails*.
4. Click **Edit**.
5. Under **Except if...**, choose **The sender's IP address is in any of these ranges or exactly matches**.
6. Add the 3rd party IP addresses.
7. Save the rule and apply changes.
