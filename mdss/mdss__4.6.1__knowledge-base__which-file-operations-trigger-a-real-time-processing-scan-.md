<!-- source: https://www.opswat.com/docs/mdss/4.6.1/knowledge-base/which-file-operations-trigger-a-real-time-processing-scan- -->

# Which File Operations Trigger a Real-Time Processing Scan?

**Applies to:** MetaDefender Storage Security (MDSS) 4.6.x and later. Real-Time Processing on all storage categories, with either monitor type: Polling or Event-Based.

Real-Time Processing (RTP) scans files that are new or have changed. This article answers which everyday file operations count as a change: opening, downloading, editing, renaming, moving, or changing only a file's metadata. It gives the answer for each storage category and monitor type, then explains the rules behind it.

---

## 1. Storage categories

The answers depend on how a storage keeps and changes files, so they are given per category, as on the *Integrations* page. Storages in the same category behave the same. Where one of them differs, a note says so.

| Category | Storages | Event-Based available for |
| ---- | ---- | ---- |
| Cloud Object Storages | Amazon S3, Wasabi, Cloudian, Oracle Cloud (S3 Compatible and Native), MinIO, Cubbit, Azure Blob, Google Cloud, Alibaba Cloud, Scality RING | All except Cubbit and Oracle Cloud (S3 Compatible) |
| File Storages | Box, OneDrive, SharePoint Online, Microsoft Teams, SharePoint On-Premise, Azure Files, OPSWAT MFT | Box and SharePoint Online |
| Network Attached Storages (NAS) | NFS, NFS with Data Wrapping, SMB, NetApp ONTAP, Amazon EFS, Dell Isilon, SFTP, FTP | SMB storages through an OPSWAT connector; any NAS storage through your own tool (see below) |

Storages without Event-Based use Polling only.

**Event-Based on NAS.** MDSS does not watch NAS storages for changes: a notifier has to tell MDSS which file changed. OPSWAT provides notifiers for SMB only:

- **NetApp ONTAP**, through Vscan: ONTAP sends scan requests to the OPSWAT ONTAP Connector.
- **Other SMB-compatible storages** (Windows file servers, Samba and NAS shares), through the **OPSWAT SMB Connector**, a Windows service shown as OPSWAT SMB File Event Monitor, available from MDSS 4.7.0.

For any other NAS storage, such as NFS, SFTP or FTP, Event-Based works when your own tool notifies MDSS through the webhook described in *Event-Based request format*. Your own tool can also be used for SMB.

---

## 2. The short answer

- **Opening, viewing or downloading a file does not trigger a scan.** Reading a file changes nothing that MDSS looks at. If the application saves the file while it is open, for example with AutoSave, that save is an edit. The one exception is NetApp ONTAP, where ONTAP can ask for a scan when a file is opened (note 13).
- **Editing and saving a file triggers a scan of the new version.** On object storages, editing means uploading a new version over the object.
- **Renaming, moving and metadata-only changes depend on the category and the monitor type**, as shown below.

### Polling

| Operation | Cloud Object Storages | File Storages | NAS |
| ---- | ---- | ---- | ---- |
| Open or view a file (read only) | No | No | No (1) |
| Download a file | No | No | No |
| Edit and save a file | Yes | Yes | Yes |
| Rename a file | Yes (2) | Conditional (3) | Conditional (4) |
| Move a file to another folder | Yes (2) | Conditional (3) | Conditional (4) |
| Change only metadata or attributes | Conditional (5) | Conditional (6) | No (7) |

1. Some applications create temporary files next to the file they open. For example, Microsoft Office creates a hidden owner file whose name starts with `~$` when a document on a network share is opened for editing. That file is new, so RTP can scan it. The document itself is not scanned again.
2. Object storages have no real rename or move: tools copy the object to its new name and delete the original. The copy is a new object with a new last-modified date, so it is scanned. A storage that renames in place, such as Azure Blob with a hierarchical namespace, can keep the object's dates; note 3 then applies.
3. Yes if the file was created or last modified on or after the job's start date (see section 3), or if the operation gives the file a new modified date. Otherwise No.
4. Yes only if the file was created or last modified on or after the job's start date. File servers keep a file's dates when it is renamed or moved within the same volume, including a move into the monitored folder from elsewhere on that volume. A move to another volume is a copy followed by a delete; on Windows file servers the copy gets a new created date, so it is scanned.
5. Yes when the change rewrites the object or gives it a new last-modified date. Editing user metadata does this on S3-compatible storages and Alibaba Cloud, which copy the object onto itself, and on Azure Blob and Google Cloud. No for changes that keep the date and the ETag, such as Amazon S3 object tags.
6. Yes if the change gives the file a new modified date. Otherwise No. On SharePoint On-Premise and Azure Files, a change that gives the file a new ETag is also scanned when the file is dated on or after the job's start date.
7. File servers do not change a file's dates or size when its attributes, permissions or owner change. Properties stored inside a file, such as Office document properties edited in File Explorer, are part of its content: changing them is an edit.

