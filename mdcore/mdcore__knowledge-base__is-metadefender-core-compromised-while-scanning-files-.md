<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/is-metadefender-core-compromised-while-scanning-files- -->

# Is Metadefender Core compromised while scanning files?

This article applies to all MetaDefender Core V5 releases deployed on Windows or Linux systems.

No, it is not.

Writing a malicious file to the disk does not mean it can do harm since, to activate malware, the malicious files must first be interpreted. MetaDefender Core does not interpret or run the files that are written to the disk - it only uses them as bitstreams.

Additional “Temporary processing files” name is randomized to avoid accidentally trigging the files, we are taking this approach to minimize the risk that malicious files could be triggered while processing. It follows that Metadefender Core should not be compromised during scans.

Support:

If you believe that MetaDefender Core has somehow been compromised during a scan, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
