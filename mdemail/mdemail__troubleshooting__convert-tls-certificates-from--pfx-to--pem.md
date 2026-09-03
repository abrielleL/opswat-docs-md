<!-- source: https://www.opswat.com/docs/mdemail/troubleshooting/convert-tls-certificates-from--pfx-to--pem -->

# Convert TLS certificates from .pfx to .pem

## [Problem](/docs/mdemail/troubleshooting/convert-tls-certificates-from--pfx-to--pem#problem)

MetaDefender Email Gateway Security expects TLS certificates (for the REST and SMTP interfaces, for the S/MIME and DKIM signatures) in .pem format.

Sometimes the certificate is available originally in .pfx format that needs to be converted to .pem. Unfortunately the conversion is possible in many different ways and not all conversion processes result in a certificate that works with Email Gateway Security.

In such cases the functionality that is intended to use the certificate may not work as expected.

## [Example](/docs/mdemail/troubleshooting/convert-tls-certificates-from--pfx-to--pem#example)

When the SMTP server of Email Gateway Security is configured with an improperly converted certificate, the SMTP server ends up in a continuous restart loop. In the meantime emails can not be received by the system as the SMTP server can not come up online.

## [Solution](/docs/mdemail/troubleshooting/convert-tls-certificates-from--pfx-to--pem#solution)

OPSWAT recommends converting .pfx certificates to .pem using the following command:

BashCopyopenssl pkcs12 -in cert.pfx -out cert.pem -nodes
