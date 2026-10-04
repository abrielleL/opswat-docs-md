<!-- source: https://www.opswat.com/docs/mddrive/getting-started/engines-technologies-statuses -->

# Engines and Technologies Statuses

MetaDefender Drive shows the status of every engine in two places: the **Engines** page, and the **Initializing Engines** window that opens when you start a scan. This page lists every status you can see, what it means, and whether you should wait, act, or go ahead and scan.

## [Status summary](/docs/mddrive/getting-started/engines-technologies-statuses#status-summary)

| Group | Statuses | What to do |
| --- | --- | --- |
| **Ready** (green) | Active · Available · Ready to scan (Initializing Engines window only) | Nothing. An Available engine is switched on automatically when a scan uses it. |
| **Wait** (orange) | Waiting for download · Downloading · Prepared · Staging · Validating · Extracting · Updating · Scheduled | The engine is being installed or updated. Wait; it moves on by itself. |
| **Needs attention** (orange) | Licensed · Download failed · Temporary failed · Permanently Failed (shown as Failed in the Initializing Engines window) · Content invalid | The engine cannot scan. Usually fixed by running an engine update. |

The dot next to each engine name is green when the engine is ready and orange for every other status. **Not Selected** appears only in the Initializing Engines window. It means the scan does not use the engine, and needs no action.

## [How an engine moves through its statuses](/docs/mddrive/getting-started/engines-technologies-statuses#how-an-engine-moves-through-its-statuses)

*Figure 1. Engine status flow.*

A failure can happen while an engine downloads or installs. Running an engine update removes an engine in **Download failed**, **Temporary failed** or **Permanently Failed**; it then shows as **Licensed** until an update that includes it installs it again. **Content invalid** is not removed; it needs a freshly downloaded update package.

An **Active** engine keeps scanning while its next update downloads and installs, so during a definitions update its row can stay on Active. **Scheduled** is often too brief to notice.

## [Engines page](/docs/mddrive/getting-started/engines-technologies-statuses#engines-page)

Each tab lists one kind of engine: Archive / FileType, Anti-Malware, Vulnerability, Data Loss Prevention, and In-Session Scan. The **Last Update** column shows the date of the engine's current definitions once the engine is installed, and is blank while it is still being installed. A tab that reads "Waiting on … engines" has no engine of that kind listed yet.

### [Ready](/docs/mddrive/getting-started/engines-technologies-statuses#ready)

| Status | What it means | What to do |
| --- | --- | --- |
| **Active** | Installed, switched on, and used for scanning. | Nothing. |
| **Available** | Installed but switched off, for example because your engine settings do not use it. | Nothing. It is switched on automatically when a scan uses it. |

### [Wait](/docs/mddrive/getting-started/engines-technologies-statuses#wait)

| Status | What it means | What to do |
| --- | --- | --- |
| **Waiting for download** | An update for this engine is queued. | Wait. |
| **Downloading** | The engine or its definitions are being copied to the drive. A progress bar shows how far it has got, with the speed and time remaining when they are known. | Wait. Keep the network connection (online update) or the update media (offline update) available until it finishes. |
| **Prepared** | The download is complete and the engine is waiting to be installed. | Wait. If it stays here a long time, see "If a status does not change" section. |
| **Staging**, **Validating**, **Extracting**, **Updating** | The engine is being checked, unpacked and installed. | Wait. |
| **Scheduled** | Installed, and about to be switched on. | Wait. It becomes Active by itself. |

### [Needs attention](/docs/mddrive/getting-started/engines-technologies-statuses#needs-attention)

| Status | What it means | What to do |
| --- | --- | --- |
| **Download failed** | The engine could not be copied to the drive. | Check the network connection or the offline update media, then run the engine update again. The engine is removed and shows as Licensed until the update installs it again. |
| **Temporary failed** | Installing the engine failed, and it may succeed on a retry. On some drives this reads "Temporarily_failed". | Wait a few minutes. If it does not change, run an engine update. The engine is removed and shows as Licensed until the update installs it again. |
| **Permanently Failed** | The engine could not be installed and will not be retried by itself. It cannot scan. | Run an engine update that includes this engine. The broken engine is removed, shows as Licensed for a while, then is installed again. |
| **Content invalid** | The update package for this engine is damaged or incomplete. | Run the update with a freshly downloaded package. If it happens again, contact OPSWAT Support. |

