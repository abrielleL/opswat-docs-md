<!-- source: https://www.opswat.com/docs/cm/knowledge-base/is-my-opswat-central-management-an-antivirus--what-does-it-scan- -->

# Is My OPSWAT Central Management an antivirus? What does it scan exactly?

No, My OPSWAT Central Management is not an antivirus engine.

Instead, it is an antivirus detection and monitoring tool, remediation tool, and second line of defense.

> **Success**
>
> My OPSWAT Central Management allows administrators to monitor and manage the status of antivirus software and threat detection events remotely, as well as other threats on your managed endpoints, including but not limited to:
>
> - missing patches and patch management status
> - CVEs (common vulnerabilities and exposures)
> - device compliance issues (overdue virus definition updates, real-time protection status, encryption, user authentication, anti-phishing status, back-up status, firewall status, storage status, operating system status, etc.)
> - unwanted apps

## Anti-malware detection

My OPSWAT Central Management detects any of the thousands of possible anti-malware products that could be installed on your managed endpoints, then reports the following:

- installed product brand, name and version
- virus definition version and up-to-date status
- real-time protection status
- last scan date.

## Anti-malware remediation

In addition to detecting the antiviruses installed on your endpoints, and details about them, My OPSWAT Central Management can remediate several issues related to them, including but not limited to:

- attempting to enable real-time protection if it is disabled
- attempting to update antimalware definition files if they are more than X days old.

## What is scanned by My OPSWAT Central Management

My OPSWAT Central Management is a unique and highly effective second line of defense for detecting advanced malware.

There are two distinct ways in which this defense is effected, these are detailed below.

1. ### Threats are detected by multi-scanning technology

- **What:** Every 24 hours, My OPSWAT Central Management enumerates all running processes and linked libraries on each managed endpoint, hashes them, then uploads them to the [MetaDefender Cloud](https://metadefender.opswat.com) for scanning with multiple leading anti-malware engines.

If any hashes are *not* found, My OPSWAT Central Management will subsequently upload the binary of the running process or library for scanning.

- **Why**: No single anti-malware engine offers 100% detection rate, especially where new threats are concerned.

Scanning through multiple advanced engines means that you can combine the strengths of each engine, and overcome their weaknesses, guaranteeing early detection.

- **When:** If enabled, this multi-engine scanning takes place once every 24 hours.

> **Please Note:**
>
> This scan is only available on accounts equipped with the **Secure Access Module** (which features MetaDefender Cloud access), or your own [MetaDefender Core](https://www.opswat.com/products/metadefender/core) (which is available as a separate product), and can be enabled via the **Policy Management > Policies > Select a policy > **open** Settings** tab, as illustrated in the screenshots below.

![](https://uploads.developerhub.io/prod/97qW/iin2wflpv3c31mu18c5gekpl5svlgr2ukkd86yc6kbfddmn8nq3lbmtp7valyger.png)

![](https://uploads.developerhub.io/prod/97qW/pc08r02m4041hque74l9ribdv5fym8wvw3hp3xn4s6jw6ssit7ovv18k6eewkk78.png)

2. ### Repeated threats are detected by My OPSWAT Central Management

- **What:** If a local anti-malware product is installed on an endpoint device, My OPSWAT Central Management will parse the logs from the engine, and scan for threats that have been detected repeatedly within 7 days.

When a repeated threat is detected, My OPSWAT Central Management will flag the device as having a persistent infection.

When possible, My OPSWAT Central Management will also report what action, if any, was taken by the local anti-malware.

- **Why**: This is done to combat common situations in which a device’s local anti-malware is ill-equipped to completely eliminate an infection, or the endpoint user is repeatedly doing something to cause re-infection.
- **When:** This is checked at your configured frequency for endpoint device reporting - configurable from every 5 to every 60 minutes.

> **Support**
>
> For further queries or concerns regarding **Features and Functionality**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/). Alternatively, contact [OPSWAT Sales](https://www.opswat.com/contact) to learn how **My OPSWAT Central Management** could help fulfill your unique cyber-security needs.
