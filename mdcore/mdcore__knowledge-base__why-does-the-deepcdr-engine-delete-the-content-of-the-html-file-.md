<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-the-deepcdr-engine-delete-the-content-of-the-html-file- -->

# Why does the DeepCDR engine delete the content of the HTML file?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

When scanning HTML files, the Deep CDR engine reconstructs the content to remove potentially malicious or hidden elements that could pose a security risk. One common reason for content being removed is the presence of specific CSS attributes or styles used to hide information from the visible page is the font-size:0px.

CSS style

The content removed

As seen from the image all the content in the <div> got removed.

Since Deep CDR recognizes these CSS attributes as methods used to conceal content, the information inside `<div>` elements that use specifically (font-size:0px) is removed during the sanitization process.

For a current workaround, we will need to disable the “Process Zero Font Text” to make sure that the Deep CDR does not recognize those elements as zero font text.

Support:

If you have followed all of the steps above but are still unable to resolve the issue. Please follow these instructions on [How to Create Support Package With Bundle Tools?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-#), before [creating a support case or chatting with our support engineer.](https://my.opswat.com/portal/support)
