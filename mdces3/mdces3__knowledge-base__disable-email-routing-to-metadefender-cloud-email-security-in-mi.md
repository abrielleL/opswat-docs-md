<!-- source: https://www.opswat.com/docs/mdces3/knowledge-base/disable-email-routing-to-metadefender-cloud-email-security-in-mi -->

# Disable Email Routing to MetaDefender Cloud Email Security™ in Microsoft 365

Summarize Page

If you need to temporarily or permanently stop routing emails through **MetaDefender** **Cloud Email Security**™, you can easily do so by disabling specific mail flow rules in Microsoft 365. This article walks you through the necessary steps.

## [Step 1: Log in to the Microsoft 365 Admin Center](/docs/mdces3/knowledge-base/disable-email-routing-to-metadefender-cloud-email-security-in-mi#step-1-log-in-to-the-microsoft-365-admin-center)

1. Go to <https://admin.microsoft.com>.
2. Sign in using your **administrator credentials.**

## [Step 2: Open the Exchange Admin Center (EAC)](/docs/mdces3/knowledge-base/disable-email-routing-to-metadefender-cloud-email-security-in-mi#step-2-open-the-exchange-admin-center-eac)

1. In the left-hand navigation panel, click **“Show all”** if needed.
2. Select **Exchange** to open the **Exchange Admin Center** (EAC).

## [Step 3: Navigate to Mail Flow Rules](/docs/mdces3/knowledge-base/disable-email-routing-to-metadefender-cloud-email-security-in-mi#step-3-navigate-to-mail-flow-rules)

1. In the EAC, select **Mail flow** from the sidebar.
2. Click on **Rules**.

## [Step 4: Disable Mail Flow Rules](/docs/mdces3/knowledge-base/disable-email-routing-to-metadefender-cloud-email-security-in-mi#step-4-disable-mail-flow-rules)

1. Look for the following mail flow rules (not all may be present):

   - `OPSWAT MDCES - Inbound emails`
   - `OPSWAT MDCES - Outbound emails`
2. For each rule that exists:

   - Select the rule.
   - Click the **Disable** (or **Turn off**) button in the toolbar.

## [Step 5: Confirm Changes](/docs/mdces3/knowledge-base/disable-email-routing-to-metadefender-cloud-email-security-in-mi#step-5-confirm-changes)

- After disabling the relevant rules, test your mail flow to ensure emails are no longer routed through **MetaDefender** **Cloud Email Security**™.
- You can re-enable the rules at any time by returning to the same location and choosing **Enable**.

Info

- These rules were originally created to route email through **MetaDefender** **Cloud Email Security**™. Disabling them reverts email handling to the default Microsoft 365 behavior.
- No need to delete the rules—disabling is enough to stop the routing.

---
