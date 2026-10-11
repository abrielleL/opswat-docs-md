<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-are-password-protected-archives-blocked-and-how-do-i-unblock -->

# Why are password protected archives blocked and how do I unblock them?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Pro Tip:

MetaDefender Core supports a wide range of encrypted (password-protected) archive file formats, including:

- *7z, Zip, RAR, PDF*, MS Word (*DOC, DOCX, DOCM, DOTX* and *DOTM) / Excel (XLS, XLSX, XLSM, XLSB, XLTM*) and Powerpoint (*PPT, PPTX, PPTM, PPSM, POTX* and *POTM*).

All of the formats above can be decrypted by MetaDefender Core’s archive module for scanning, on provision of the associated passwords.

We advise customers to rescan the password protected file via both Core UI and REST API

Seeing a **Blocked** encrypted/password-protected archive could mean that you have failed to enter the associated password or that the file format you are attempting to scan is not supported by MetaDefender Core.

In addition, failing to enable archive handling in your settings may also lead to **Blocked** results.

To enable archive handling:

1. Go to **MetaDefender Core Management Console>Workflow Management>Workflow**s, and click **Edit** to adjust the relevant workflow rules, as illustrated below.

2. Once in your chosen workflow, go to the **Archive** tab.
3. Here, you should ensure that the following actions are enabled:

   1. Archive extraction
   2. Scan of original unextracted archive
   3. Extraction of office documents

You can also ensure that tasks are handled as **Failed** when they are/in the case of:

- Extracted partially
- Unsupported compression method.

4. Finally, click **Save changes** to apply your settings.

## [Option 1: Manually add passwords when uploading a file through the UI](/docs/mdcore/v5.22.1/knowledge-base/why-are-password-protected-archives-blocked-and-how-do-i-unblock#option-1-manually-add-passwords-when-uploading-a-file-through-the-ui)

To unlock supported password-protected archives for scanning (once you have configured your chosen workflow), please do the following:

1. Go to your **MetaDefender Core Management Console>Dashboard**, and drop a password encrypted file into the field for processing.
2. You will now be asked whether the file is password protected, as highlighted in the screenshot below, click to confirm.

3. Enter the file’s password in the field provided, then click **OK**.

4. Your file is now ready for processing and, provided the encrypted file type is supported and your archive settings are configured, the file should no longer return a **Blocked** result. (if no other restriction settings are in place on the workflow)

## [**Option 2: Use Password Storage in the Library.**](/docs/mdcore/v5.22.1/knowledge-base/why-are-password-protected-archives-blocked-and-how-do-i-unblock#option-2-use-password-storage-in-the-library)

Instead of entering the archive password during each file upload, add commonly used passwords to the Library password storage and enable the workflow to use stored passwords when processing password-protected archives. This allows you to automate the process, as an archive file can contain embedded child files that require their own unique password as well.

1. Open MetaDefender Core and go to **Library**.
2. Select the **Password Storage** section and Create a new storage.
3. Add the password or passwords that should be available for archive extraction. Save the changes.
4. Go to **Workflows > Workflow Configuration > Select a workflow rule > Archive tab > Scroll down and check Password storage**
5. Select the password storages you would like to use for this workflow.
6. Test the workflow with a known password-protected archive to confirm the file is extracted and scanned as expected.

Users would use this option when the same archive passwords are reused across submissions, when files are submitted through automated workflows or APIs where manually entering a password is not practical, or when administrators want to centrally manage password[s] used for scanning instead of requiring users to provide them during upload.

For details, see [Library Management - MetaDefender Core](https://www.opswat.com/docs/mdcore/operating/library-management#password-storage).

Support:

If you have followed the instructions above but are still **Unable To Unblock Password Protected Archives**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