### Event-Based

| Operation | Cloud Object Storages | File Storages: SharePoint Online | File Storages: Box | NAS: OPSWAT SMB Connector | NAS: NetApp ONTAP or your own tool |
| ---- | ---- | ---- | ---- | ---- | ---- |
| Open or view a file (read only) | No | No | No | No | Depends on the notifier (13) |
| Download a file | No | No | No (11) | No | Depends on the notifier (13) |
| Edit and save a file | Yes | Yes | Yes (11) | Yes (12) | Depends on the notifier (13) |
| Rename a file | Yes (8) | Yes (10) | No (11) | Yes (12) | Depends on the notifier (13) |
| Move a file to another folder | Yes (8) | Yes (10) | Conditional (11) | Yes (12) | Depends on the notifier (13) |
| Change only metadata or attributes | Conditional (9) | Yes (10) | No (11) | No (12) | Depends on the notifier (13) |

8. The documented cloud setups forward object-creation events (see section 4). A rename or move copies the object to its new name, which is an object creation, so it is scanned. An in-place rename (note 2) is not an object creation and is not scanned.
9. Yes when the change copies the object onto itself, which is an object creation: editing user metadata on S3-compatible storages and Alibaba Cloud. No on Azure Blob and Google Cloud, where editing metadata is not an object creation, and No for object tags.
10. For files inside the storage unit's scope: its document library, or its folder if one is set. A file moved out of the scope is not scanned. SharePoint reports every change it records on a file, including edits to library columns. In MDSS 4.6.x this includes some updates SharePoint makes on its own shortly after an upload, such as image tags or Office document properties, so a new file can be scanned a second time.
11. Box notifies MDSS through the webhook you create during setup, with the trigger **File Uploaded** (see *Event-based handling for Box*). Box sends File Uploaded when a file is uploaded, when a new version is saved, and when a file is moved into the folder that has the webhook. It does not send it for previews, downloads, renames or metadata changes.
12. The OPSWAT SMB Connector reports every file that is created, written or renamed in a watched share, once the file has settled, and ignores temporary names such as `~$report.docx` and `*.tmp`. A move within a share is a rename and a move into a share creates the file, so both are scanned. Attribute and permission changes on a file are not reported (connector 1.0.4 and later). Renaming a folder in place, or changing its permissions, makes the connector read the whole folder again, so its files are scanned again.
13. With NetApp ONTAP, ONTAP sends the OPSWAT ONTAP Connector a scan request when a file is accessed or modified, as its Vscan on-access policy decides, so opening or reading a file can also trigger a scan. With your own tool, MDSS scans every file the tool reports, so the answers depend on what it sends.

---

## 3. How Polling decides that a file needs a scan

Polling lists the files of the storage unit in cycles; a new cycle starts shortly after the previous one ends. A listing reads names, sizes and dates, never file content. A file is scanned when it passes two checks.

**Check 1: the file is recent enough.** The later of the file's created date and modified date must be on or after the job's start date. The start date is the moment the real-time job was last started, or the date chosen in **Pick files modified since**. The `DISCOVERY_SERVICE_<PROTOCOL>_RTP_HANDLING` setting of earlier versions is no longer used. A file changed in the last 10 seconds waits for a later cycle, so that MDSS reads complete files.

**Check 2: MDSS has not scanned this version yet.** MDSS remembers each version it scans by the file's path, its modified date and a version value from the storage:

