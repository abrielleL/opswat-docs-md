<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/what-is-the-document-encryption-timeout-setting-and-how-does-it- -->

# What is the Document Encryption Timeout setting and how does it work?

This article applies to all MetaDefender Core V5 releases deployed on Windows and Linux systems.

The **Document Encryption Timeout** is a configurable setting located under: **Workflows > DeepCDR > Timeouts > Document encryption**

This setting specifies the maximum duration MetaDefender Core allows for re-encrypting a sanitized document during the Deep CDR process.

### [When is this setting used?](/docs/mdcore/v5.22.0/knowledge-base/what-is-the-document-encryption-timeout-setting-and-how-does-it-#when-is-this-setting-used)

The Document Encryption Timeout is only applicable when the option **“Retain password protection on supported document files”** is enabled.

When MetaDefender Core detects an encrypted document or archive (e.g., password-protected PDF, Word, or Excel file), the system performs the following steps:

1. Attempts to decrypt the file using a list of preconfigured passwords.
2. Once successfully decrypted, the Deep CDR engine sanitizes the file to remove potential threats.
3. The sanitized content is then recompressed and re-encrypted using the original password.
4. If this re-encryption process exceeds the configured timeout value, MetaDefender Core will return a timeout error.

### [Why you may need to modify this setting](/docs/mdcore/v5.22.0/knowledge-base/what-is-the-document-encryption-timeout-setting-and-how-does-it-#why-you-may-need-to-modify-this-setting)

By default, the timeout is set to 5 minutes. In some environments, especially when processing large or complex encrypted files, the default timeout value may not be sufficient to complete the re-encryption process. If you notice timeout errors during the sanitization of encrypted documents, you may need to increase the Document Encryption Timeout to ensure these files can be processed successfully without interruption.

Adjusting this setting can help balance security, performance, and user experience depending on your organization's needs.

Support:

If **Further Assistance** is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/portal/support).
