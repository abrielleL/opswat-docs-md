<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-to-add-an-embedded-image-in-to-the-notification-email -->

# How to add embedded images to notification email templates?

Summarize Page    Connect to Cursor Connect to VS Code

To add embedded images (as part of the email message instead of being referenced from an external source) as data URIs to MetaDefender Managed File Transfer email templates:

Data URI

A data URI for an image is a way to embed the image data directly into a web page or document by encoding it as a text string, allowing it to be displayed without the need for a separate file.

For further details, see <https://en.wikipedia.org/wiki/Data_URI_scheme>.

1. Obtain the data URI for your image using online converters or by encoding the image in Base64. Prefix it with the appropriate MIME type, e.g., "data/png;base64," followed by the encoded data.
2. Go to your MetaDefender Managed File Transfer email template page and select "Tools" → "Source code."

3. Find or create the <img> tag where you want to embed the image, and paste the data URI into the src attribute of the <img> tag.

4. Save the dialog and the email template.
