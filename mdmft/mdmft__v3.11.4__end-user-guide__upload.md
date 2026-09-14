<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/end-user-guide/upload -->

# Uploading Files

Summarize Page    Connect to Cursor Connect to VS Code

To upload files or folders:

1. Click the "Upload Files" button.

2. In the upload window, add files by clicking "+Add files" or drag and drop them.

3. Review the upload list and remove any items by clicking the "×**"** icon next to them.

4. If you want to share files during upload, click "Go to advanced settings" to open the "Advanced settings" window.

   1. Choose users, guests or groups to share the files with, or you can choose to [share](/docs/mdmft/v3.11.4/end-user-guide/share) them later.
   2. Set an expiration date for the files. Administrators may disable this feature.

5. Click "Upload" to start the process.

Info

**Folder structure**

Uploaded folders will retain their original structure.

Warning

**Empty folders**

Empty folders or subfolders will not be created in MetaDefender MFT.

**File size limit**

If you encounter issues uploading large files, check with your administrator about the size limit.

**Upload size and time limits**

If large uploads fail, try dividing them into smaller parts and uploading separately.

---

### [Password-Protected Files](/docs/mdmft/v3.11.4/end-user-guide/upload#password-protected-files)

To upload password-protected files, provide the password(s) to allow MetaDefender® MFT to scan them.

To provide one or more passwords, select the "File is protected by password" option in the upload window and enter the password. To add additional passwords, click the "+" sign next to the text box.

Provide all necessary passwords

If an uploaded file is password-protected or contains additional password-protected files inside, you must provide all required passwords to unlock them.

Blocking password-protected files

If you upload password-protected files without providing the necessary passwords, the files will be blocked.

How to unlock blocked files

To unlock blocked password-protected files, click the "key" icon next to the file name, enter the password in the "Add Password" window, and click "Save." You can add multiple passwords by clicking the "+" sign if needed. The files will be scanned and made available if no threats are detected.

### [Drag and Drop Upload](/docs/mdmft/v3.11.4/end-user-guide/upload#drag-and-drop-upload)

To upload files or folders using drag-and-drop, simply select the items from your file explorer and drag them over to the My Files/Shared With Me dropzone area. Once dropped, MetaDefender Managed File Transfer™ will automatically begin the upload process. You can monitor the progress through the upload modal located in the bottom-right corner of the interface.

Info

Drag-and-drop uploads in Shared With Me are limited:

- You can’t upload files to the Shared With Me root.
- You can drag and drop files only into shared folders where you have the Editor permission.
Info

If you forget to apply certain settings, such as adding an upload reason, setting a password for encrypted files, or sharing the file with someone, you can still configure these options after the upload is complete.

Dragging items over an empty My Files

Dragging items into root of My Files
