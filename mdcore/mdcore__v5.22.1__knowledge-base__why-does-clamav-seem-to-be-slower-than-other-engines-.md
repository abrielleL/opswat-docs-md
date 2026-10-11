<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-does-clamav-seem-to-be-slower-than-other-engines- -->

# Why does ClamAV seem to be slower than other engines?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Due to certain engine-specific design factors, ClamAV is known to be one of the slower performing engines included in the MetaDefender Core system.

However, ClamAV’s slow scan speed is easily counterbalanced by its high detection rate, quality, and stability.

As a workaround for the slow scan time, users can change some settings on the actual engine as described below:

- Limiting the file size that the engine should process by changing “**Max File Size**”

- Disabling “**PDF Deep Scan”** also makes the PDF scan faster but the trade-off is less detection rate.

Pro Tip:

Should you still wish to remediate slow performance, OPSWAT suggests you set the **Engine Timeout** on MetaDefender Core for **Engine Level.**

ClamAV will then scan as usual, but for files that take longer to scan, ClamAV will stop its scanning process.

Support:

If you are having issues or require further assistance regarding **Clam AV**s performance on MetaDefender Core, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
