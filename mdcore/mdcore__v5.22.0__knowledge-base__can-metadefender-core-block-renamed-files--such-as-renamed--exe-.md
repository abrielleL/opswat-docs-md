<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/can-metadefender-core-block-renamed-files--such-as-renamed--exe- -->

# Can MetaDefender Core block renamed files (such as renamed .exe files)?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Yes.

Thanks to MetaDefender Core’s built-in **File Type Verification Engine**, files that have manually or otherwise had their extensions altered (e.g. a *.exe* file disguised as a *.txt*) can be processed according to their actual format.

Pro Tip:

Often, altered file types can be an indicator of malicious intent, so it is highly recommended that users consider enabling this feature as part of their daily file security workflow.

To configure this feature, please go to your **MetaDefender Core Management Console>workflow Management>Workflows>{Your Relevant Workflow}>File Type** to enable detection as illustrated in the screenshot below.

***Core has a first option to detect and block on file type mismatch based on true file type detection.***

## [Detect file type mismatch:](/docs/mdcore/v5.22.0/knowledge-base/can-metadefender-core-block-renamed-files--such-as-renamed--exe-#detect-file-type-mismatch)

- When enabled, this detects discrepancies between the file extension and the actual file format.
- These files will be blocked and [Post Actions](/docs/mdcore/v5.22.0/knowledge-base/how-does-the-post-actions-feature-work) can be configured to further process these files as needed.
- Post actions are highly configurable, so specific remediation steps (in the form of policies/rules) can be customized per target/actual file type.

***If customer decides to process mismatched file then enabling the third option will allow CDR engine to sanitize files based on file extension when needed.***

## [Fallback file type detection to current extension if needed:](/docs/mdcore/v5.22.0/knowledge-base/can-metadefender-core-block-renamed-files--such-as-renamed--exe-#fallback-file-type-detection-to-current-extension-if-needed)

- When enabled, the File Type Verification Engine will work in conjunction with the Deep CDR module to detect and sanitize files according to their true file type.
- This means Deep CDR will only attempt to sanitize according to the given extension in the event that ‘true type’ sanitization fails.

***If the true file type could not be detected for whatever reasons (relevant engine/module encounters issues while processing etc.) then we have a second option to skip and block the processing for such files.***

## [Skip processing if actual file type could not be detected:](/docs/mdcore/v5.22.0/knowledge-base/can-metadefender-core-block-renamed-files--such-as-renamed--exe-#skip-processing-if-actual-file-type-could-not-be-detected)

- When enabled, this will produce a **Not Scanned** result in cases where the File Type Verification Engine is unable to detect the true file type.
- This should only occur when the engine is crashed/disabled/timed-out/canceled.

## [Customize mismatch detection settings:](/docs/mdcore/v5.22.0/knowledge-base/can-metadefender-core-block-renamed-files--such-as-renamed--exe-#customize-mismatch-detection-settings)

If a file is detected with a specific file type ID but can have a different extension, the user can configure it as shown above to allow possible extensions for that file type. The file type ID can be seen on the scan results page.

Support:

If you have followed the instructions above but are **Having Difficulty Configuring the Filetype Mismatch Feature**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
