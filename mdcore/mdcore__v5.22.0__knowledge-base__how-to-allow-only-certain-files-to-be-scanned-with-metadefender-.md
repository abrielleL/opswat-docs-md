<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-only-certain-files-to-be-scanned-with-metadefender- -->

# How To Allow Only Certain Files to be Scanned with MetaDefender Core?

The steps provided in this article apply to MetaDefender Core versions 4.x and 5.x. The user interface and options may vary slightly depending on your version.

MetaDefender Core offers extensive customization options, empowering administrators to filter files based on their extensions. This feature allows you to define rules that permit scanning only specific file types, enhancing security and efficiency. This article explains how to configure file extension filtering in MetaDefender Core using the Web UI and provides a sample regular expression to allow only certain file extensions, effectively restricting the scanning process.

## [Prerequisites:](/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-only-certain-files-to-be-scanned-with-metadefender-#prerequisites)

- Access to the MetaDefender Core Web UI
- Appropriate user permissions to modify workflows

## [Steps:](/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-only-certain-files-to-be-scanned-with-metadefender-#steps)

1. Launch a web browser and navigate to the MetaDefender Core Web UI.
2. Log in using your administrator credentials.
3. Go to the "Workflow Management" section.
4. Click on "Workflows" in the left-hand menu.
5. Select the workflow to which you want to apply file extension filtering.
6. In the workflow details, navigate to the "Blocklist" tab.
7. Enable the "Blocklist by filename" option.
8. Click the "Add" button to create a new filename rule.
9. In the "Filename" field, enter the following sample regular expression: Sample regular expression: `^(?!.*\.(?:extension1|extension2|extension3)$).*$`

Replace `extension1`, `extension2`, `extension3`, etc., with the desired file extensions. For example, to allow only ".txt" and ".pdf" files, use `^(?!.*\.(?:txt|pdf)$).*$`.

Note: Make sure the regular expression accurately represents the desired file extensions. If you need assistance with regular expressions, consult the appropriate documentation or reach out to your organization's IT team.

10. To apply filtering based on file size, enable the "If bigger than" option.
11. Specify the minimum file size in the corresponding field.
12. Click "Save" or "Apply" to save your changes.

## [Additional Resources:](/docs/mdcore/v5.22.0/knowledge-base/how-to-allow-only-certain-files-to-be-scanned-with-metadefender-#additional-resources)

- For more information on using the MetaDefender Core Blocklist/Allowlist feature, refer to the following documentation: [How to use MetaDefender Core V5 Blocklist/Allowlist feature?](/docs/mdcore/v5.22.0/knowledge-base/how-to-use-metadefender-core-v5-blocklist-allowlist-feature)
- To learn about other workflow configuration options in MetaDefender Core, including the Blocklist and Allowlist, consult the Workflow Configuration Template documentation: [Workflow Configuration Template](/docs/mdcore/v5.22.0/configuration/workflow-configuration-template)

Support

If you have followed the instructions above but are still **Unable to Allow Only Certain Files to be Scanned with MetaDefender Core**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
