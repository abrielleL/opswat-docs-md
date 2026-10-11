<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-automate-backup-configuration-settings-for-md-core---api- -->

# How to automate backup configuration settings for MD Core? (API)

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows.

This article provides a simple Bash script template that allows users to automate the export of MetaDefender Core configuration using the `/admin/export/v2` API endpoint. For reference: [GET - Export configuration](/docs/mdcore/v5.22.1/metadefender-core#adminexportv2)

### [Prerequisites](/docs/mdcore/v5.22.1/knowledge-base/how-to-automate-backup-configuration-settings-for-md-core---api-#prerequisites)

- A valid **MetaDefender Core API key** (`session_id`), which the user has received from the post request for Login [POST - Login](/docs/mdcore/v5.22.1/metadefender-core#userlogin)

#### [**Export settings:**](/docs/mdcore/v5.22.1/knowledge-base/how-to-automate-backup-configuration-settings-for-md-core---api-#export-settings)

Response example

**Bash script template:**

#### [Import settings](/docs/mdcore/v5.22.1/knowledge-base/how-to-automate-backup-configuration-settings-for-md-core---api-#import-settings)

- The prerequisites for this also required the login `session_id` to make the API call. For reference: [POST - Import configuration](/docs/mdcore/v5.22.1/metadefender-core#adminimportv2)

Import request

Include the file

**Bash scripts template:**

Support:

If you have followed all of the steps above but cannot set the desired RAM Drive security permissions, please follow these instructions on [How to Create Support Package With Bundle Tools?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-#) before [creating a support case or chatting with our support engineer.](https://my.opswat.com/portal/support)
