<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-manage-disk-space-usage-in-pg-data-base-directory-in-meta -->

# How to manage Disk Space Usage in pg_data\base directory in MetaDefender Core for Windows?

#### [Issue](/docs/mdcore/v5.21.0/knowledge-base/how-to-manage-disk-space-usage-in-pg-data-base-directory-in-meta#issue)

The directory located at OPSWAT\MetaDefender Core\data\pg_data\base continues to grow in size until the disk becomes full, eventually causing scans to fail or stop running altogether.

#### [Cause](/docs/mdcore/v5.21.0/knowledge-base/how-to-manage-disk-space-usage-in-pg-data-base-directory-in-meta#cause)

This folder stores critical components such as:

- Scanning history
- Executive report
- Other related data used by MetaDefender Core

Without proper data retention policies in place, this data accumulates indefinitely, consuming excessive disk space.

#### [Solution](/docs/mdcore/v5.21.0/knowledge-base/how-to-manage-disk-space-usage-in-pg-data-base-directory-in-meta#solution)

To manage and reduce the size of this directory, configure **automatic deletion** through the **Data Retention** settings in MetaDefender Core. **Steps to Configure Automatic Deletion:**

1. Navigate to the **Settings** page in the MetaDefender Core UI.
2. Go to the **Data Retention** section.
3. Set a retention period—**we recommend 1 to 4 weeks**, depending on your organizational needs and storage capacity.
4. For Deep CDR and DLP, these are recommended to remain set to the 4 h default.

#### [Optional: Immediately Free Up Space](/docs/mdcore/v5.21.0/knowledge-base/how-to-manage-disk-space-usage-in-pg-data-base-directory-in-meta#optional-immediately-free-up-space)

To quickly recover disk space after updating the settings:

- Use the **Delete** button at the bottom of the **Data Retention** settings page to remove existing data that falls outside the new retention period.
- Use the database vacuum tool (instructions can be found here [Database Maintenance | MetaDefender Core 4.19.0 or above](/docs/mdcore/v5.21.0/operating/database-maintenance---metadefender-core-4-19-0-or-above))

Note:

Please consider that even after data retention changes, it will take some time for the storage to be cleaned (usually up to 24 h, due to the internal database vacuum process).

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
