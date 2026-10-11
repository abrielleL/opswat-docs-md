<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/operating/multi-scanning-and-data-sanitization -->

# Multi-Scanning and Data Sanitization

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Integrating MetaDefender Core](/docs/mdmft/v3.11.5/operating/multi-scanning-and-data-sanitization#integrating-metadefender-core)

To integrate MetaDefender Managed File Transfer with Metadefender Core, follow the instructions in the [Integration with MetaDefender Core](/docs/mdmft/v3.11.5/integrations/metadefender-core-integration) guide.

Integration with MetaDefender Core provides:

- Anti-malware multi-scanning
- Data sanitization (CDR)
- Data Loss Prevention (DLP)
- Vulnerability information
- Sandbox capabilities
- Additional security features

Configuration of MetaDefender Core is done through the MetaDefender Core Management Console and requires purchasing, installing, and configuring MetaDefender Core.

Note that this user guide does not cover MetaDefender Core configuration steps; see the [MetaDefender Core User Guide](/docs/mdmft) for details.

## [Viewing Scan Results for Files](/docs/mdmft/v3.11.5/operating/multi-scanning-and-data-sanitization#viewing-scan-results-for-files)

Users can view scan results from the "My Files," "Shared with Me," "Processing History," "Approval History," or "Pending Approval" pages by clicking on any file. The scan result from MetaDefender Core will be shown in a new browser tab.

## [Viewing Scan Results for Files in a Compressed File](/docs/mdmft/v3.11.5/operating/multi-scanning-and-data-sanitization#viewing-scan-results-for-files-in-a-compressed-file)

Users can view scan results for files within a compressed file by selecting the compressed file from the "File List."

Users can then view detailed results for each specific file within the compressed file.

## [Data Sanitization (CDR)](/docs/mdmft/v3.11.5/operating/multi-scanning-and-data-sanitization#data-sanitization-cdr)

Content Disarm & Reconstruction (CDR), also known as data sanitization, treats all files as potentially malicious. It sanitizes and rebuilds each file, ensuring full usability with safe content. For more details, refer to the [MetaDefender Core documentation](/docs/mdmft).

After a file is processed by MetaDefender Managed File Transfer, it will be in the "Sanitized" state.

The MetaDefender Core scan result indicates that the file has been sanitized:

Info

Administrators and supervisors can choose between the original and sanitized versions of the file when downloading. For regular users, the redacted file is downloaded automatically.

## [Data Loss Prevention (DLP)](/docs/mdmft/v3.11.5/operating/multi-scanning-and-data-sanitization#data-loss-prevention-dlp)

The Proactive DLP engine detects and blocks sensitive data, such as credit card numbers and social security numbers. It supports a wide range of file types, including Microsoft Office documents and PDFs. For more information, refer to the [MetaDefender Core documentation](/docs/mdmft).

The user can download a redacted file with sensitive information masked, while the structure of the document remains intact. This feature leverages the Proactive DLP module from MetaDefender Core and works even if sanitization (Deep CDR) is not configured.

After the files are processed by MetaDefender Managed File Transfer, they will be in "DLP processed" state.

Sensitive data identified in the file will be displayed on the scan result page.

Info

Administrators and Supervisors can choose between the original and redacted versions of the file when downloading. For regular users, the redacted file is downloaded automatically.

Info

If both Deep CDR and DLP modules are enabled, the file will be in "Sanitized" state, and the processed file will be both sanitized and DLP-processed.

Info

MetaDefender Managed File Transfer™ sends the logged-in user's username and email address as "metadata" to MetaDefender Core, allowing the configuration of custom watermarks with ${vault_user_ name} and ${vault_email_ address} variables in the Proactive DLP process. For more details, see the [Proactive DLP watermark documentation](/docs/mdmft).

## [Sandbox](/docs/mdmft/v3.11.5/operating/multi-scanning-and-data-sanitization#sandbox)

The OPSWAT Sandbox engine in MetaDefender Core uses Adaptive Threat Analysis (ATA) to scan files for threats. For more information, refer to the [MetaDefender Core documentation.](/docs/mdmft)

If a file is scanned by the Sandbox, the MetaDefender Core scan result will indicate that no threats were detected.
