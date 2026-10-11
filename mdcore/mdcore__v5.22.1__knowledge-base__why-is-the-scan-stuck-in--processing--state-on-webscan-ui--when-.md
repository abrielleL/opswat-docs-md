<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-is-the-scan-stuck-in--processing--state-on-webscan-ui--when- -->

# Why is the scan stuck in "processing" state on WebScan UI, when the Core Processing History shows that it is already finished?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

If a file has been submitted for scan via WebUI, WebUI will make 999 queries as part of the polling process.

If file analysis progress hasn’t reached 100% by the time the polling stops, the WebUI will appear to be frozen.

Remedy:

A simple webpage refresh will reset the query counter and allow the WebUI to continue fetching results.

Support:

If you have refreshed the webpage but the WebUI is still stuck in a **Processing** state, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
