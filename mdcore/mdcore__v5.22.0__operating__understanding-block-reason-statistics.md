<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/operating/understanding-block-reason-statistics -->

# Understanding Block Reason Statistics

## [Overview](/docs/mdcore/v5.22.0/operating/understanding-block-reason-statistics#overview)

When files are blocked in the OPSWAT MetaDefender Core system, they can be blocked for multiple reasons simultaneously (e.g., a file might be both "Infected" and contain "Sensitive Data Found"). To make statistics clearer and more actionable, our system reports each blocked file under only one block reason in statistical reports - the highest priority reason.

## [How Block Reasons Work](/docs/mdcore/v5.22.0/operating/understanding-block-reason-statistics#how-block-reasons-work)

### [Files with Multiple Block Reasons](/docs/mdcore/v5.22.0/operating/understanding-block-reason-statistics#files-with-multiple-block-reasons)

When a file is scanned, it may trigger multiple block verdicts, for example:

- Malware detection ("Infected")
- Sensitive Data Found
- File type restrictions (Blocklisted by File Type)
- Size limitations (Blocklisted by File Size)
- Failed sanitization
- And many others

All applicable block reasons are recorded for each file in the detailed scan results. However, for statistical reporting, only the highest priority reason is counted.

### [Archive Files](/docs/mdcore/v5.22.0/operating/understanding-block-reason-statistics#archive-files)

Archive files (ZIP, RAR, etc.) present a special case:

- An archive itself might not directly trigger any block reasons
- However, if any file within the archive is blocked, the archive inherits block reasons from its contents
- If multiple files within an archive are blocked for different reasons, the archive will have multiple block reasons

## [Block Reason Priority](/docs/mdcore/v5.22.0/operating/understanding-block-reason-statistics#block-reason-priority)

When counting files for statistical purposes, we use a priority-based system where each file is counted only once under its highest priority block reason.

The general priority order (from highest to lowest) is:

1. Blocklist configure in workflow rule: Block by file type, file size, etc.
2. Security threats (Infected, Suspicious).
3. Policy violations (Sensitive Data Found, Country of Origin).
4. Processing issues (Failed Sanitization, Password Protected).
5. Workflow rule configuration (File Size Exceeded, Timeout).

## [Example: Understanding Block Statistics](/docs/mdcore/v5.22.0/operating/understanding-block-reason-statistics#example-understanding-block-statistics)

If our system reports:

- 5 files blocked due to "Infected"
- 4 files blocked due to "Blocklisted by File Size"
- 1 file blocked due to "Sensitive Data Found"

This means:

- 5 files had "Infected" as their highest priority block reason (they may have had other reasons too)
- 4 files had "Blocklisted by file size" as their highest priority reason
- 1 file had "Sensitive Information Found" as its highest priority reason

## [Important Notes](/docs/mdcore/v5.22.0/operating/understanding-block-reason-statistics#important-notes)

1. **Complete details are available**: While statistics show only the highest priority reason, complete block information for each file is available in detailed scan results.
2. **Archive handling**: An archive containing multiple blocked files is counted as a single blocked file in statistics, using the highest priority block reason among all its contents.
3. **Accuracy**: This prioritization system ensures each file is counted exactly once in statistics, preventing inflated numbers while highlighting the most critical issues.

By understanding how block reasons are prioritized and counted, you can better interpret security statistics and focus remediation efforts on the most critical issues first.
