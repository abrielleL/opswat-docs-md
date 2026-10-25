<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/why-is-the-metadefender-icap-activation-failing-even-if-activati -->

# Why is the MetaDefender ICAP activation failing even if Activation URL is whitelisted?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to MetaDefender ICAP Server versions 5.0 through 5.9 deployed on Windows.

#### [**Issue:**](/docs/mdicap/v5.15.0/knowledge-base/why-is-the-metadefender-icap-activation-failing-even-if-activati#issue)

Activation attempts fail despite allowlisting the activation server. Logs indicate CRL lookup failures preventing SSL/TLS verification:

[WARNING] 2025.06.13 13:12:08.182: (common.licensemgr) Call http request failed, url='[https://activation.dl.opswat.com/activation?…'](https://activation.dl.opswat.com/activation?%E2%80%A6'), error_code='35', error_ detail='schannel: next InitializeSecurityContext failed: CRYPT_E_REVOCATION_OFFLINE (0x80092013) - The revocation function was unable to check revocation because the revocation server was offline.' [msgid: 4885]

#### [**Resolution:**](/docs/mdicap/v5.15.0/knowledge-base/why-is-the-metadefender-icap-activation-failing-even-if-activati#resolution)

There are two options to resolve this issue:

- Option 1: Allowlist CRL and OCSP URLs
- Option 2: Upgrade MetaDefender ICAP to Version 5.10

#### [**Steps:**](/docs/mdicap/v5.15.0/knowledge-base/why-is-the-metadefender-icap-activation-failing-even-if-activati#steps)

**Option 1: Allowlist CRL and OCSP URLs**

Ensure the following Certificate Revocation List (CRL) and Online Certificate Status Protocol (OCSP) URLs are whitelisted in your network firewall or proxy settings:

- `http://crl.r2m02.amazontrust.com/r2m02.crl`
- `http://crl.rootca1.amazontrust.com/rootca1.crl`
- `http://ocsp.rootca1.amazontrust.com`
- `http://crt.rootca1.amazontrust.com/rootca1.cer`

**Option 2: Upgrade MetaDefender ICAP to Version 5.10**

1. Download the MetaDefender ICAP 5.10 installer from the OPSWAT Customer Portal.
2. Run the 5.10 installer and follow the wizard prompts.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
