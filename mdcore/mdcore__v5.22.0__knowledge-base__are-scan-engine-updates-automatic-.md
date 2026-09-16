<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/are-scan-engine-updates-automatic- -->

# Are scan engine updates automatic?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

By default, engines and their dependent databases are downloaded and updated automatically and on schedule thanks to MetaDefender Core update settings.

When applicable, customers can configure MetaDefender Core update settings to manually update them via the Internet (on trigger), or designated local folder source, or upload engine packages manually.

MetaDefender Core update settings also supports to control update window time.

A side note that, MetaDefender Core supports to pin each engines and databases separately to avoid automatic update happening, and ensure only packages well-tested on customers' staging will be deployed in the production.

Most MetaDefender Core V5 scan engines (and their signature/definition databases) can be configured to either **Internet** (Automatic), **Local** (Automatic) or **Manual** updates, as illustrated in the screenshot below.

To learn about configuring updates for MetaDefender Core V5, visit [Engines Update Configuration](/docs/mdcore/v5.22.0/configuration/engines-update-configuration).

When configured for Automatic updates, MetaDefender Core V5 will check for available scan engine and signature/definition database updates on a regular basis. Visit [Regular Maintenance](/docs/mdcore/v5.22.0/operating/regular-maintenance) to learn more.

Pro Tip:

OPSWAT highly recommends that users upgrade to the latest version of MetaDefender Core. Current versions incorporate updated scan engines, state-of-the-art features and necessary bug fixes, and are freely available for all license holders to download.

Support:

If you have any issues configuring your **Scan Engine Updates**, or for further guidance on the subject, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
