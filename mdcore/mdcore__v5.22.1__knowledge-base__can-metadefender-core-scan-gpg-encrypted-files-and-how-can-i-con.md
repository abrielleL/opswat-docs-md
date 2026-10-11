<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-gpg-encrypted-files-and-how-can-i-con -->

# Can MetaDefender Core scan GPG encrypted files and how can I configure it to do so?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check your version:**

This article applies to MetaDefender Core and is applicable to all MetaDefender Core V5 releases deployed on Windows and Linux systems.

## [**Overview**](/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-gpg-encrypted-files-and-how-can-i-con#overview)

When scanning files encrypted with GPG such as .txt.gpg files, MetaDefender Core may return the status “**Document is encrypted with a password”**. This can occur even when a password is provided, depending on how the file type is detected and processed.

This behavior is not necessarily a limitation, but it may require a workflow configuration adjustment so the system correctly identifies and handles GPG encrypted files.

## [**Solution**](/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-gpg-encrypted-files-and-how-can-i-con#solution)

You can configure MetaDefender Core to properly recognize GPG encrypted files by overriding the file type in the workflow settings.

Follow these steps:

1. Open the MetaDefender Core web UI
2. Navigate to Workflow Management and then Workflows
3. Select the workflow you are using for scanning
4. Go to the File Type tab
5. Scroll down to the section labeled **Overwrite a file type by another file type**
6. Click Add
7. In the Filetype field, select Encrypted GPG
8. In the Sub filetype field, select GPG
9. Save the workflow

File Type tab showing the option to overwrite Encrypted GPG file type with GPG sub file type

After applying this configuration, MetaDefender Core will properly detect GPG encrypted files.

**Support:**

If you have questions, concerns or issues regarding **MetaDefender** **Core**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
