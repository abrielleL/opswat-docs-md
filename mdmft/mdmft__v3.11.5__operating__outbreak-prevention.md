<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/operating/outbreak-prevention -->

# Outbreak Prevention

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Outbreak Prevention protects your organization from false negative results and zero-day vulnerabilities by locking new files and automatically re-scanning them for a specified period. An overview of file processing and detection activity can be found in the "Outbreak Prevention" section.

Info

To enable Outbreak Prevention, navigate to "Settings" → "Core Integration" and enable integration with MetaDefender Core™. Outbreak Prevention cannot be used without MetaDefender Core.

Upload files to create a report.

## Enabling File Locking

To enable file locking, go to the "Outbreak Prevention" page and click the "Settings" button.

The lock interval determines how long files remain locked before they are automatically unlocked by MetaDefender Managed File Transfer™. For example, specifying 30 minutes locks new files for half an hour, after which they are re-scanned by MetaDefender Core before being unlocked.

## Enabling Periodic Automatic Rescan

To enable automatic re-scanning, go to the "Outbreak Prevention" page and click the "Settings" button**.**

The automatic rescan period determines when files should be reprocessed by MetaDefender Core™. If a file's analysis is older than the configured value, it should be rescanned. For instance, if you specify 60 minutes, files will be re-scanned if their last scan was performed over an hour ago.

After uploading files,, users can see "Total Files Processed", "Detection Activity", and "Last Processed Files."

### Configuring Allowed Times

You can configure specific time slots for automatic rescans by enabling the "Rescans in Configured Times" option. This allows you to define when rescans should start and how long they can run on selected days. It is possible to define multiple allowed time slots.

For example, rescans of files older than 60 minutes can be scheduled for Tuesdays and Fridays from 10:00 AM for two and a half hours and on Mondays from 12:30 PM for four hours.
