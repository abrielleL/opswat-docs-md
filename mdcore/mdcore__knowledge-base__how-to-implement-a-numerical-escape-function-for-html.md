<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-implement-a-numerical-escape-function-for-html -->

# How to implement a numerical escape function for HTML?

This knowledge base article provides step-by-step instructions on how to fix an issue related to Outlook and its HTML rendering engine. It seems that certain escaped characters are not rendered correctly in Outlook when specified using their HMTL entity name, for example:

`&CloseCurlyQuote;`

Original Email: Please find the summary of today’s meeting

Processed email: Please find the summary of today`&CloseCurlyQuote;`s meeting

Note

The fix is available starting with CDR engine version 6.8.0

1. Navigate to the MD Core Web UI.
2. Locate and choose the workflow associated with the EGS instance.
3. Access the DeepCDR tab and proceed to the Advanced section.

4. Under File Type Handling, select "Others" and specifically choose "HTML."

5. Scroll down to find the option labeled "Use Numeric Entity" and activate it.

6. Confirm your changes by clicking on the "OK" button, followed by "Save Changes."

Support

If you encounter any problems with this guide or if the steps provided do not work, proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
