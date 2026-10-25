<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/release-notes/release-notes-smart-touch -->

# MetaDefender Drive Smart Touch v2.3.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page

|  |  |
| --- | --- |
| **Released on** **Oct 13, 2026** | This release includes new features, improvements, bug fixes. |

**New Features**

- **Improved the Secure Files User Experience**: so the device automatically goes directly to file sharing, eliminating the need for users to manually leave Locked Mode, even before the device is plugged in.
- **Smart Touch now synchronizes system time with Central Management or My OPSWAT,** including air-gapped on-premises Central Management environments without Internet NTP access.

**Improvements**

- **Download progress:** The update progress bar displays current transfer speed alongside percentage and bytes remaining, letting administrators know how quickly a large image is arriving.
- **MetaDefender Drive uses Smart Touch Internet Bridging** as an automatic fallback when a scan host has no direct internet access, provide an option when internet is needed, under user control.
- A storage-full device can be cleared using an offline maintenance script that removes rebuildable files — such as leftover update packages, log files, caches and crash dumps, or optionally engine definitions and the MetaDefender Drive package — while never touching customer data like license keys, settings or scan reports.
- Smart Touch enrollment finishes faster — full enrollment now takes around 2 minutes rather than remounting and re-extracting unchanged components on every attempt.
- Smart Touch administrators can configure One-Time Password settings for enrolled MetaDefender Drive devices through OPSWAT Central Management, with changes synchronized automatically to ensure consistency across all platforms.
- When Central Management does not have an MetaDefender Drive image available, Smart Touch reports clearly which item was missing rather than showing a generic error.

**Bug Fixes**

- Smart Touch coredumps are now named after the crashing process and previous versions' dumps are purged on upgrade.
- MetaDefender Drive booted from Smart Touch uses the appliance's connection automatically when it has none of its own.
- MetaDefender Drive no longer fails to enroll with OPSWAT Central Management when the image is unavailable or the MetaDefender Drive version is empty, so enrollment completes with a clear status instead of reporting an error.
