<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-eos-eol-status-for-open-source-sof -->

# Does MetaDefender Core Detect EOS/EOL Status for Open-Source Software?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

MetaDefender Core does not directly detect whether an open-source library or software package has reached EOS/EOL. This is mainly because most open-source projects do not explicitly provide EOS/EOL information. In many cases, the absence of new releases for a long period may suggest that the project is no longer actively maintained.

However, MetaDefender Core can still help address this concern. The SBOM (Software Bill of Materials) feature provides visibility into both the current package version and the latest available version.

You can use this information to:

- Compare the current version in use with the latest version available to determine how outdated it may be.
- Assess whether they are running the latest version (which reduces operational risk).
- Identify potential risks if their version is significantly behind the latest release.

This allows you to make informed decisions about whether the software they are using may pose an operational risk due to being outdated or unsupported.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
