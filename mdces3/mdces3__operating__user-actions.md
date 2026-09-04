<!-- source: https://www.opswat.com/docs/mdces3/operating/user-actions -->

# User Actions wizard

Summarize Page

This guide explains how to interact with **MetaDefender Cloud Email Security ™** when handling emails with special actions required — such as encrypted attachments, blocked content, or release requests.

When you receive an email flagged by **MetaDefender Cloud Email Security ™**, you will be prompted to take one or more actions before accessing the message or its attachments.

Info

End users can access the Ozzy chatbot while the User Actions Wizard is visible on screen. See [Chatbot (Ozzy)](/docs/mdces3/getting-started/ozzy) for more information.

The **User Actions** process involves:

# [Security Verification](/docs/mdces3/operating/user-actions#security-verification)

When accessing a flagged email, you will see a **Security Verification Required** screen.

The end user must:

- Enter his/hers email address.
- Click **Verify** to proceed.

This ensures only the intended recipient can take further action.

Info

The user can click **"What’s this?"** to view more information about why the email was flagged (e.g. encrypted content, blocked content, or policy violations).

## [Authentication](/docs/mdces3/operating/user-actions#authentication)

For security, **MetaDefender Cloud Email Security ™** will send a **One-Time Password (OTP)** to the email address previously specified.

The end user must:

- Enter the OTP code on the verification page.
- Click **Verify Code** to continue.

Info

Providing the incorrect OTP code three times will require a new code to be sent.

# [Email Details](/docs/mdces3/operating/user-actions#email-details)

The **Email Details** section displays summary information about the quarantined email.

It includes:

- **Status:** Current processing status of the email (for example, **Quarantined**).
- **Actions Required:** Displays any action required before processing can continue, such as **Provide Passwords**.
- **From:** Sender's email address.
- **To:** Recipient's email address.
- **Subject:** Email subject.
- **Date Sent:** Date and time the email was sent.
- **Attachments:** Number of attachments, including the number of encrypted attachments.
- **Verdict:** Final processing verdict or reason the email was held.

## [Why We Held It](/docs/mdces3/operating/user-actions#why-we-held-it)

The **Why We Held It** section explains why the email has been quarantined.

Common reasons include:

- Password-protected attachments that cannot be scanned.
- Attachments containing malware or other known threats.
- Files requiring additional verification before delivery.

This information helps recipients understand why the email has not yet been delivered.

## [Content](/docs/mdces3/operating/user-actions#content)

The **Content** section displays all files contained in the email together with their current scan status.

Files are grouped by processing result.

## [Files We Couldn't Open](/docs/mdces3/operating/user-actions#files-we-couldnt-open)

Lists password-protected attachments that could not be scanned.

For each attachment, you can:

- Review the attachment name.
- Enter the attachment password using the **Enter Password** field.

Once the correct password is provided, the attachment becomes eligible for rescanning.

## [Files That Came Back Clean](/docs/mdces3/operating/user-actions#files-that-came-back-clean)

Displays files that were successfully scanned and determined to be safe.

Each file displays its processing result, for example:

- **Sanitized**

---

# [Rescanning the Email](/docs/mdces3/operating/user-actions#rescanning-the-email)

After entering the required password(s), select **Rescan Email** to submit the password and initiate a new scan.

During rescanning:

- The encrypted attachment is decrypted using the supplied password.
- MetaDefender Cloud Email Security scans the attachment using configured detection and prevention technologies.
- If sanitization is enabled, eligible files are processed using Content Disarm and Reconstruction (CDR).
- The email verdict is updated based on the scan results.

If all attachments are determined to be safe and organizational policy permits, the email is released to the recipient.

If malware is detected or the attachment cannot be safely processed, the email remains quarantined or is handled according to the configured security policy.

# [Password Requirements](/docs/mdces3/operating/user-actions#password-requirements)

- Enter the password exactly as it was used to encrypt the attachment.
- If multiple password-protected attachments are present, provide the password for each encrypted file.
- If an incorrect password is entered, the attachment cannot be scanned and the email remains quarantined until a valid password is provided.

# [Notes](/docs/mdces3/operating/user-actions#notes)

- Passwords are used only for scanning the protected attachment and are not stored after processing.
- Rescanning does not bypass organizational security policies.
- Only users authorized to access the quarantined email can submit passwords and request a rescan.
