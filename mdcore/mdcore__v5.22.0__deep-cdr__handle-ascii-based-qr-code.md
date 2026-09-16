<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/deep-cdr/handle-ascii-based-qr-code -->

# ASCII-based QR code

QR code can be created in a document by a combination of ASCII block characters (e.g., █ ). This tactic is designed to prevent security software from extracting malicious URLs from QR codes. Attackers can embed malicious links into the QR code and encourage users to scan the code, which would then take them to a fake page that appears to be a trusted service or application.

Deep CDR engine can detect and report the link from ASCII-based QR code to users (not sanitized).

Users can configure to process QR codes that are composed by ASCII characters.

The configuration can be modified under rule:

**Workflow Management> Workflows > Workflow Name > Deep CDR > Advanced configuration > File type handling**

Here is an screenshot of an QR code created by ASCII block characters:

**Supported file types**: MS Office, RTF.
