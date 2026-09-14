<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/what-does-the-items-sanitized-removed-count-in-deep-cdr-sanitiza -->

# What does the items sanitized/removed count in Deep CDR sanitization report mean?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

After sanitizing a document using Deep CDR, in the processing result afterwards, the number of sanitized/removed items are counted and listed.

Take the following example: Deep CDR sanitization result for a DOCX document containing in-line images, hyperlinks, and embedded PDF, XLSX files.

The objects are counted as a group when they have the same result or meaning. In the above example, when four images are sanitized successfully, or when 3 hyperlinks are removed, they are grouped together.

For the embedded objects, if Deep CDR’s Recursive Level config is turned on (and bigger than 0) and these objects are sanitized, then each file usually has a different result (i.e., a DOCX file, an XLSX file, or a different sanitization detail). Therefore, the embedded objects are separated to show the specific detail of each recursive sanitization.

Support:

For further assistance regarding MetaDefender Core Deep CDR, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
