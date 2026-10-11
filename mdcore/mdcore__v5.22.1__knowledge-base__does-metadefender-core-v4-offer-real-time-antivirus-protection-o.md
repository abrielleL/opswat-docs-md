<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-v4-offer-real-time-antivirus-protection-o -->

# Does MetaDefender Core v5 offer real-time antivirus protection on the system where it is installed?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases installed on Windows or Linux systems.

No.

Although MetaDefender Core uses a number of antivirus engines that are typically found in real-time anti-malware products, it does not offer **real-time** protection for the system on which it is installed.

MetaDefender Core is designed to scan only those files that are submitted to it on demand.

Pro Tip:

If real-time protection is required, OPSWAT recommends installing an additional, real-time anti-malware protection product on the MetaDefender Core server.

However, when installing a real-time protection agent on the MetaDefender Core server, be sure to exclude both MetaDefender Core’s **Installation** directory and its **Temporary** directory (used for scanning) from the protection agent’s coverage.

Please Note:

Be advised that, should you choose to leverage a pre-installed anti-malware engine for real-time protection that also happens to be included as a scan engine in your MetaDefender Core V4 or V5 release, there are similar exception rules that will need to be applied.

Read [This Article](/docs/mdcore/v5.22.1/knowledge-base/how-to-mitigate-scan-failures-in-metadefender-core-triggered-by-) learn more.

Support:

Feel free to contact OPSWAT Support for expert guidance when installing additional **Protection Agents** or **Programming Exceptions**. Log a [support case or chat with our support engineer](https://my.opswat.com/portal/support) to get in touch.
