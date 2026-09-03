<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-isn---t-an-attached-file-inside-a-pdf-being-converted-to-a-d -->

# Why isn’t an attached file inside a PDF being converted to a different format during Deep CDR sanitization?

When sanitizing a PDF that contains an attached file (for example, an XLS attachment), you may notice that the attached file is sanitized but not converted into a different file type (e.g., XLS → XLSX), even if your policy specifies a conversion.

This is expected behavior due to how recursive sanitization works in Deep CDR:

- Attached or embedded files are treated as components of the parent PDF, rather than standalone inputs.
- Deep CDR is designed to preserve the original file structure and format of embedded content when sanitizing.
- As a result, the attached file is sanitized but is not subject to type conversion rules (e.g., XLS → XLSX, DOC → DOCX, etc.).

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
