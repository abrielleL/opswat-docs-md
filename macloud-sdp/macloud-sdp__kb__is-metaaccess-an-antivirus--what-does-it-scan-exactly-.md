<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/is-metaaccess-an-antivirus--what-does-it-scan-exactly- -->

# Is MetaDefender IT Access an antivirus? What does it scan exactly?

This article applies to all MetaDefender IT Access products deployed on Windows, macOS, Linux, Android and iOS systems.

No, MetaDefender IT Access is not an antivirus engine.

Instead, it is an antivirus detection and monitoring tool, remediation tool, and second line of defense.

Success

MetaDefender IT Access allows administrators to monitor and manage the status of antivirus software and threat detection events remotely, as well as other threats on your managed endpoints, including but not limited to:

- missing patches and patch management status
- CVEs (common vulnerabilities and exposures)
- device compliance issues (overdue virus definition updates, real-time protection status, encryption, user authentication, anti-phishing status, back-up status, firewall status, storage status, operating system status, etc.)
- unwanted apps.
## Anti-malware detection

MetaDefender IT Access detects any of the thousands of possible anti-malware products that could be installed on your managed endpoints, then reports the following:

- installed product brand, name and version
- virus definition version and up-to-date status
- real-time protection status
- last scan date.

## Anti-malware remediation

In addition to detecting the antiviruses installed on your endpoints, and details about them, MetaDefender IT Access can remediate several issues related to them, including but not limited to:

- attempting to enable real-time protection if it is disabled
- attempting to update antimalware definition files if they are more than X days old.

## What is scanned by MetaDefender IT Access

MetaDefender IT Access is a unique and highly effective second line of defense for detecting advanced malware.

There are two distinct ways in which this defense is effected, these are detailed below.

1. ### Threats are detected by multi-scanning technology

- **What:** Every 24 hours, MetaDefender IT Access enumerates all running processes and linked libraries on each managed endpoint, hashes them, then uploads them to the [MetaDefender Cloud](https://metadefender.opswat.com) for scanning with multiple leading anti-malware engines.

If any hashes are *not* found, MetaDefender IT Access will subsequently upload the binary of the running process or library for scanning.

- **Why**: No single anti-malware engine offers 100% detection rate, especially where new threats are concerned.

Scanning through multiple advanced engines means that you can combine the strengths of each engine, and overcome their weaknesses, guaranteeing early detection.

- **When:** If enabled, this multi-engine scanning takes place once every 24 hours.

Please Note:

This scan is only available on accounts equipped with the **Secure Access Module** (which features MetaDefender Cloud access), or your own [MetaDefender Core](https://www.opswat.com/products/metadefender/core) (which is available as a separate product), and can be enabled via the **MetaDefender IT Access** **Console>Policy Management>Policies>Relevant Policy>Settings** tab, as illustrated in the screenshots below.

2. ### Repeated threats are detected by MetaDefender IT Access

- **What:** If a local anti-malware product is installed on an endpoint device, MetaDefender IT Access will parse the logs from the engine, and scan for threats that have been detected repeatedly within 7 days.

When a repeated threat is detected, MetaDefender IT Access will flag the device as having a persistent infection.

When possible, MetaDefender IT Access will also report what action, if any, was taken by the local anti-malware.

- **Why**: This is done to combat common situations in which a device’s local anti-malware is ill-equipped to completely eliminate an infection, or the endpoint user is repeatedly doing something to cause re-infection.
- **When:** This is checked at your configured frequency for endpoint device reporting - configurable from every 5 to every 60 minutes.

Support:

For further queries or concerns regarding **MetaDefender IT-OT Access** **Features and Functionality**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/). Alternatively, contact [OPSWAT Sales](https://www.opswat.com/contact) to learn how **MetaDefender IT-OT Access** could help fulfill your unique cyber-security needs.
