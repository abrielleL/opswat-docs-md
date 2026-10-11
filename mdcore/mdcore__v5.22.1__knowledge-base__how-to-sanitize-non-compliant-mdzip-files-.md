<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-sanitize-non-compliant-mdzip-files- -->

# How to Sanitize Non-Compliant MDZIP Files?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to DeepCDR version 7.4 and later, which requires MetaDefender Core version 5.14.0 or higher to function properly.

**Issue:** Some MDZIP files from customers may not strictly follow the MDZIP format, preventing them from being sanitized. R&D is unable to relax the format rules to support these non-compliant files.

**Resolution:** These files can still be sanitized as regular ZIP files, provided the settings are configured to ensure the following:

- The sanitized files retain their original `.mdzip` extension.
- All internal file names remain unchanged. This is crucial for CAMEO to read the files correctly after sanitization.

**Workarounds:**

To keep the `.mdzip` extension, consider these options:

- Manually rename the extension to `.mdzip` after sanitization.
- Wait for the new feature enhancement in Core 5.15.0.

To preserve the internal file names after sanitization:

- Enable the setting: `Preserve entry name in sanitized files`. This feature has been available starting from DeepCDR version 7.4 and later, and it needs MetaDefender Core version 5.14.0 or above to work correctly.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
