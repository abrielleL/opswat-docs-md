<!-- source: https://www.opswat.com/docs/mdss/4.6.0/release-notes/release-notes -->

# Release notes

## **MetaDefender™ Storage Security 4.6.0**

**Release date:** October 5, 2026

**End of support**: April 5, 2028

#### **New Features**

- **Workflow file filters.** A workflow can now skip files by type, size and last modified date before they reach a scan pool, saving scan capacity for the files you care about. In this release the filters are set through the REST API. Skipped files are listed in the report and the PDF export with the filter that excluded them, and each gets an audit entry.
- **Scan pool routing rules.** A scan pool can now mix MetaDefender Core and MetaDefender Cloud instances. In Settings, Scan Pools, Configure Routing you choose a balancing algorithm (least recently used or lowest outstanding), add ordered rules that send files to specific instances by type or size, and decide what happens to files no rule matches. Configuration export and import include the routing settings.
- **Automatic storage unit sync for the NetApp ONTAP Connector.** The OPSWAT ONTAP Connector reads the storage units under event-based real-time protection from MDSS and keeps its own configuration current, adding units when protection starts and removing them when it stops, with no manual edits and no service restart. Share path and server address changes made in MDSS are picked up as well.
- **Usage dashboard.** A new Usage tab on the Dashboard shows, for one storage unit, a timeline of past, running and upcoming scans and a heat map of files processed per hour over the selected date range, up to 90 days.

#### **Enhancements**

- **New SMB service on Linux.** Linux deployments use a new SMB service that mounts shares through the host's CIFS kernel module, so the host needs that module available. It supports custom SMB ports, reports wrong credentials and unreachable servers when you add the account, and reports a missing share path when you add the storage unit. Where the host cannot grant the service its mount privileges, you can switch back to the previous SMB service.
- **Target load per MetaDefender Core instance.** Each MetaDefender Core scan instance has a Desired load setting from 20 to 80 percent, 40 by default, editable in the UI and included in configuration export. Scanning is no longer capped by the message queue consumer limit, and when an instance set above 40 percent starts refusing work, the System tab recommends lowering it.
- **API key required for MetaDefender Core instances.** Adding or editing a MetaDefender Core scan instance now requires an API key. After an upgrade, workflows that use a scan pool with a keyless instance are flagged, cannot start new jobs, and keep a banner on screen until those instances have a key.
- **Clearer scan results in reports.** Report file tables now show the MDSS verdict, Allowed or Blocked, next to the result returned by the scan instance, so you can see why each file was allowed or blocked. The Remediations column shows the action that ran on each file.
- **Workflow details in Inventory.** Storage unit lists in Inventory can show the details of the workflow each unit's latest job ran with. Display options on Reports, Inventory and Accounts are grouped in sections you can select or clear at once, and the Reports page now opens with six columns by default instead of all of them.
- **External services on a dedicated host.** On Linux, `mdss -c start -e db,cache,queue` starts PostgreSQL, Redis and RabbitMQ on a separate host with generated credentials and prints the settings to paste into customer.env on the product host. Any subset of the three services can be selected.

#### **Improvements**

- **Faster, lighter storage integrations.** Most storage integrations now run inside the main services instead of in their own containers, so discovery, downloads and remediation skip a message broker round trip, and there are fewer containers to run and patch. NFS and SMB keep a small dedicated container.
- **Clearer System tab.** Informational recommendations no longer turn a healthy system amber, severity bands follow the reported severity, status lines are written in third person, and the tab marks its data as stale when health checks stop arriving. Product naming on the tab is corrected to MetaDefender Storage Security.
- **Syslog format notice.** The external logger settings state that only the logs sent to the external logger use the RFC 5424 format, while MDSS service and container logs keep their own format.
- **Platform component upgrades.** RabbitMQ is upgraded to 4.3.5 and Redis to 8.6.6, and on Windows, Garnet is upgraded to 1.1.10.

