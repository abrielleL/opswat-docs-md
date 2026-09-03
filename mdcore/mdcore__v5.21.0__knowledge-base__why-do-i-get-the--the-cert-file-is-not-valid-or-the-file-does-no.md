<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-do-i-get-the--the-cert-file-is-not-valid-or-the-file-does-no -->

# Why do I get the "The cert file is not valid" or "the file does not exist" when adding my cert?

**Check Your Version:**

This article applies to all MetaDefender Core releases after v5.8.0 on both Windows and Linux systems.

When adding a certificate to MetaDefender Core, you may encounter the error: “The cert file is not valid or the file does not exist.” This error can occur for a variety of reasons, often related to file type mismatches, missing passphrases, permission issues, or problems with the certificate’s content and chain. By understanding the common causes, you can more efficiently troubleshoot and ensure your certificate is properly recognized by MetaDefender Core.

## [Possible Causes & Solutions](/docs/mdcore/v5.21.0/knowledge-base/why-do-i-get-the--the-cert-file-is-not-valid-or-the-file-does-no#possible-causes--solutions)

### [1. Incorrect File Type or Mismatch](/docs/mdcore/v5.21.0/knowledge-base/why-do-i-get-the--the-cert-file-is-not-valid-or-the-file-does-no#1-incorrect-file-type-or-mismatch)

- Verify you’re using the correct SSL file types (e.g., .crt for certificate and .key for private key).
- Attempting to upload a PFX bundle (or other certificate formats) will cause an error.

  - MetaDefender Core requires a Base64-encoded file that contains only the leaf certificate, ideally without additional chain or encoding variations.
- Ensure the certificate and key match—mismatched pairs can cause validation errors. You can verify via OpenSSL hashes

### [2. **Missing Passphrase File (if applicable)**](/docs/mdcore/v5.21.0/knowledge-base/why-do-i-get-the--the-cert-file-is-not-valid-or-the-file-does-no#2-missing-passphrase-file-if-applicable)

- If your private key is encrypted, you must supply the passphrase—typically via a separate passphrase file.
- There’s an optional "Password File" field during certificate upload. If omitted for an encrypted key, it will cause failure. [OPSWAT](https://www.opswat.com/docs/ocm/configuration/enabling-https?utm_source=chatgpt.com)

### [3. **Location & Filesystem Permissions (Linux)**](/docs/mdcore/v5.21.0/knowledge-base/why-do-i-get-the--the-cert-file-is-not-valid-or-the-file-does-no#3-location--filesystem-permissions-linux)

- Confirm that both .crt and .key files are correctly placed in /etc/ometascan/nginx.d.
- They must be owned by the metascan user, with read/write permissions for that user.
- If these files are missing, inaccessible, or have incorrect ownership/permissions, it results in the “not valid or does not exist” error.

### [4. **Certificate Content & Chain Issues**](/docs/mdcore/v5.21.0/knowledge-base/why-do-i-get-the--the-cert-file-is-not-valid-or-the-file-does-no#4-certificate-content--chain-issues)

- Ensure the certificate’s **Subject** or **Subject Alternative Name** contains the server’s FQDN or IP.
- If it's a wildcard certificate, it must match the server’s domain.
- Confirm that the full certificate chain (intermediate and root CAs) is trusted on the system—missing or untrusted chain members can break the validation process.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
