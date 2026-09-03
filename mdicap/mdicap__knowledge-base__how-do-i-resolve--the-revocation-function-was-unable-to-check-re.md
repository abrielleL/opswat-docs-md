<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/how-do-i-resolve--the-revocation-function-was-unable-to-check-re -->

# How do I resolve “the revocation function was unable to check revocation for the certificate” when adding MD Core server profile to MD ICAP Server using HTTPS?

Since MD ICAP Server is using native secure channel of Windows for TLS (Schannel) to communicate with MD Core, the behavior of revocation is managed by Windows OS: t**he certificate revocation server needs to be accessible for the account running ICAP**.

Thus, if the revocation server is not available, you might encounter: “The revocation function was unable to check revocation because the revocation server was offline.”

## [Solution](/docs/mdicap/knowledge-base/how-do-i-resolve--the-revocation-function-was-unable-to-check-re#solution)

Please verify certificate revocation list availability and validity, and test certificate revocation.

Example: after you export your leaf certificate into leafCertificate.cer

Run the following commands:

BashCopycertutil -urlfetch -verify leafCertificate.cer
certutil -user -urlfetch -verify leafCertificate.cer
certutil -url leafCertificate.cer

To check certificate revocation under SYSTEM and Network Service context, run the same commands as below. Requires: [PSTools](https://learn.microsoft.com/en-us/sysinternals/downloads/pstools)

BashCopypsexec -s certutil -urlfetch -verify c:/temp/leafCertificate.cer
psexec -u "nt authority\networkservice" certutil -urlfetch -verify c:/temp/leafCertificate.cer
psexec -i -d -u "nt authority\networkservice" certutil -url c:\temp\leafCertificate.cer

Alternatively, you can add the following in MD ICAP Server’s configuration, to disable SSL certificate check on ICAP’s side: create and set “verifypeer” to “false” in “internal” section of configuration. Then restart the service.

Note: this setting causes potential security risk, so it is not recommended.

**Windows**: HKEY_LOCAL_ MACHINE\SOFTWARE\OPSWAT\ICAP Server

**Linux**: mdicapsrv.conf

Support:

For further assistance regarding **Unable to Check Revocation for the Certificate**, please follow these instructions on [How To Create a Support Package](/docs/mdicap/troubleshooting/how-to-create-support-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
