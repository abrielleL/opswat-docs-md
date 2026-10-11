<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/configuration/trusting-files-by-digital-signature -->

# Trusting Files by Digital Signature

View as Markdown Ask ChatGPT about this page Ask Claude about this page
# [Trusting Files by Digital Signature](/docs/mdkiosk/v4.8.6/configuration/trusting-files-by-digital-signature#trusting-files-by-digital-signature)

MetaDefender Kiosk can skip scanning for files that are digitally signed by a certificate you've marked as trusted, so known-good signed software (such as internal installers or drivers) can be processed faster. Any file that isn't signed by a trusted certificate — including unsigned files and files with an invalid, expired, or revoked signature — is still scanned normally. This option is available starting in Kiosk 4.7.7 and is turned off by default.

## [Prerequisites](/docs/mdkiosk/v4.8.6/configuration/trusting-files-by-digital-signature#prerequisites)

- At least one certificate must already be added to Kiosk (see your certificate management page) before you can select it as a trust source for this feature.

## [Enabling Trust by Digital Signature](/docs/mdkiosk/v4.8.6/configuration/trusting-files-by-digital-signature#enabling-trust-by-digital-signature)

1. Navigate to **Configuration → Advanced**.
2. In the **Scanning** section, select the checkbox labeled **Allow files by digital signature**.
3. Choose one or more certificates from the list to use as trusted sources.
4. Click **Save Updates**.

This setting can also be configured centrally if your Kiosk is enrolled in Central Management or My OPSWAT.

## [What Gets Trusted](/docs/mdkiosk/v4.8.6/configuration/trusting-files-by-digital-signature#what-gets-trusted)

- Applies to executable-type files: `.exe`, `.dll`, `.msi`, `.sys`, and `.efi`.
- A file is allowed without a full scan only if its signature is valid, current, and matches one of your configured trusted certificates.
- If a file's signature is missing, invalid, expired, or revoked, Kiosk scans it normally — it is never allowed just because signature validation didn't succeed.

Tip

Because unsigned or non-matching files are always scanned normally, enabling this option only changes behavior for files you've explicitly chosen to trust — it doesn't reduce protection for anything else.
