<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/sandbox/internet-connection -->

# Internet Connection

The following features require a working internet connection

## [OSINT lookups](/docs/mdcore/v5.22.0/sandbox/internet-connection#osint-lookups)

Affected features:

- OSINT lookups (Basic)
- OSINT lookups (Full)

Accessed URL: `https://api.metadefender.com/v4/`

## [Executive summary](/docs/mdcore/v5.22.0/sandbox/internet-connection#executive-summary)

Affected features:

- Executive Summary

Accessed URL: `https://api.openai.com/v1/chat/completions/`

## [Digital signature verification](/docs/mdcore/v5.22.0/sandbox/internet-connection#digital-signature-verification)

Affected features:

- Digital signature whitelist

Sandbox needs to access the Certificate Revocation List (CRL) to verify digital certificates revocation status. Without this, whitelisting based on certificate is not working.

Common CRL distribution points:

- crl.microsoft.com
- crl.verisign.com
- crl.globalsign.com
- crl.digicert.com
- crl.entrust.net
- crl.sectigo.com
