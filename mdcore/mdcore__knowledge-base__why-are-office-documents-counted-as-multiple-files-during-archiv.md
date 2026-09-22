<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-are-office-documents-counted-as-multiple-files-during-archiv -->

# Why Are Office Documents Counted as Multiple Files During Archive Extraction?

**Check Your Version:** This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

## [**Issue:**](/docs/mdcore/knowledge-base/why-are-office-documents-counted-as-multiple-files-during-archiv#issue)

Some customers observe that Microsoft Office documents (such as DOCX or XLSX) may be treated as multiple files by security inspection engines, even when the document does not contain any visible attachments or embedded files. This behavior can lead to unexpected blocking or processing limits being reached.

## [**Explanation:**](/docs/mdcore/knowledge-base/why-are-office-documents-counted-as-multiple-files-during-archiv#explanation)

Modern Microsoft Office files use the Office Open XML format. These file types are ZIP‑based containers, not single flat files. Internally, an Office document consists of multiple components, including:

- XML files that define document content and structure
- Metadata and relationship files
- Style definitions, headers, and document properties
- Optional embedded objects (even if not apparent to the user)

During archive or content extraction, the security engine processes these internal components individually rather than treating the document as one opaque file. As a result, each internal element is counted separately.

### [**Why Office Documents Cannot Be Treated as a Single File:**](/docs/mdcore/knowledge-base/why-are-office-documents-counted-as-multiple-files-during-archiv#why-office-documents-cannot-be-treated-as-a-single-file)

From a security perspective, Office Open XML documents cannot be handled as a single “black‑box” file. Analyzing only the outer container would prevent inspection of internal components and could allow threats such as:

- Embedded malicious payloads
- Malicious macros
- Exploit‑based XML content
- ZIP bombs disguised as Office documents

To effectively detect and prevent these threats, the security engine must unpack and analyze each internal component of the document.

### [**Is it possible to count the whole Office document as a single file?**](/docs/mdcore/knowledge-base/why-are-office-documents-counted-as-multiple-files-during-archiv#is-it-possible-to-count-the-whole-office-document-as-a-single-file)

No. Office Open XML documents are intentionally decomposed during inspection so that their internal structure can be fully analyzed. Treating them as a single file would reduce visibility and weaken security protection.

**Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