#### **Bug Fixes**

- **Upgrade from 4.2.0 no longer fails on credentials.** The account credential migration aborted the upgrade with a base64 decoding error when credentials were already in the current format, leaving the deployment unable to finish upgrading. The migration now completes, converts only credentials still in the old format, and can be repeated without error.
- **Windows upgrade no longer hangs for standard users.** Double-clicking the installer as a standard user on a machine with MDSS installed left the wizard on the preparing screen indefinitely. The installer now asks for administrator credentials right after launch and continues with the existing settings, including the configured ports.
- **Move and Copy remediation details kept after upgrade.** Upgrading from a version before 4.2.0 no longer resets the Move and Copy remediation details shown in job reports to Keep. Files were always moved and copied as configured.
- **NFS scans with inaccessible folders.** An on-demand scan of an NFS share containing a folder the service could not read completed with zero files. Inaccessible entries are now skipped and shown as a discovery warning in the report, and all accessible files are scanned.
- **Dropped uploads retried.** A file whose upload to a scan instance was interrupted no longer fails at once; the upload is retried, and a clear error is reported if the retry fails too.
- **Reprocessed files stay processed.** A failed file that was reprocessed successfully could be marked Failed again by the hourly stuck-file check, consuming its retry budget until reprocessing gave up. The check now measures from the retry, so a successful retry is left alone while a file that stalls is still caught.
- **Zero-byte files are remediated regardless of extension.** With Deep CDR enabled, an empty file whose extension was not .txt was recorded as a failed sanitization and its Move or Delete remediation was skipped, although MetaDefender Core had reported success. Empty files of every extension now follow the same path.
- **Storage errors no longer throttle scan instances.** Files that failed to read from storage no longer count as scan instance errors, and an instance that rejects its API key is taken out of the pool until the key works again.
- **Database disk on a separate filesystem is monitored.** When the Docker data root sat on its own volume, the database could fill it to 100 percent without processing being paused. MDSS now measures free space on the filesystem that holds the database, pauses at the same thresholds as for the machine disk, and the System tab names the database disk as the cause. Where the database role cannot run that check, a start-up warning points to the GUARDRAILS_PG_DISK_SIZE_BYTES setting.
- **Memory badge on the System tab.** A machine with enough RAM was shown as below the minimum memory spec whenever the CPU count was below spec, because one flag covered both cards. CPU and memory are judged separately, and the memory value is labelled GiB.
- **Storage and account edits locked during scans.** The web UI no longer lets you change a storage unit's source or its account's credentials while a scan is running on it.
- **Scan cleanup and scheduled jobs survive restarts.** Deleting an on-demand scan during a service restart no longer leaves its file records behind, and one failed scheduled job no longer stops the others in its batch.
- **KMS setting saved on Amazon S3 accounts.** Enabling KMS client-side encryption on an Amazon S3 account was not shown as enabled after saving. The setting and its secret name are now saved and shown, and the Secrets Manager and KMS service URLs are optional.
- **Deep CDR status for files deflected by OPSWAT Alin AI.** A file that OPSWAT Alin AI Deflection cleared before sanitization showed Deep CDR as "Unsupported file type" and went through the CDR unsupported remediation. It now shows sanitization as skipped and follows the normal Allowed or Blocked remediation.
- **Configuration import without storage units.** Importing a configuration with no storage units during first-time setup now completes the setup instead of leaving the wizard stuck.
- **Message broker disk alarm.** During a RabbitMQ disk or memory alarm, queue-depth checks leaked channels until the connection could open no more, which blinded the autoscaler and flooded the logs until a restart. Each service now logs the blocked connection once, keeps its channel count stable, and resumes probing when the alarm clears.
- **Garnet CPU usage on Windows.** The Garnet cache service on Windows could get stuck at 100 percent CPU after running for some time. Its thread pool is now capped, and upgrades apply the new setting.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
