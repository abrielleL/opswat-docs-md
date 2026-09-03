<!-- source: https://www.opswat.com/docs/mdfs/kb/why-attachments-disappear-when----delete-original-file----is-ena -->

# Why Attachments Disappear When “Delete Original File” Is Enabled in File Sanitization

When the **“Delete Original File”** option is enabled in **Content Disarm and Reconstruction (CDR)**, attachments may appear to disappear. This behavior is expected and stems from how **Chatter** handles file references.

### [What’s Actually Happening](/docs/mdfs/kb/why-attachments-disappear-when----delete-original-file----is-ena#whats-actually-happening)

When a file is uploaded to Chatter, Chatter stores a reference to the **original file version**. If CDR is configured to delete the original file after scanning, that original file record is removed. However, Chatter does **not automatically update its reference** to point to the newly created **sanitized version** of the file.

As a result, once the original file is deleted, Chatter continues to reference a file that no longer exists - causing the attachment to disappear or trigger an “**entity is deleted**” error.

### [Intended vs. Actual Behavior](/docs/mdfs/kb/why-attachments-disappear-when----delete-original-file----is-ena#intended-vs-actual-behavior)

The intended use case is:

1. Upload a file to Chatter.
2. Wait for the file to be scanned and sanitized.
3. Send an email with the sanitized version attached.

In practice, this flow breaks because Chatter remains linked to the original file instance and does not switch to the sanitized file automatically.

### [Platform Limitation, Not a Bug](/docs/mdfs/kb/why-attachments-disappear-when----delete-original-file----is-ena#platform-limitation-not-a-bug)

This behavior is best described as a **Chatter platform limitation**, not a product defect. When “Delete Original File” is enabled:

- The **original file** has its own `ContentSize`, `ContentDocumentId`, and `ContentBodyId`.
- The **sanitized file** is created as a **new, separate file** with different IDs and a different size.

Because the sanitized file is treated as a new file, existing references to the original file are not preserved.

### [Recommended Workaround](/docs/mdfs/kb/why-attachments-disappear-when----delete-original-file----is-ena#recommended-workaround)

To ensure the sanitized file is sent successfully:

1. Upload the file to Chatter.
2. Wait for the scan to complete.
3. Allow the original file to be deleted.
4. Locate the newly created sanitized file.
5. Manually attach the sanitized file in Chatter or to the email.

This approach ensures that the attachment references the correct, sanitized file version.
