<!-- source: https://www.opswat.com/docs/md-ot-security/operating/ask-ai -->

# Ask AI

---

## [Introduction](/docs/md-ot-security/operating/ask-ai#introduction)

The **Ask AI** feature allows you to query asset information in the system using natural language. Instead of using complex filters, you can simply ask questions and the system will automatically search and return relevant results.

### [Benefits:](/docs/md-ot-security/operating/ask-ai#benefits)

- Quick queries using natural language
- No need to understand complex data structures
- Saves time searching for information
- Supports various types of asset-related questions

---

## [System Requirements](/docs/md-ot-security/operating/ask-ai#system-requirements)

- **Version:** OPSWAT MetaDefender OT Security 3.5.0 or higher
- **Access Rights:** Users must have access to:

  - Settings
  - Assets
  - "AI-Powered Enablement Settings" feature

---

## [Enabling the Feature](/docs/md-ot-security/operating/ask-ai#enabling-the-feature)

**Important Step:** Before using the Ask AI feature, you **MUST** enable the "Natural Language Asset Information Queries" option in Site Manager Settings.

### [Step-by-Step Instructions:](/docs/md-ot-security/operating/ask-ai#step-by-step-instructions)

#### [Step 1: Log In and Access Site Manager](/docs/md-ot-security/operating/ask-ai#step-1-log-in-and-access-site-manager)

1. Log in to the OPSWAT MetaDefender OT Security system
2. Select **Site Manager** from the components list (if you are currently in Sensor, switch to Site Manager)

#### [Step 2: Open Settings Page](/docs/md-ot-security/operating/ask-ai#step-2-open-settings-page)

1. In the left navigation bar, click on **Settings**
2. Wait for the Settings page to load

#### [Step 3: Select Application Tab](/docs/md-ot-security/operating/ask-ai#step-3-select-application-tab)

1. At the top of the Settings page, you will see several tabs:

   - Network & Discovery
   - Protocol
   - Alert
   - **Application** (Click on this tab)
   - Asset Type
   - My Account

#### [Step 4: Locate AI-Powered Enablement Settings](/docs/md-ot-security/operating/ask-ai#step-4-locate-ai-powered-enablement-settings)

1. Scroll down to the **"Operation"** section
2. Find the **"AI-Powered Enablement Settings"** section

#### [Step 5: Enable Natural Language Asset Information Queries](/docs/md-ot-security/operating/ask-ai#step-5-enable-natural-language-asset-information-queries)

1. Locate the toggle switch labeled **"Natural Language Asset Information Queries"**
2. Click on the toggle to switch it to **ON** (blue color)
3. If the toggle is already ON, no changes are needed

#### [Step 6: Save Settings](/docs/md-ot-security/operating/ask-ai#step-6-save-settings)

1. Click the **"Save"** button below the AI-Powered Enablement Settings section
2. Wait for the success confirmation message

> **Note:** After enabling the feature, you may need to wait a few seconds for the system to fully activate it. If the feature doesn't work immediately, refresh the page or log out and log back in.

---

## [Using Ask AI](/docs/md-ot-security/operating/ask-ai#using-ask-ai)

After enabling the feature in Settings, you can use Ask AI on the Assets page.

### [Step-by-Step Instructions:](/docs/md-ot-security/operating/ask-ai#step-by-step-instructions)

#### [Step 1: Access Assets Page](/docs/md-ot-security/operating/ask-ai#step-1-access-assets-page)

1. In the left navigation bar, click on **Assets**
2. Select the **Asset List** tab (if not already selected)

#### [Step 2: Locate Ask AI Search Bar](/docs/md-ot-security/operating/ask-ai#step-2-locate-ask-ai-search-bar)

1. At the top of the Asset List page, you will see a large search bar
2. To the right of the search bar, there is a blue button labeled **">> Ask AI"**

#### [Step 3: Enter Your Question](/docs/md-ot-security/operating/ask-ai#step-3-enter-your-question)

1. Click on the search bar
2. Type your question in English about the asset information you want to find
3. Example: "List all PLC devices" or "How many PLC devices are there?"

#### [Step 4: Submit Your Question](/docs/md-ot-security/operating/ask-ai#step-4-submit-your-question)

1. Click the **">> Ask AI"** button or press Enter
2. The system will process your question and display results

#### [Step 5: View Results](/docs/md-ot-security/operating/ask-ai#step-5-view-results)

1. Results will appear in a dropdown directly below the search bar
2. A list of matching assets will be displayed
3. You can click on any result to view details

## [Example Questions](/docs/md-ot-security/operating/ask-ai#example-questions)

Here are some example questions you can use with Ask AI:

