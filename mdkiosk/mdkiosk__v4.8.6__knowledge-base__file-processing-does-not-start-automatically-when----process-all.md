<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/file-processing-does-not-start-automatically-when----process-all -->

# File processing does not start automatically when “Process all files” is enabled — why?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk versions.

When **Process all files** is enabled, the customer may expect file processing to start automatically after inserting a removable storage device into MetaDefender Kiosk. However, this is not how Kiosk is designed.

Kiosk does not start file processing automatically when a device is inserted, regardless of the workflow configuration.

The manual start action acts as a safety gate. Kiosk workflows can include destructive actions, such as deleting non-compliant files, wiping the storage device, or quarantining content. If processing started immediately after device insertion, these actions could run before the user is ready or aware, which may cause unintended data loss.

Administrators can reduce user steps by setting **Process all files** as the default scan mode and diabling all user questions. In this case, users do not need to select a scan option; they only need to confirm and start processing.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
