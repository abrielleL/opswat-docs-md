<!-- source: https://www.opswat.com/docs/mdcore/sandbox/integrating-deep-cdr-analysis-mode-version -->

# How do I obtain my OPSWAT MetaDefender Cloud Reputation API Key?

OPSWAT MetaDefender Cloud offers reputation analysis of files, URLs, and IP addresses. To access these services, you'll need an API secret, which is a unique key that authorizes your requests.

Here is a detailed guide on how to obtain the **MetaDefender Cloud Reputation API Key**:

**In your MetaDefender Cloud dashboard:**

1. Look for the **Licenses** section in the navigation menu.
2. This section will allow you to generate MetaDefender Cloud API key, including your **Reputation API Key**.

Find more information at the [Licenses and Usage Limits documentation of MetaDefender Cloud.](https://www.opswat.com/docs/mdcloud/account-management/licenses-and-usage-limits)

To enable MetaDefender Core to utilize MetaDefender Cloud for reputation checks, you need to configure it to use the API secret you obtained from the MetaDefender Cloud service.

**Step 1: Access MetaDefender Core Configuration**

1. Log in to MetaDefender Core
2. Ensure you have Admin Access

### [**Step 2: Locate the API Configuration Section**](/docs/mdcore/sandbox/integrating-deep-cdr-analysis-mode-version#step-2-locate-the-api-configuration-section)

In the MetaDefender Core dashboard:

1. **Go to the Inventory page**
2. **Navigate to the Modules Section and then find Adaptive Sandbox**:

   - Look for an option called **Configuration**.
   - This section is where you can add your MetaDefender Cloud API Key

### [**Step 3: Enter MetaDefender Cloud Reputation API** **Key**](/docs/mdcore/sandbox/integrating-deep-cdr-analysis-mode-version#step-3-enter-metadefender-cloud-reputation-api-key)

1. Input Your API Secret into **OPSWAT Reputation secret** field as shown below
