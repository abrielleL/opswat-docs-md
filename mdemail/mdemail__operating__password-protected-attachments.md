<!-- source: https://www.opswat.com/docs/mdemail/operating/password-protected-attachments -->

# Password protected attachments

## [Problem](/docs/mdemail/operating/password-protected-attachments#problem)

Communicating parties apply encryption to maintain the confidentiality of their communiqués.

Given by the nature of encryption, real - potentially malicious - contents of an encrypted file are hidden from MetaDefender Email Gateway Security, thus encrypted files are blocked by default.

## [Solution](/docs/mdemail/operating/password-protected-attachments#solution)

### [Automated decryption and scanning](/docs/mdemail/operating/password-protected-attachments#automated-decryption-and-scanning)

Email Gateway Security can attempt to automatically decrypt password protected attachments and scan them.

Passwords are attempted to be taken from two sources:

1. The email body: the product can try to match regular expressions against the email body to try to extract attachment passwords. For details see [Attachment password patterns](/docs/mdemail/configuration/settings#attachment-password-patterns).
2. Password lists: in MetaDefender Core administrators can define lists of passwords for each Core side Workflow that will be attempted to decrypt password protected files. For details see [Password Storage](https://www.opswat.com/docs/mdcore/operating/inventory-management#password-storage).

Successful automated decryption

If the attachment can be decrypted automatically then it gets scanned. Based on the outcome of the scan, the email gets blocked or delivered.

No automated decryption

If the attachment can not be decrypted automatically, then the email gets retained in the quarantined and a dialog based password provision and rescan procedure is applied that is detailed below.

### [Marking emails that have password protected attachments](/docs/mdemail/operating/password-protected-attachments#marking-emails-that-have-password-protected-attachments)

If Email Gateway Security is set accordingly, then emails with password protected attachments⁠—that could not have been automatically decrypted and scanned⁠—will be put into the Quarantine and marked with a padlock icon (for details see [Operating/Quarantine](/docs/mdemail/operating/quarantine) ).

### [Initiate rescan and provide password](/docs/mdemail/operating/password-protected-attachments#initiate-rescan-and-provide-password)

When rescanning an email that has password protected attachments, password for the encrypted items is requested by Email Gateway Security. For details about rescanning see the *Rescan* section in [Operating/Quarantine](/docs/mdemail/operating/quarantine).

Rescan may be initiated by two parties:

1. Administrators with Quarantine access (for details see [Operating/Quarantine](/docs/mdemail/operating/quarantine))
2. Recipients of the email

#### [Administrators with quarantine access](/docs/mdemail/operating/password-protected-attachments#administrators-with-quarantine-access)

Administrators who are authorized to rescan on the Web Management Console, can initiate rescanning any blocked email on the **Quarantine** page. In this case the administrator need to enter the password for the encrypted attachments.

To initiate a rescan:

1. Select the email which needs to be rescanned and click the *Rescan* button.

2. Select the security rule (for details see [Configuration/Policy](/docs/mdemail/configuration/policy)) that will process the email and provide the password.

#### [Recipients of the email](/docs/mdemail/operating/password-protected-attachments#recipients-of-the-email)

Recipients of the blocked email may receive a notification (for details see [Configuration/Policy](/docs/mdemail/configuration/policy)) about the fact that the email was blocked, and a link where rescanning can be initiated.

To initiate a rescan:

1. Open the notification email and click the actions link.

2. Email Gateway Security’s rescan page opens; provide the password here to decrypt the document.

Rescan link availability

The link, where rescanning can be initiated, has a limited availability that can be configured under **Settings > General / Configuration / Public actions link availability**. For details see [Configuration/Settings](/docs/mdemail/configuration/settings).

Rescan link visibility

Please note that if **Settings > General**_/_*Configuration / Public server address* is not set then the rescan link won't be included in the notification email. For details see [Configuration/Settings](/docs/mdemail/configuration/settings).

### [Nested password protected attachments](/docs/mdemail/operating/password-protected-attachments#nested-password-protected-attachments)

From MetaDefender Email Gateway Security version 5.5.1 nested password protected attachments (e.g. password protected pdf in a password protected zip) are supported both in the rescan page and in the Quarantine rescan function.

Order of passwords

The order of the passwords provided is irrelevant, MetaDefender Email Gateway Security will apply the appropriate password to the appropriate nested attachment.

Quarantine:

Rescan page:

Number of passwords

The number of passwords allowed to be entered in the dialog is 10.

Failing rescan

The rescan will fail if

- any of the passwords are incorrect, or
- the password is missing for any of the nested attachments.
### [Supported file types](/docs/mdemail/operating/password-protected-attachments#supported-file-types)

The following file types are supported:

| **Category** | **File types (extension)** |
| --- | --- |
| Archive files | .zip, .7z, .rar |
| Portable Document Format files | .pdf |
| Microsoft Office files | .xls, .xlt, .xlsx, .xlsm, .xltx, .xltm, .xlsb, .ppt, .pptx, .doc, .dot, .docx, .docm, .dotx, .dotm |
| GnuPG *symmetric encryption* | .gpg |
