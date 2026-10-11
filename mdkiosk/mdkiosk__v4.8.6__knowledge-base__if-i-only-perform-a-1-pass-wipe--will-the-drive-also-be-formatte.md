<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/if-i-only-perform-a-1-pass-wipe--will-the-drive-also-be-formatte -->

# If I Only Perform a 1-Pass Wipe, Will the Drive Also Be Formatted?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to MetaDefender Kiosk of all versions.

This KB explains how performing a **1 pass wipe** on removable media in Kiosk affects the drive when the **Format** option is **not enabled**. It clarifies what parts of the media are erased, what remains intact, and what the user will see, helping administrators understand the impact of the wipe operation.

When a 1 pass wipe is performed without enabling Format, the drive is **not formatted**, but the data is securely erased:

- **Drive Appearance:** To the end user, the drive will appear empty, similar to a formatted drive.
- **Data Handling:** All existing files are overwritten with random data, making the original data nearly impossible to recover using standard recovery tools.
- **File System:** The file table and partition structure remain intact, meaning the drive’s file system and partitions are unchanged.
- **Operation Duration:** The time required depends on the size of the media and the number of passes, but only one pass is performed in this case.
- **Security Implication:** Even without formatting, the 1-pass wipe ensures that sensitive or malicious data is removed, leaving no recoverable traces on the media.

This separation of wiping and formatting allows administrators to control **how data is erased** and **what remains on the media**, providing flexibility in managing removable drives securely.

### [Key Takeaway](/docs/mdkiosk/v4.8.6/knowledge-base/if-i-only-perform-a-1-pass-wipe--will-the-drive-also-be-formatte#key-takeaway)

Selecting **1 pass wipe** does **not** imply formatting unless formatting is explicitly enabled elsewhere in the configuration.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
