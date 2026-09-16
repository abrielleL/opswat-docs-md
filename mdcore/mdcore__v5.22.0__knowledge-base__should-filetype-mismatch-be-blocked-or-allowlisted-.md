<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted- -->

# Should Filetype Mismatch Be Blocked or Allowlisted?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

## [Overview](/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted-#overview)

Customers often raise this question when they experience a high volume of *Filetype Mismatch* detections that impact normal business workflows (for example, email attachments, files from legacy systems, or user-renamed files).

This article explains the security implications of allowlisting Filetype Mismatch and OPSWAT’s recommended approach.

## [Why does Filetype Mismatch occur so frequently?](/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted-#why-does-filetype-mismatch-occur-so-frequently)

Common legitimate causes include:

- Email gateways or applications renaming attachments
- Legacy systems exporting files with incorrect extensions
- Users manually renaming files
- Archives containing mixed file types

However, the same technique is also commonly used by malware to disguise malicious files.

## [Does allowlisting Filetype Mismatch affect detection or scanning accuracy?](/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted-#does-allowlisting-filetype-mismatch-affect-detection-or-scanning-accuracy)

No.

MetaDefender Core uses **content-based file type detection (magic bytes)**. Even when Filetype Mismatch is allowlisted:

- The real file type is still detected correctly
- The appropriate scanning engines are selected
- Archive extraction and recursive scanning still occur
- Parsers and analysis steps continue to run as expected

From a processing perspective, scanning remains technically correct.

## [What security risks does allowlisting introduce?](/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted-#what-security-risks-does-allowlisting-introduce)

The main risks occur at the **workflow and user-exposure level**:

- **File type spoofing** – executables disguised as documents (e.g., `invoice.pdf.exe`)
- **Policy bypass** – scripts or executables passing through document-only workflows
- **Downstream system trust issues** – systems relying on extensions may mishandle dangerous files
- **Higher chance of user execution** – users are more likely to open files that appear harmless

These techniques are widely used in phishing and malware campaigns.

## [What is OPSWAT’s recommendation?](/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted-#what-is-opswats-recommendation)

### [Default (best practice)](/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted-#default-best-practice)

**Block Filetype Mismatch.**

This provides the strongest protection against disguised malware and workflow bypass.

### [If allowlisting is required for business reasons](/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted-#if-allowlisting-is-required-for-business-reasons)

Apply the following compensating controls:

- Allowlist **only specific workflows or trusted sources** (not globally)
- Continue blocking when the detected type is **executable or script**
- Keep **deep and recursive scanning enabled**
- Maintain full engine coverage
- Improve file visibility for end users (for example, show file extensions in Windows via GPO)
- Educate users to be cautious with unexpected attachments

## [Summary](/docs/mdcore/v5.22.0/knowledge-base/should-filetype-mismatch-be-blocked-or-allowlisted-#summary)

Blocking Filetype Mismatch provides the strongest protection. Allowlisting does not break scanning, but it increases the risk of disguised malware and policy bypass and should be used only in tightly controlled scenarios.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
