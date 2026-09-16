<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/proactive-dlp/redact-sensitive-information -->

# Redact/Substitution/Hash sensitive information

It is imperative to safeguard sensitive data as soon as it has been detected in order to prevent unauthorized access to it. In order to address this concern, OPSWAT Proactive Data Loss Prevention (PDLP) system comes with two distinct features: **redaction**, **substitution** and **Hash**:

- **Redaction**: As a result of redaction, sensitive information such as Credit Card Numbers (CCNs) and Social Security Numbers (SSNs) is concealed, while maintaining the overall structure and layout of the document as a whole. It is important to note that this method ensures that the private information is hidden while maintaining the readability of the remaining content.
- **Substitution:** On the other hand, the substitution feature is able to replace sensitive data with placeholders, thus adding another level of security for confidential information. OPSWAT PDLP system preserves privacy and prevents unauthorized access to sensitive data by incorporating both redaction and substitution features.
- **Hash:** This feature introduces a secure hashing mechanism for PII substitution, enabling compliant and safe data sharing. The hashing process ensures that any substituted personal information remains non-reversible and unintelligible if intercepted, providing an additional layer of security and protection against data exposure.

  - Standardized substitution format: PII is replaced with `<pii-id prefix>_<hash-value>`
  - Supported hashing algorithms: SHA-256 SHA-384 SHA-512

## [Supported File Types](/docs/mdcore/v5.22.0/proactive-dlp/redact-sensitive-information#supported-file-types)

- Portable Document Format (PDF)
- Microsoft Office Word (DOC/DOCX)
- Microsoft Office Word XML (XML)
- Microsoft Office Excel (XLS/XLSX)
- Microsoft Office Excel XML (XML)
- Microsoft Office PowerPoint (PPT/PPTX)
- Microsoft Rich Text Format (RTF)
- Extensible Markup Language (XML)
- Comma Separated Values (CSV)
- Text files (TXT, HTML)
- JPG *(Optical Character Recognition based)*
- PNG *(Optical Character Recognition based)*
- TIFF *(Optical Character Recognition based)*
- BMP *(Optical Character Recognition based)*

## [Supported Sensitive Information](/docs/mdcore/v5.22.0/proactive-dlp/redact-sensitive-information#supported-sensitive-information)

- All categories under Detect Financial Information
- All categories under Detect personal identity information
- All categories under Detect network and device information
- All categories under Detect corporation information
- All categories under Detect drug and health information
- All categories under Detect sensitive information with AI (BETA)
- All categories under Detect secret
- Custom regular expression

## [Enabling redaction](/docs/mdcore/v5.22.0/proactive-dlp/redact-sensitive-information#enabling-redaction)

- Workflow Management > Workflows > "Workflow name" > Proactive DLP

Enable "Allow if redacted" will mark the final result to be "Allowed" even the files have sensitive info

Sample redacted file

Following sample does not represent an actual person.

## [Enabling substitution](/docs/mdcore/v5.22.0/proactive-dlp/redact-sensitive-information#enabling-substitution)

- Workflow Management > Workflows > "Workflow name" > Proactive DLP

By enabling the substitution feature, you can effectively replace sensitive data with alternate characters or placeholders based on your need.

Following sample does not represent an actual person.

## [Enabling Hash](/docs/mdcore/v5.22.0/proactive-dlp/redact-sensitive-information#enabling-hash)

- Workflow Management > Workflows > "Workflow name" > Proactive DLP

By enabling the Hash Redaction feature, the system replaces detected sensitive information with its hashed equivalent, preserving data structure while protecting confidentiality.

Info

Following sample does not represent an actual person.
