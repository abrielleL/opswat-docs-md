<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-files-are-not-sanitized -->

# Why files are not sanitized?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

There are a few details too look at when the files you scan are not being sanitized:

1. Make sure that the Deep CDR engine is enabled.

2. Make sure that the extension of the file you are scanning is enabled in the DEEP CDR module.

To do so, please access the MetaDefender Core WEB UI (by default <http://localhost:8008>) and access Workflow Management -> Workflows -> Select your workflow -> DEEP CDR tab

Here navigate to “Enable for filetypes”

Click on Edit and enable all extensions that you want to sanitize:

Once selected, click OK and then Save changes.

Support

If you have followed the instructions above but **Files are still not sanitized** please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
