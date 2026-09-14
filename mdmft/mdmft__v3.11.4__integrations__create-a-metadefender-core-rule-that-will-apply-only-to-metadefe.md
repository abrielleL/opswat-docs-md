<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/integrations/create-a-metadefender-core-rule-that-will-apply-only-to-metadefe -->

# Creating a MetaDefender Core rule for MetaDefender Managed File Transfer

Summarize Page    Connect to Cursor Connect to VS Code

To fine-tune the integration between MetaDefender Managed File Transfer™ and MetaDefender Core™, create a security rule in MetaDefender Core™ that applies to all files uploaded to MetaDefender Managed File Transfer™.

## [Creating a rule only for MetaDefender Managed File Transfer](/docs/mdmft/v3.11.4/integrations/create-a-metadefender-core-rule-that-will-apply-only-to-metadefe#creating-a-rule-only-for-metadefender-managed-file-transfer)

1. In the "MetaDefender Core™ Management Console," go to "Policy" → "Security Rules" → "Workflow rules" → "Add new rule."
2. Name the rule and choose your desired workflow.
3. In the "Limit to specified user agents" field, enter "mft" and click "Add."
4. Complete the other settings and click "Save."
5. Reorder the rules so the new rule is at the top (each rule is processed in order).

You can now upload files in MetaDefender Managed File Transfer™ and verify that they are processed using your new rule.
