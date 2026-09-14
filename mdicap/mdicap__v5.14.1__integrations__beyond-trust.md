<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/beyond-trust -->

# Beyond Trust

Beyond Trust has not accept Sanitized/Redacted content then before setup, please make sure CDR engine and redact feature of DLP engine on Meta Defender Core are disabled

1. log in to admin interface of BeyondTrust and navigate to Management -> Security

Input MD ICAP Server to "ICAP Server URL" with format: **icap://host:port**

Info

By default **1344** is ICAP port without TLS

2. hit “Test with a file” button to check the connection with the MD ICAP Server

1. Enable TLS for ICAP connection (ICAPS) - optional

Info

1. Must enable ICAPS at MD ICAP Server
2. port 11344 is ICAPS default port

- Input ICAP Server URL with format: **icaps**://<host>:<port>
