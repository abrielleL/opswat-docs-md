<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-do-you-sometimes-see-a-discrepancy-between-the-file-type-and -->

# Why do you sometimes see a discrepancy between the File Type and MIME Type information?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

In certain cases, it is observed that the "File Type" and "File Type ID/MIME Type" information associated with a file do not match, as shown in the example below:

This indicates that the file type engine has identified the input file as a vCalendar file, but with some degree of uncertainty. It is possible that the input file does not strictly conform to the file specification, which may cause the file type and MIME type information to be inconsistent.

When a file follows the file specification correctly, the categories, file types, and MIME type will have the appropriate and consistent information, as demonstrated in the example below:

It is important to note that the correct identification of file types and MIME types is critical in various applications, such as content filtering, file sharing, and data management. Therefore, it is recommended to ensure that files adhere strictly to the file specification and standards to avoid discrepancies in the file type and MIME type information.

Support:

If Further Assistance is required, please follow the instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-), then proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
