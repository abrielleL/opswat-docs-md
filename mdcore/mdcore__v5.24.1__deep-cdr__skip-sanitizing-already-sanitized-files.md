<!-- source: https://www.opswat.com/docs/mdcore/v5.24.1/deep-cdr/skip-sanitizing-already-sanitized-files -->

# Skip Sanitizing Already-sanitized Files

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

If a submitted file is the output of a previous Deep CDR sanitization, MetaDefender Core skips Deep CDR for that file.

For example, Deep CDR sanitizes file A and produces A′. If A′ is submitted later, MetaDefender Core recognizes it as already sanitized, skips Deep CDR, and does not create a new sanitized file.

Sanitization is skipped only when both of the following match the original sanitization:

- Deep CDR settings
- Deep CDR engine version

To enable **Skip Sanitizing Already-sanitized Files** option, modify rule under

- **Workflow Management> Workflows > Workflow Name > Deep CDR** > **Process**.

- Sanitize result will be **Sanitization Skipped By Rule**

**Supported file types:**

- Non archive file only
