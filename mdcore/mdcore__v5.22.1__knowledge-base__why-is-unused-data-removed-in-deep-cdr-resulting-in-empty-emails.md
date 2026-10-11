<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-is-unused-data-removed-in-deep-cdr-resulting-in-empty-emails -->

# Why is unused data removed in Deep CDR resulting in empty emails being received?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [Issue description:](/docs/mdcore/v5.22.1/knowledge-base/why-is-unused-data-removed-in-deep-cdr-resulting-in-empty-emails#issue-description)

The end user reports receiving empty emails from a specific client. Analysis of the scan results indicates that the associated .HTML file contained 'unused data,' which was sanitized during processing.

#### [Solution:](/docs/mdcore/v5.22.1/knowledge-base/why-is-unused-data-removed-in-deep-cdr-resulting-in-empty-emails#solution)

To ensure proper sanitization in the Deep CDR engine, enable the Include Documents Without HTML Tag option. This setting is required for files with invalid or missing HTML structures, allowing the engine to process them correctly.

We are already aware of this scenario and have provided this configuration to help users bypass the issue.

Support:

If you encounter any issues or require further assistance, please contact OPSWAT support via My OPSWAT at: https://my.opswat.com/home

Our support team will be able to provide you with the necessary guidance and resolution for any license-related concerns.