## [Initializing Engines window](/docs/mddrive/getting-started/engines-technologies-statuses#initializing-engines-window)

When you start a scan, MetaDefender Drive switches on the engines the scan needs and switches off the ones it does not. The **Initializing Engines** window lists every engine while this happens, with engines that are not ready yet at the top. Its statuses refresh every few seconds, and the scan starts by itself once every engine it needs is ready. If all engines are already ready, the window may only flash briefly.

*Figure 2. What can happen when you start a scan.*

The window has no time limit. It stays open until every engine the scan needs is ready, an engine fails, or you press **Cancel**.

| Status | What it means | What to do |
| --- | --- | --- |
| **Ready to scan** | The engine is on and ready for this scan. | Nothing. |
| **Scheduled** | The engine is installed and being switched on for this scan. An engine that the Engines page shows as Available reads Scheduled here. | Wait. |
| **Not Selected** | This scan does not use the engine. | Nothing. |
| **Prepared**, **Downloading**, **Staging** and the other install statuses | The same meaning as on the Engines page: the engine is still being installed. | Wait, or press **Cancel** and start the scan when the Engines page shows it as Active. |
| **Failed** | The same engine the Engines page shows as Permanently Failed. | The scan cannot use it. See the messages below. |

### [Messages you may see when starting a scan](/docs/mddrive/getting-started/engines-technologies-statuses#messages-you-may-see-when-starting-a-scan)

| Message | What it means | What to do |
| --- | --- | --- |
| *Engines are still being installed (N of M ready). Please wait for the installation to complete before scanning.* | An engine update is still installing engines. Scanning now would leave some engines out. | Wait until the Engines page shows the engines as Active, then start the scan again. |
| *Some engines are not ready to use and will affect the overall scan results. Are you sure you want to continue?* | One or more engines cannot be used. When the drive can tell which ones, they are named in the message. | **Continue** scans without them, so the results may be incomplete. **Cancel** and run an engine update for full coverage. |
| *N engines have been outdated for over N days. Please update them to continue, or cancel to select a different scan type allowed by policy.* | **Engine Policy Violation**: your engine policy does not allow scanning with engines this old. | **Update Engines** opens the Engines page. **Edit Anti-Malware Engines Settings** changes which engines are used. Or cancel and choose a scan type the policy allows. |
| *Malware engines are not active and scanning cannot start. Install or Update the engines to enable scanning.* | An engine the scan needs could not be switched on, or no engines are installed. | Open the Engines page, fix any engine that needs attention (see the Needs attention table above), then scan again. |
| *The File Type and Archive engines are not ready, so scanning cannot start. Please try again once both engines are available.* | Every scan needs the File Type and Archive engines, and they were not ready in time. | Check the Archive / FileType tab on the Engines page. Run an engine update if either one needs attention, then try again. |

## [Why the same engine can read differently in the two places](/docs/mddrive/getting-started/engines-technologies-statuses#why-the-same-engine-can-read-differently-in-the-two-places)

| Engines page | Initializing Engines | Why |
| --- | --- | --- |
| Active | Ready to scan | Same status, different wording. |
| Available | Scheduled | The engine is installed but switched off. The scan is switching it on, so it shows orange until it is ready. |
| Permanently Failed | Failed | Same status, shorter label. |
| any status | Not Selected | The engine is not used by this scan, so its install status does not matter here. |
| Licensed | not listed | The engine is not installed, so there is nothing for the scan to switch on. |

## [If a status does not change](/docs/mddrive/getting-started/engines-technologies-statuses#if-a-status-does-not-change)

1. **Downloading** with a progress bar that does not move: check the network connection, or the offline update media.
2. **Prepared**, **Staging** or another install status that stays the same for more than 30 minutes: run the engine update again. On slow USB media a large offline update can take a long time, so give it that long before retrying.
3. **Initializing Engines** that stays on the same statuses: press **Cancel**, open the Engines page, and handle any engine that is not Active or Available.
4. If an engine keeps returning to **Permanently Failed** or **Content invalid** after an update, contact OPSWAT Support, and include the engine name and the drive's logs.
