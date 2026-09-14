<!-- source: https://www.opswat.com/docs/ocm/7.39.0/integrations/delivering-module-updates-to-metadefender-core-instances -->

# Delivering module updates to MetaDefender Core instances

The following guideline describes how to deliver module updates to MetaDefender Core instances.

1. In the MetaDefender Core management page, select the connected instances that need to be updated.

2. Select **Update Engine** from the **ACTIONS** drop-down menu.
3. In the **Update Engine** dialog, select the update method:

- **Direct update from Central Management updater:** Update the MetaDefender Core instances with the module updates already downloaded to OPSWAT Central Management's module pool. Please refer to [MetaDefender Core Module](/docs/ocm/7.39.0/integrations/metadefender-core-module) for more details on the module pool. This option only works with MetaDefender Core instances version 4.16.0 and beyond.

- **Mediate update from MetaDefender Core server:** Manually upload the module updates that will be delivered to MetaDefender Core instances.

4. This step differs depending on the method chosen.

   1. **Direct Update:** Enter the PIN and confirm the update process by selecting **UPDATE.**

2. **Mediate Update:**

1. Drag-and-drop or click on **Browse** to select an update file (an archive file format such as .zip) and an update information file (.yml format). Then click **Next**. Note that the maximum file can be uploaded is 1536 MB and a timeout is 6 minutes.

2. Enter the PIN and click Update to confirm the update.

5. OPSWAT Central Management console will display a notification when the delivery process is complete.

Known issues

MetaDefender Core instances cannot download engine packages from OPSWAT Central Management if the latter only has TLSv1.3 enabled.

MetaDefender Core below version 5.4.1 does not support the TLSv1.3 protocol. As a workaround, [please enable additional TLS protocols for OPSWAT Central Management.](/docs/ocm/7.39.0/configuration/enabling-https#via-the-management-console)
