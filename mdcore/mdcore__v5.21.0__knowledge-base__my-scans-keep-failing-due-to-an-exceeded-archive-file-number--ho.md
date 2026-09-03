<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/my-scans-keep-failing-due-to-an-exceeded-archive-file-number--ho -->

# My scans keep failing due to an exceeded archive file number, how do I determine the number of files in an archive and then configure my process settings accordingly?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

MetaDefender Core’s built-in Archive Extraction Engine supports a wide range of archive, archive-like, and encrypted file formats, many of which can contain hundreds or even thousands of child-files that will need to be extracted for processing.

Pro Tip:

Our supported file types include the following.

|  |  |
| --- | --- |
| **Pure archive formats** | *Zip, 7z, JAR, RAR, RAR5, TAR, ISO, CAB, ARJ, LHA, LZH, RPM, DEB, LZMA, WIM, DMG, XAR, MSM, SFX, XZ, VDI, VHD, CPIO, HFS, APK, GZ, MSI, TAZ, TGZ, TBZ, BZ2, VIB, AR, ALZ, TSE, TSEC, TSEZ, ACE, PST, OST, OFT, IPA, JMOD, MSIX, APPX, EGG, DLL,* and *PGP* (with password only) |
| **Self-extracting archive formats** | which are created by both *7zip, WinRAR, PKZIP* and *IExpress* |
| **Microsoft Office Documents** | (e.g. *DOCX* files) which are detected as archive files by default |
| **Email/Calendar files** | (e.g. *EML, MSG* and *ICS*) which are extracted to scan header, body, attachments |
| **Encrypted files** | *7z, Zip, RAR, PDF*, MS Word (*DOC, DOCX, DOCM, DOTX* and *DOTM) / Excel (XLS, XLSX, XLSM, XLSB, XLTM*) / Powerpoint (*PPT, PPTX, PPTM, PPSM, POTX* and *POTM*) which can be decrypted by the archive module with a given password. |

To avoid seeing your scans fail due to **Exceeded Archive File Number** and other archive related issues, users attempting to scan large volume archives, large image files and other archive-like formats should adjust their settings accordingly.

Unfortunately, there’s no quick-fix in terms of estimating the number of child-files or folders within a given archive, so it is recommended that you test and adjust your settings against a file that is a fair, general representation of the larger files you’re expecting to scan.

To access these settings, follow the instructions below:

1. Go to your **MetaDefender Core Management Console>Workflow Management>Workflows**, to select your chosen workflow, as illustrated in the screenshot below.

2. Inside your chosen workflow, click on the **Archive** tab, as shown below, where you can configure a range of archive-related rules.

3. Now, adjust the following values to a level that lets your test-file scan to completion. Then allow some room for error:

   1. **Max nesting level**
   2. **Max number of files extracted**
   3. **Max expansion factor**
   4. **Archive analysis timeout**

      1. Large or complex archives may require a longer timeout (for example, 60~120 minutes) to complete analysis.

So, if your test archive is allowed through at 4500, set the levels to 5000, etc.

4. Finally, click **Save** to apply your settings before processing your files as needed.

By adjusting this set of rules on any workflow in which you’re expecting a throughput of large volume archive, image and archive-like files, you can minimize or even eliminate the number of scans that fail due to archive-related factors, including exceeded archive file numbers.

Support:

If you have followed the instructions above but are still **Experiencing Failed Scans Due To Exceeded Archive Numbers**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
