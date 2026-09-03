<!-- source: https://www.opswat.com/docs/mdces3/configuration/verdicts -->

# Verdicts

Summarize Page

**MetaDefender Cloud Email Security ™** assigns a verdict to every scanned email to summarize the outcome of its analysis. These verdicts help administrators and security teams quickly understand the risk level of content and determine the appropriate next steps.

Below is a detailed explanation of each available Actionable verdicts (configure through [Policies](/docs/mdces3/configuration/policies)) and Non-Actionable verdicts.

## [Actionable Verdicts](/docs/mdces3/configuration/verdicts#actionable-verdicts)

### [Malicious](/docs/mdces3/configuration/verdicts#malicious)

**Description:** The content has been positively identified as a confirmed threat.

**What this means:** One or more security engines detected malware, exploits, or other high-confidence malicious behavior. This verdict indicates a verified security risk.

**Recommended action:** Block by Policy. Immediate investigation is recommended.

### [Suspicious](/docs/mdces3/configuration/verdicts#suspicious)

**Description:** Potentially harmful content was detected, but the threat could not be fully confirmed.

**What this means:** Email/attachment(s) shows warning signs (such as unusual structure, risky behavior patterns, or low-confidence detections) but does not meet the threshold for a confirmed malicious verdict.

**Recommended action:** Block by Policy. Perform manual inspection.

### [Sanitized](/docs/mdces3/configuration/verdicts#sanitized)

**Description:** The content was successfully sanitized.

**What this means:** Potentially unsafe elements (such as macros, embedded scripts, or active content) were removed or neutralized, producing a safe version of the original email body and/or attachments (based on Policy).

### [Unsupported File Type](/docs/mdces3/configuration/verdicts#unsupported-file-type)

**Description:** The file format is not supported for sanitization.

**What this means:** While the file may still be scanned for malware, it cannot be sanitized because its format is not compatible with the sanitization engine.

**Typical action:** Some organizations block unsupported types, while others allow them with warning banner attached (see [Banners](/docs/mdces3/configuration/banners)).

### [Invalid File Structure](/docs/mdces3/configuration/verdicts#invalid-file-structure)

**Description:** The content failed to sanitize due to an unknown/invalid file structure.

**What this means:** While the file may still be scanned for malware, it cannot be sanitized because its format is not valid/recognized by the sanitization engine.

**Typical action:** Block by Policy. Review sanitization results or file integrity recommended.

### [Sanitization Policy Error](/docs/mdces3/configuration/verdicts#sanitization-policy-error)

**Description:** The content failed to sanitize due to an unknown reason.

**What this means:** A sanitization policy was applied, but the process could not be completed—often due to file corruption, unsupported features within the file, or policy constraints.

**Typical action:** Block by Policy. Review sanitization results or file integrity recommended.

### [Encrypted Content](/docs/mdces3/configuration/verdicts#encrypted-content)

**Description:** The email contained encrypted content or password-protected attachment(s).

**What this means:** Because the content is encrypted, **MetaDefender Cloud Email Security ™** cannot inspect its internal data. This is common with password-protected archives or encrypted documents.

**Recommended action:** Block by Policy. Request the affected user to provide valid passwords via the [User Actions wizard](/docs/mdces3/operating/user-actions).

### [Failure to Analyze](/docs/mdces3/configuration/verdicts#failure-to-analyze)

**Description:** The content could not be analyzed.

**What this means:** Scanning failed due to technical reasons such as file corruption, incomplete data, timeouts, or internal processing errors.

**Typical action:** Block by Policy. Perform manual inspection to help determine the root cause. Report to OPSWAT using [Chatbot (Ozzy)](/docs/mdces3/getting-started/ozzy).

## [Non-Actionable Verdicts](/docs/mdces3/configuration/verdicts#non-actionable-verdicts)

### [No Threat Detected](/docs/mdces3/configuration/verdicts#no-threat-detected)

**Description:** No known threats were identified in the email or its attachments.

**What this means:** The content successfully passed all enabled security checks. At the time of scanning, no malicious indicators were found.

### [Skipped](/docs/mdces3/configuration/verdicts#skipped)

**Description:** Scanning was skipped.

**What this means:** The content was intentionally bypassed by scanning engines, usually because of trusted sender configurations (See [Allowlist](/docs/mdces3/configuration/allowlist)).
