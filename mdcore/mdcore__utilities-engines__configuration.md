<!-- source: https://www.opswat.com/docs/mdcore/utilities-engines/configuration -->

# Configuration

### [Detailed explanations](/docs/mdcore/utilities-engines/configuration#detailed-explanations)

#### [Process](/docs/mdcore/utilities-engines/configuration#process)

- **Skip Encrypted Items**: When enabled, encrypted files that cannot be decrypted are excluded from the output during the compression of the processed archive.
- **Skip Malicious Items**: When enabled, files identified as malicious are excluded from the output during the compression of the processed archive. You can configure which verdicts should be skipped as malicious:

#### [Archive Sanitization](/docs/mdcore/utilities-engines/configuration#archive-sanitization)

- **Enable archive sanitization**: When this option is enabled, child files inside archive will be sanitized. Otherwise they will not be processed.
- **Distinguish partial archive process result**: When this option is enabled, if any child file within an archive cannot be sanitized for any reason (e.g., unsupported file type, unselected file type for sanitization, etc.), the sanitization result will be marked as 'Sanitized Partially.' Conversely, if all child files within the archive are successfully sanitized without failures or timeouts, the sanitization result will be marked as 'Sanitized.'

- **Add tombstone file during archive process**: please refer to this page for more detailed information: [Tombstone file](/docs/mdcore/deep-cdr/tombstone-file)

#### [Archive Compression for DLP](/docs/mdcore/utilities-engines/configuration#archive-compression-for-dlp)

When analyzing an archive file, an aggregated archive file will be produced, that contains allowed files and files processed by Proactive DLP.

Info

Should not turn on this option along with Enable Archive Sanitization option, it can make the performance down.

#### [Retain password protection on supported files](/docs/mdcore/utilities-engines/configuration#retain-password-protection-on-supported-files)

Select the supported archive file types for which you want to retain the original password.

#### [Timeout](/docs/mdcore/utilities-engines/configuration#timeout)

The designated timeout duration for the compression operation.

#### [Enable for archive compression filetypes](/docs/mdcore/utilities-engines/configuration#enable-for-archive-compression-filetypes)

Select the supported archive file types to apply compression, whether for archive sanitization or DLP processing.
