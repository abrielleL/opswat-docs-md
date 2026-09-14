<!-- source: https://www.opswat.com/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration -->

# Changing MetaDefender Core Configuration

The following guideline describes how to change the configuration of a MetaDefender Core instance remotely.

1. Go to the **MetaDefender Core** management page under **Inventory** in the sidebar.

2. Click the **Setting** button (from the gear icon) of the MetaDefender Core instance you wish to configure.

3. OPSWAT Central Management will load the setting of the MetaDefender Core.

4. Change any settings and click the **Submit** button.

## [Security zones](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#security-zones)

The following guideline describes how to modify the Security Zone setting for MetaDefender Core.

- The **SECURITY ZONES** tab:

## [Add a new security zone](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#add-a-new-security-zone)

1. Click the **ADD NEW ZONE** button in the right top panel.

2. Fill the proper inputs and then click the **SAVE** button.

- **Zone Name:** The new zone's name.

- **Description:** The new zone's description

- **Networks:** The networks assigned to this security zone

3. The Security Zone management page will be reloaded automatically if the result is successful.

4. Click button **SAVE POLICY CHANGES**.

5. Show the message for saving the policy successfully.

## [Modify the existing security zones](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#modify-the-existing-security-zones)

1. Click each Security Zone record or the edit icon to modify zone and click **SAVE CHANGES** to save.

2. If you wish to delete a specific Security Zone, click the delete icon in the corresponding Security Zone record and click the **DELETE** button.

3. The Security Zone management page will be reloaded automatically if the result is successful.

## [Workflow templates](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#workflow-templates)

The following guideline describes how to modify the Workflow Templates setting for MetaDefender Core.

- The **WORKFLOW TEMPLATES** tab

## [Add a new workflow](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#add-a-new-workflow)

1. Click **ADD NEW WORKFLOW** button in the right top panel.

2. Fill the proper inputs and then click the **SAVE** button.

- **Workflow Name:** The new workflow's name

- **Description:** The new workflow's description.

3. The Workflow Templates management page will be reloaded automatically if the result is successful.

4. Click button **SAVE POLICY CHANGES**.

5. A confirmation message is displayed.

## [Modify the existing workflow templates](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#modify-the-existing-workflow-templates)

1. Click each Workflow Templates record or the edit icon to modify the workflow and then click **SAVE CHANGES** to save.

2. If you wish to delete a specific workflow, click the delete icon in the corresponding Workflow Templates record and then click the **DELETE** button.

3. If you wish to clone a specific workflow, click the clone icon in the corresponding Workflow Templates record, give a new name to the new workflow and then click the **SAVE** button.

4. The Workflow Templates management page will be reloaded automatically if the result is successful.

## [Workflow rules](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#workflow-rules)

The following guideline describes how to modify the Workflow Rules setting for MetaDefender Core.

- The **WORKFLOW RULES** tab

## [Add a new rule](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#add-a-new-rule)

1. Click **ADD NEW RULE** button in the top right panel.

2. Fill the proper inputs and then click **SAVE** button.

- **Name:** The new rule's name

- **Description:** The new rule's description

- **Apply To Zone:** The zone that the new rule should apply to

- **Use Workflow Template:** Make the new rule follow a preset template

- **Use Certificate To Generate Batch Signature:** Choose if the new rule should be digitally signed

- **Certificate Used For Batch Signing:** If the above option is selected, pick the certificate that should be used.

3. The Core page will be reloaded automatically if the result is successful.

4. Click the **SAVE POLICY CHANGES** button.

5. A confirmation message is displayed.

## [Modify the existing rules](/docs/ocm/7.39.0/integrations/changing-metadefender-core-configuration#modify-the-existing-rules)

1. Click each Workflow Rules record or the edit icon to modify zone and click **SAVE CHANGES** to save.

2. If you wish to delete a specific rule, click the delete icon in the corresponding Workflow Rules record and then click the **DELETE** button.

3. The MetaDefender Core page will be reloaded automatically if the result is successful.
