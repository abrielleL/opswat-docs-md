<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-to-increase-the-maximum-file-size-for-scanning-in-metadefend -->

# How to increase the maximum file size for scanning in MetaDefender Kiosk via OPSWAT Central Management v7?

This article applies to all MetaDefender Kiosk releases managed by OPSWAT Central Management v7

## [**Overview**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-increase-the-maximum-file-size-for-scanning-in-metadefend#overview)

By default, MetaDefender Kiosk workflows enforce maximum file size limits for scanning. Files larger than the configured limit may be rejected, resulting in failed scans. This article explains how to increase the maximum allowable file size for scanning within MetaDefender Kiosk workflows using OPSWAT Central Management v7.

## [**Steps**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-increase-the-maximum-file-size-for-scanning-in-metadefend#steps)

---

#### [**Increase the maximum file size on the Kiosk workflow in the MetaDefender Core used by Kiosk**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-increase-the-maximum-file-size-for-scanning-in-metadefend#increase-the-maximum-file-size-on-the-kiosk-workflow-in-the-metadefender-core-used-by-kiosk)

1. Log in to OPSWAT Central Management v7.
2. Navigate to **Inventory** → **MetaDefender Core**.
3. Locate the integrated Core instance used by Kiosk and click the **Settings (gear)** icon.
4. Go to **Workflow Rules** → **Kiosk**.
5. Under the **General** tab, find the **FILE SCAN** setting.
6. Increase the maximum file size limit to suit your environment’s needs.
7. Save your changes and deploy policy updates.

---

#### [**Increase the maximum file size on Guest or Employee workflows on MetaDefender Kiosk (if applicable)**](/docs/mdkiosk/v4.8.5/knowledge-base/how-to-increase-the-maximum-file-size-for-scanning-in-metadefend#increase-the-maximum-file-size-on-guest-or-employee-workflows-on-metadefender-kiosk-if-applicable)

1. Within Central Management, go to **Inventory** → **MetaDefender Kiosk**.
2. Click the **Settings (gear)** icon for the relevant Kiosk instance.
3. Navigate to **Workflows** settings.
4. Edit the **Guest** or **Employee** workflow by clicking the **pen** icon.
5. Under the **Processing** tab, locate the **File limits** section.
6. If the **Max file size** option is enabled, adjust the value accordingly.
7. Save changes and deploy policy updates.

Support:

If **Further Assistance** is required, please proceed to log a [****support case or chatting with our support engineer****](https://my.opswat.com/support).
