<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/using-the--copy---go--feature -->

# How do I use the Copy & Go feature in MetaDefender Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows or Linux systems.

Copy & Go is a time-saving feature designed to streamline the Kiosk experience by allowing users to copy their files to the Kiosk before scanning.

This means users can remove their portable media much sooner than the traditional scan, which requires that the media remain connected to the Kiosk. Following the scan, all copied files will be deleted from the Kiosk system.

Pro Tip:

There are benefits and drawbacks to enabling the Copy & Go feature, and it is only appropriate and effective for certain use cases.

Therefore, please review this article in-full before enabling the Kiosk Copy & Go feature.

## [When to use Copy & Go](/docs/mdkiosk/v4.8.6/knowledge-base/using-the--copy---go--feature#when-to-use-copy--go)

Copy & Go is ideal for users who need a faster experience at the Kiosk, such as when users need to scan hundreds or thousands of files, and copying files would be significantly faster than standing and waiting at the Kiosk for the scan to finish.

On the other hand, Copy & Go is *not* recommended for users scanning a small number of files, as the overall time saved by copying would be negligible.

## [How to enable Copy & Go](/docs/mdkiosk/v4.8.6/knowledge-base/using-the--copy---go--feature#how-to-enable-copy--go)

- Go to your **Kiosk Management Console>Workflows**, then click the *edit* icon on the appropriate workflow, as highlighted in the screenshot below:

- Go to the Processing section, as illustrated below, ensuring that both the **Use Core Server** and the **Copy & Go** options are selected.

- Finally click **Apply** to save your settings.

Please Note:

Enabling the Copy & Go feature will automatically disable any previously enabled **Workflow File Handling** option that copies or moves files to the original media.

## [The standard Copy & Go flow](/docs/mdkiosk/v4.8.6/knowledge-base/using-the--copy---go--feature#the-standard-copy--go-flow)

The standard process flow for Copy & Go runs as follows:

1. The user logs into the Kiosk and follows the prompts to insert their media.
2. The user then selects their files for scanning
3. The files are automatically copied to the Kiosk
4. A pop-up prompts the user to remove their media, which still contains the original files
5. The copied files are scanned by Kiosk
6. A scan report is produced
7. Depending on settings, processed files may be copied to the associated MetaDefender Managed File Transfer or to another specified location at this point
8. The copied and scanned files are then deleted from the MetaDefender Kiosk.

The Copy & Go enabled Kiosk process is similar to the standard Kiosk process, except for steps 3. and 4. above, that allow the user to remove their media early and then go on their way.

The Workflow will then continue to scan the files and produce a report. With Copy&Go, some actions that need human response, like email address input, password for encrypted media,... are moved prior to scanning so that user can prepare in advance; some actions that Kiosk can select a default option, like Print or Skip, Copy or Skip,... are waiting for user inputs within 3 seconds or default actions (Print, Copy...) will be proceeded.

## [Warnings](/docs/mdkiosk/v4.8.6/knowledge-base/using-the--copy---go--feature#warnings)

- **Hard drive space**

  - The Copy & Go feature will copy all of the selected files to the Kiosk system.
  - Therefore, the amount of free hard drive space should be closely monitored when using Copy & Go, to ensure the Kiosk system does not run out of space.
- **Malicious files**

  - Copy & Go may open up the Kiosk system to infection in the event that malicious files exist on the media, which then get copied to the Kiosk system.
- **Disabled Workflow features**

  - Any Workflow option that copies files back to the original media will be automatically disabled when Copy & Go is enabled.
  - This includes File Remediation options that remediate the files on the original media or copy remediated versions of the files back to the original media after scanning.
- **Media should still be considered UNSAFE when Copy & Go is enabled**

  - Copy & Go copies files from the original media to the Kiosk system and then ejects the original media unchanged.
  - The removable media should therefore still be treated as unsafe and unscanned.

Support:

If you have any difficulty **Using MetaDefender Kiosk’s Copy & Go Feature**, please follow these instructions on [How To Create a Support Package](https://docs.opswat.com/mdkiosk/troubleshooting#creating-the-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