### [Count Questions:](/docs/md-ot-security/operating/ask-ai#count-questions)

- "How many PLC devices are there?"
- "What is the total number of PLC devices?"
- "Count all PLC devices"
- "How many devices are offline?"
- "How many devices have been patched in the last 30 days?"
- "How many devices are running Windows?"

### [List Questions:](/docs/md-ot-security/operating/ask-ai#list-questions)

- "List all PLC devices"
- "Show me all devices with critical vulnerabilities"
- "What are the top 5 most vulnerable devices?"
- "List all devices manufactured by Siemens"
- "Show me devices with high risk scores"
- "What are the most common device types?"

### [Analysis Questions:](/docs/md-ot-security/operating/ask-ai#analysis-questions)

- "What is the average risk score across all devices?"
- "What are the most common device types?"
- "Show me devices with high risk scores"

### [Search by Attribute Questions:](/docs/md-ot-security/operating/ask-ai#search-by-attribute-questions)

- "List all devices manufactured by Siemens"
- "Show me all devices with critical vulnerabilities"
- "How many devices are running Windows?"

---

## [Usage Tips](/docs/md-ot-security/operating/ask-ai#usage-tips)

### [1. Use Natural Language](/docs/md-ot-security/operating/ask-ai#1-use-natural-language)

- You don't need to use special syntax
- Ask questions as if you're talking to a person
- Example: "How many PLCs do we have?" instead of "SELECT COUNT(*) FROM devices WHERE type='PLC'"

### [2. Be Specific](/docs/md-ot-security/operating/ask-ai#2-be-specific)

- The more specific your question, the more accurate the results
- Good example: "List all PLC devices manufactured by Siemens"
- Poor example: "Show me devices"

### [3. Combine Multiple Conditions](/docs/md-ot-security/operating/ask-ai#3-combine-multiple-conditions)

- You can combine multiple conditions in one question
- Example: "Show me all PLC devices with critical vulnerabilities"

### [4. Use Important Keywords](/docs/md-ot-security/operating/ask-ai#4-use-important-keywords)

- Use keywords such as: "PLC", "HMI", "vulnerabilities", "offline", "manufacturer", "risk score"
- This helps the system better understand your intent

### [5. View Detailed Results](/docs/md-ot-security/operating/ask-ai#5-view-detailed-results)

- After receiving the list of results, you can click on each asset to view detailed information
- Use additional filters on the Asset List page to refine results

---

## [Troubleshooting](/docs/md-ot-security/operating/ask-ai#troubleshooting)

### [Issue: "Ask AI" Button Not Visible](/docs/md-ot-security/operating/ask-ai#issue-ask-ai-button-not-visible)

**Possible Causes:**

- Feature not enabled in Settings
- Currently in Sensor instead of Site Manager
- System version doesn't support the feature

**Solutions:**

1. Verify that you have enabled "Natural Language Asset Information Queries" in Settings
2. Ensure you are in Site Manager (not Sensor)
3. Check system version (requires 3.5.0 or higher)
4. Refresh the page (F5) or log out and log back in

### [Issue: No Results Returned](/docs/md-ot-security/operating/ask-ai#issue-no-results-returned)

**Possible Causes:**

- Question is unclear or too complex
- No matching data in the system
- System is still processing

**Solutions:**

1. Try simplifying your question
2. Use more specific keywords
3. Check if there is data in the system
4. Wait a few seconds and try again

### [Issue: Results Not Accurate](/docs/md-ot-security/operating/ask-ai#issue-results-not-accurate)

**Solutions:**

1. Clarify your question
2. Use more specific keywords
3. Try breaking down your question into simpler questions

### [Issue: Cannot Enable Toggle in Settings](/docs/md-ot-security/operating/ask-ai#issue-cannot-enable-toggle-in-settings)

**Possible Causes:**

- Insufficient access rights
- Feature not available in current version

**Solutions:**

1. Contact your administrator to check access rights
2. Verify that "AI-Powered Enablement Settings" is in your permission list
3. Check system version

---

## [Summary](/docs/md-ot-security/operating/ask-ai#summary)

1. **First Step:** Go to Settings -> Application -> Enable "Natural Language Asset Information Queries"
2. **Then:** Go to Assets -> Use the search bar with the "Ask AI" button
3. **Enter Question:** Use natural language in English
4. **View Results:** Click on results to view details

---

## [Support](/docs/md-ot-security/operating/ask-ai#support)

If you encounter issues or have questions about the Ask AI feature, please:

- Contact your system administrator
- Refer to OPSWAT MetaDefender OT Security technical documentation
- Check system logs for error details (if applicable)
