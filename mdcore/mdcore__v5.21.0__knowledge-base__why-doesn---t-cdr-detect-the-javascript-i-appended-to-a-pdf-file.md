<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-doesn---t-cdr-detect-the-javascript-i-appended-to-a-pdf-file -->

# Why doesn’t CDR detect the JavaScript I appended to a PDF file?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

## [Cause](/docs/mdcore/v5.21.0/knowledge-base/why-doesn---t-cdr-detect-the-javascript-i-appended-to-a-pdf-file#cause)

If the JavaScript-containing objects are added to the PDF but the Xref (Cross-Reference) table is not updated accordingly, CDR will not detect them.

- The Xref table is crucial for referencing valid objects in a PDF.
- Objects missing from the Xref table are considered garbage data and will be removed by the CDR engine.

## [Solution](/docs/mdcore/v5.21.0/knowledge-base/why-doesn---t-cdr-detect-the-javascript-i-appended-to-a-pdf-file#solution)

To ensure that JavaScript in a PDF is detected by CDR:

1. Update the Xref Table:

- When adding JavaScript, ensure that the corresponding object is correctly referenced in the Xref table.

2. Follow PDF File Structure Specifications:

- The JavaScript should be stored in a properly structured and up-to-date object within the PDF.

## [Conclusion](/docs/mdcore/v5.21.0/knowledge-base/why-doesn---t-cdr-detect-the-javascript-i-appended-to-a-pdf-file#conclusion)

For JavaScript to be recognized in a PDF by CDR, it must be placed in a valid object that is correctly indexed in the Xref table and complies with the PDF file structure specifications.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
