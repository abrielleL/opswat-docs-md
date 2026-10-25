<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/advanced-usages/ocm-https-certificates-rootca -->

# OCM Uses a Complete Certificate Chain with a Private Root CA

View as Markdown Ask ChatGPT about this page Ask Claude about this page

When OPSWAT Central Management (OCM) is fronted by a TLS server certificate issued from a **private** root CA (an internal PKI or a self-generated root), MetaDefender Drive can only enroll over HTTPS if **two** conditions are met:

1. The OCM server presents a **complete certificate chain** — server → intermediate → root — during the TLS handshake, not just the leaf certificate.
2. Each MetaDefender Drive device **trusts the root CA** through its system trust store.

A web browser may complete a partial chain from its own certificate store and report success, but MetaDefender Drive cannot — it validates strictly against the chain the server presents and the roots it has been told to trust. This is why a Drive can fail to enroll while a browser pointed at the same OCM appears to work.

This guide walks through generating a root CA, an intermediate CA, and a server certificate with the correct extensions (including a Subject Alternative Name, which MetaDefender Drive requires), bundling them into a single chain file, configuring OCM to present that chain, and installing the root CA on each Drive device.

## [Requirements](/docs/mddrive/v4.4.10/advanced-usages/ocm-https-certificates-rootca#requirements)

- **MetaDefender Drive v4.4.5 or later** and **OPSWAT Central Management v10 or later**. Reliable HTTPS enrollment between MetaDefender Drive and Central Management v10 using a private root CA requires Drive v4.4.5+; earlier versions can fail the TLS handshake even with a correctly configured chain.
- OpenSSL on the machine used to generate the certificates.
- The FQDN (and any additional host names or IPs) by which Drive devices reach the OCM server.

## [Pick a platform](/docs/mddrive/v4.4.10/advanced-usages/ocm-https-certificates-rootca#pick-a-platform)

The procedure is identical on both platforms; only the shell syntax (line continuations, here-strings, encoding flags) differs.

- [OCM Uses a Complete Certificate Chain with a Private Root CA (Windows)](/docs/mddrive/v4.4.10/advanced-usages/ocm-https-certificates-rootca-windows)— uses Windows PowerShell.
- [OCM Uses a Complete Certificate Chain with a Private Root CA (Linux)](/docs/mddrive/v4.4.10/advanced-usages/ocm-https-certificates-rootca-linux)— uses the bash shell.

## [What the procedure produces](/docs/mddrive/v4.4.10/advanced-usages/ocm-https-certificates-rootca#what-the-procedure-produces)

Following either guide, you will end up with three files:

- `root.crt` — the private root CA, to be installed on every MetaDefender Drive device.
- `server.key` — the private key, installed on the OCM server.
- `server.chain.crt` — the full certificate chain (server, intermediate, root) presented by OCM during the TLS handshake.

The Drive devices trust `root.crt`; OCM presents `server.chain.crt`; the TLS handshake completes; Drive enrollment over HTTPS succeeds.
