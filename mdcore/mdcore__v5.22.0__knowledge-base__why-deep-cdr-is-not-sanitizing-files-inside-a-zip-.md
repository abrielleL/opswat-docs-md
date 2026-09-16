<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-deep-cdr-is-not-sanitizing-files-inside-a-zip- -->

# Why Deep CDR is not Sanitizing Files Inside a ZIP?

The .gif files are expected to be sanitized and converted to .jpeg format using Deep CDR rules. While this process worked for individual .gif files, when the files were inside a ZIP archive, the ZIP file returned with the original .gif files instead of the converted .jpeg files.

The issue was due to a missing configuration setting in the MetaDefender Core. Specifically, the "Enable archive sanitization" option was not activated, and the appropriate archive file types were not selected under "Enable for archive compression filetypes."

## [Solution:](/docs/mdcore/v5.22.0/knowledge-base/why-deep-cdr-is-not-sanitizing-files-inside-a-zip-#solution)

To resolve this issue, follow these steps:

1. Navigate to the MetaDefender Core UI.
2. Go to the Workflows section and select the relevant workflow.
3. Access the Compression tab.
4. Ensure that "Enable archive sanitization" is turned on.
5. Under "Enable for archive compression filetypes," select all relevant archive file types.

Once these settings are correctly configured, Deep CDR should properly sanitize files inside ZIP archives as expected.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