| Category | Dates MDSS reads | Version value |
| ---- | ---- | ---- |
| Cloud Object Storages | Last modified, and created where the storage reports it | ETag (Google Cloud: MD5 or CRC32C checksum) |
| File Storages | Created and Modified | Item ID (OneDrive, SharePoint Online, Microsoft Teams), SHA-1 of the content (Box), ETag (SharePoint On-Premise, Azure Files), file ID (MFT) |
| NAS | Created (where available) and Modified | File size and modified date (FTP: the server's checksum, when it provides one) |

This explains the Polling table:

- **Open, view, download:** nothing changes, so the version is already known.
- **Edit and save:** the file gets a new modified date, so this is a new version.
- **Rename and move:** the path changes, so this is a version MDSS has not scanned, and it is scanned if it passes check 1. On object storages the renamed object is a new copy with a new date, so it always passes. Elsewhere, a file dated before the start date passes only if the operation gives it a new date.
- **Metadata or attributes only:** the path stays the same, so this is a new version only if the modified date or the version value changes, and check 1 still applies.

Two consequences to plan for:

- **Renaming or moving a folder** changes the path of every file in it. On object storages every object under the folder is copied, so all of them are scanned. On File Storages and NAS, every file in the folder that passes check 1 is scanned again.
- **The start date can move forward.** When **RTP history retention** (Data Retention) removes old results of a running job, MDSS moves the job's start date to the retention cut-off, so that the removed files are not scanned again. Files dated before the new start date then no longer pass check 1.

---

## 4. How Event-Based decides that a file needs a scan

In Event-Based mode the storage, or a system acting for it, tells MDSS which file changed, and MDSS scans that file. MDSS does not compare dates or versions and does not look at the event type, and **Pick files modified since** does not apply. Every notification for a file in the storage unit's scope can lead to a scan, including a scan of a version MDSS has already scanned.

What triggers a scan therefore depends on what is notified:

- **Cloud Object Storages:** the event setup you create in the cloud decides (see [Event-Based Real-Time Cloud Functions Examples](https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples)). The documented setups forward object-creation events: uploads, overwrites and copies.
- **SharePoint Online:** MDSS creates and renews a Microsoft Graph subscription for each document library in the unit's scope. SharePoint reports every file added or changed, including renames, moves and column edits. MDSS ignores deleted items and folders.
- **Box:** the triggers of the Box webhook decide (note 11).
- **NAS:** the notifier decides: the OPSWAT SMB Connector (note 12), NetApp ONTAP through Vscan, or your own tool (note 13).

Because every notification can lead to a scan, Event-Based mode can scan the same file several times. AutoSave and co-authoring, for example, can save several versions of a document within minutes, and each one can be scanned. Polling scans the version it finds in each cycle, once the file has been unchanged for 10 seconds.

### Polling and Event-Based compared

|  | Polling | Event-Based |
| ---- | ---- | ---- |
| What starts a scan | A new version found by the next listing cycle | A notification |
| Files dated before the start date | Not scanned, even after a rename or move, unless the operation gives them a new date (object storage copies always get one) | Scanned when notified; the start date does not apply |
| Same version scanned again | No | Possible, once per notification |
| Available for | All storages | See section 1 |

---

## 5. Recommendations

- **To scan renamed and moved files whatever their age** on File Storages and NAS, create the Polling job with **Pick files modified since** set to **Use the oldest available timeframe**. Every file then passes check 1: the first cycles scan the existing files in scope, and after that every rename or move is scanned. Expect a large first backlog on big storages.
- **To rescan files that have not changed**, for example after an engine update, run an on-demand or scheduled scan. Real-Time Processing only scans new versions.
- **Cover the gaps of Event-Based.** Notifications that arrive while an Event-Based job is stopped are refused, so changes made in that time may never be scanned. Run an on-demand scan for that period, and consider a scheduled scan at a long interval, for example weekly, as a safety net.
- **Forward only the events that the setup guides use.** MDSS scans the file named in every notification, whatever the event type. On object storages, forward only object-creation events: delete events end as "file not found" errors, and other events add scans. On Box, keep File Uploaded as the only trigger: File Previewed or File Downloaded would scan a file every time it is opened or downloaded.
- **Run one OPSWAT SMB Connector per share.** Two connectors watching the same share make MDSS scan every file twice.
- **Workflow filters still apply.** A changed file that the workflow's filters exclude is not scanned.
- **To find out why Polling skipped a file**, search the Discovery service log (included in the support package) for `predates the real-time start date`. MDSS logs this line for each file dated before the job's start date.

---

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/4.6.1/llms.txt)
