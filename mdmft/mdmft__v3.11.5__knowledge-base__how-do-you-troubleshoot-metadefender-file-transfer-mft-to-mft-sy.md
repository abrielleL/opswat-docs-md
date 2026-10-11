<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy -->

# How do you troubleshoot MetaDefender File Transfer MFT-to-MFT synchronization issues?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

**Check Your Version:**

This article applies to all MetaDefender File Transfer releases deployed on Windows that use MFT-to-MFT synchronization to transfer files between MFT instances.

## [**Overview**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#overview)

MFT-to-MFT synchronization issues can appear as failed transfers, delayed file availability, inconsistent sync behavior, or files that do not appear in the expected destination folder.

These issues are commonly related to:

- network interruptions
- authentication or permission changes
- destination-side processing delays
- storage availability
- environmental changes such as firewall, proxy, DNS, or certificate updates.

This article provides a safe troubleshooting process to help administrators identify where the transfer stopped and what information to collect before contacting OPSWAT Support.

---

## [**Common Symptoms**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#common-symptoms)

Use this article when one or more of the following symptoms occur:

- Files sync inconsistently between MFT systems.
- Some files transfer successfully while others do not.
- A sync job appears successful, but files are not visible in the expected destination.
- Manual re-sync works sometimes but not consistently.
- Files appear late on the destination MFT

## [**Check the transfer direction and topology**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#check-the-transfer-direction-and-topology)

First, determine whether the issue occurs in one direction or both directions. For example, confirm whether files fail only from the source MFT to the destination MFT, only in the reverse direction, or in both directions.

Also review the network path between the systems. If the transfer path includes a firewall, proxy, load balancer, diode, bidirectional security gateway, or other network security device, include it in the investigation. Session timeout, inspection, routing, or reset behavior in the network path can interrupt transfers even when both MFT instances are healthy.

## [**Confirm where the file stopped**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#confirm-where-the-file-stopped)

A reported sync issue does not always mean the transfer itself failed. The file may have stopped at different points in the workflow.

For example, the file may still be waiting on the source system, may have transferred but not completed destination-side processing, may be delayed by scanning, or may have been written to an unexpected folder due to configuration.

When investigating, confirm whether the file:

- Exists on the source MFT.
- Was selected by the sync or automation job.
- Reached the destination MFT.
- Is still processing on the destination.
- Was written to the expected destination folder.
- Has completed any required scanning or post-processing.

This helps separate transfer failures from processing delays or visibility issues.

## [**Check connectivity and network stability**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#check-connectivity-and-network-stability)

If different files fail at different times, or if manual retry works inconsistently, review the network path carefully. Intermittent failures often indicate that a session is being interrupted while the transfer is in progress.

Administrators should check firewall, proxy, gateway, load balancer, DNS, TLS, and routing behavior between the MFT systems. Pay special attention to timeout settings, TLS inspection, session reset behavior, and recent network changes.

If the issue involves a diode, bidirectional security gateway, or other controlled transfer path, verify that the device is not interrupting or delaying sessions unexpectedly.

## [**Validate credentials and permissions**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#validate-credentials-and-permissions)

Authentication and authorization changes can stop MFT-to-MFT synchronization even when connectivity is working.

Confirm that the credential or API key used by the sync configuration is still valid, has not expired, has not been revoked, and belongs to an active account. Also confirm that the account has the required access to the source and destination folders.

If the sync configuration uses an API key, verify that the key validity period is appropriate for the integration. If the key was recently rotated, confirm that the new key was updated in all required locations.

## [**Check destination-side processing**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#check-destination-side-processing)

Sometimes the file transfer succeeds, but the file does not appear immediately where users expect it. In these cases, the destination MFT may still be processing the file, scanning it, writing it to storage, or waiting behind other queued work.

Review the destination MFT health, storage availability, system resource usage, and MetaDefender Core processing status if scanning is part of the workflow. High file volume, large batches, storage pressure, or scan queue delays can make a successful transfer appear to be a failed sync.

If the file reached the destination but remains pending, focus the investigation on destination-side processing rather than source-side transfer.

## [**Safe recovery actions**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#safe-recovery-actions)

After the likely cause has been identified and corrected, **retry a single affected file first**. This helps confirm whether the issue is resolved before retrying a larger batch.

If files are delayed or appear incomplete, confirm their status on both the source and destination systems before deleting or re-uploading anything.

Do not remove source files until successful delivery and processing on the destination have been confirmed.

If repeated cleanup messages or temporary file issues are observed after an interrupted transfer, **collect logs before restarting services** or making manual changes. If a service restart is required, perform it during an approved maintenance window or under guidance from OPSWAT Support.

## [**What to avoid**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#what-to-avoid)

Avoid treating a successful job summary as proof that the file reached the expected destination. Always confirm the file location, processing status, and scan status if applicable.

**Avoid deleting temporary files manually** while MFT services are running unless instructed by OPSWAT Support.

## [**Information to collect before contacting OPSWAT Support**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#information-to-collect-before-contacting-opswat-support)

To help OPSWAT Support investigate the issue more effectively and respond as quickly as possible, please gather the following information before opening a support case:

- MFT version on both systems
- Direction of the failure
- Affected file names and approximate timestamps
- Sync or automation job configuration details
- Whether the issue is consistent or intermittent
- Whether manual retry succeeds or fails
- Whether a firewall, proxy, gateway, diode, load balancer, or other network device is in the path
- Recent changes to credentials, certificates, DNS, firewall rules, proxies, storage, permissions, or automation jobs
- Support package from both the source and destination MFT systems for the same timestamp window
- MetaDefender Core processing details if scanning is involved

Providing logs from both sides helps determine whether the issue occurred before transfer, during transfer, or during destination-side processing.

## [**Summary**](/docs/mdmft/v3.11.5/knowledge-base/how-do-you-troubleshoot-metadefender-file-transfer-mft-to-mft-sy#summary)

MFT-to-MFT synchronization issues are usually caused by connectivity interruptions, credential or permission problems, destination-side processing delays, storage conditions, or recent environmental changes.

**Support:**

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support) and share the gathered information about the issue.
