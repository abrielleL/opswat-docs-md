<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-can-i-reduce-the-number-of-false-positives-in-threat-detecti -->

# How can I reduce the number of false positives in threat detection?

This article applies to the current MetaDefender IT Access Console, MetaDefender Cloud, supported versions of the MetaDefender Core API, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

To reduce the number of **False Positives** being reported by MetaDefender IT Access’s **Threat Detection** feature (available via integration with MetaDefender Cloud or MetaDefender Core API), please do the following.

Please Note:

Bear in mind that, while the following methods may limit the number of false positives being detected, they may also lessen the efficacy of overall threat detection.

## [Option 1](/docs/macloud-sdp/kb/how-can-i-reduce-the-number-of-false-positives-in-threat-detecti#option-1)

1. Open your **MetaDefender IT Access Console** and navigate to **Policy Management>Policies>Relevant Policy>Settings>Threat Detection**.
2. Adjust the option to **Consider a file as a THREAT/BLOCKED if it’s reported as suspicious by X or more engines**.
3. Then, click **Save**, as illustrated below.

Pro Tip:

While the default setting is 1 anti-malware engine, you are free to select up to the number of engines supported by your MetaDefender IT Access license and scan source settings (scan server settings).

Raising the number above the default would mean that you would not be notified of any threat unless X number of engines detected it, thereby reducing the number of false-positives reported, potentially.

## [Option 2](/docs/macloud-sdp/kb/how-can-i-reduce-the-number-of-false-positives-in-threat-detecti#option-2)

1. Open your **MetaDefender IT Access Console** and navigate to **Policy** **Management>Policies>Relevant Policy>Settings>Threat Detection**.
2. Select the engines that you would like to use for threat detection under this policy, by unchecking the selection boxes alongside the engines that you feel are responsible for the most false positives.
3. Finally, click **Save**, as illustrated below.

Pro Tip:

The lower the number of engines selected for threat scanning, the lower the number of false-positives, potentially, but the lower the efficacy of overall threat detection.

The higher the number of engines selected for threat scanning, the higher the number of false-positives, potentially, but the higher the efficacy of overall threat detection.

Support:

For queries, concerns or issues regarding **Reducing The Number Of False Positives In Threat Detection**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
