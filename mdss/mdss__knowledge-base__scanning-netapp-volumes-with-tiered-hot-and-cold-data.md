<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/scanning-netapp-volumes-with-tiered-hot-and-cold-data -->

# Scanning NetApp Volumes with Tiered (Hot and Cold) data

**Applies to:** MetaDefender Storage Security protecting NetApp ONTAP volumes that tier inactive data: FabricPool on AFF and FAS systems, Amazon FSx for NetApp ONTAP, Azure NetApp Files with cool access, and Google Cloud NetApp Volumes with auto-tiering.

NetApp can move data that nobody has used for a while from fast SSD storage to cheaper object storage, and bring it back when it is used again. Before pointing MDSS at such a volume, customers usually ask three questions:

- Does scanning pull cold data back to the SSD tier?
- Does Real-Time Protection keep data hot, so that it never tiers?
- What does a scan cost on a volume that is mostly cold?

This article answers them, explains what happens behind the scenes, and walks through five examples.

---

## 1. The short answer

| Question | Answer |
| ---- | ---- |
| Does MDSS move data between tiers? | No. Only ONTAP moves data. MDSS reads files through SMB or NFS like any other client. |
| Does discovery or polling change anything? | No. Discovery reads only metadata (names, sizes, dates), and metadata always stays on the SSD tier. |
| Does scanning a file pull it back to the SSD tier? | Not with NetApp's default settings. MDSS reads each file once from start to end, which ONTAP treats like an antivirus or backup read: cold data is served from the object tier and stays cold. |
| Does scanning make data cold? | No. Only time without reads makes data cold. Reading a file that is still on SSD restarts its cooling clock. |
| What does a scan of cold data cost? | Time and, on cloud platforms, object-store reads. The object tier is slower than SSD, and cloud platforms bill the reads. |

One volume setting changes this picture: the **cloud retrieval policy**. If it is set to **On-read**, every file MDSS scans is written back to the SSD tier. See section 5.

---

## 2. How NetApp decides what is hot and what is cold

NetApp tracks temperature per 4 KB block, not per file.

1. When data is written, its blocks are **hot** and live on the SSD tier.
2. A background scan lowers the temperature of blocks that are not read: hot, then **warm**, then **cold**. A block becomes cold after the volume's **cooling period**: 31 days by default with the Auto policy, adjustable from 2 to 183 days.
3. Cold blocks are packed into 4 MB objects and moved to the object tier. The file keeps its name, size, dates and permissions. Users and applications see no difference, except that opening the file takes longer.
4. Reading a block that is still on SSD makes it hot again. What a read does to a cold block depends on how the file is read.

"Warm" is only a step on the way from hot to cold. There is no warm tier.

| What happens | Effect on temperature |
| ---- | ---- |
| A file is written or changed | Its changed blocks are hot |
| A file on SSD is read | Its blocks are hot again; cooling starts over |
| A cold file is opened and browsed by an application (random reads) | Its blocks come back to SSD and are hot (Auto policy) |
| A cold file is read once from start to end (backup, antivirus, indexing, MDSS) | Its blocks stay cold and are served from the object tier |
| A folder is listed or file properties are read | Nothing. Metadata never tiers |
| Nothing happens for the cooling period | Blocks go hot, warm, cold, then move to the object tier |

The same mechanism has a different name on each platform:

| Platform | Fast tier | Cold tier | Feature name |
| ---- | ---- | ---- | ---- |
| ONTAP on AFF and FAS | Local (performance) tier | Cloud tier: StorageGRID, S3, Azure Blob, Google Cloud Storage | FabricPool |
| Amazon FSx for NetApp ONTAP | SSD storage | Capacity pool | Data tiering |
| Azure NetApp Files | Hot tier | Cool tier | Cool access |
| Google Cloud NetApp Volumes | Hot tier | Cold tier | Auto-tiering |

Two volume settings matter for this article:

- **Tiering policy**: what may be tiered. *Auto* tiers cold user data and snapshots (the default in the FSx console). *Snapshot-only* tiers only snapshot blocks, so live files never go cold (the default from the FSx API and the ONTAP CLI). *All* tiers everything soon after it is written. *None* tiers nothing.
- **Cloud retrieval policy**: what a read of cold data does. *Default* follows the table above. *On-read* brings every block that is read back to SSD. *Never* brings nothing back. *Promote* brings the whole volume back.

---

## 3. What MDSS does on a tiered volume

MDSS does three things on a share. Only the last one reads file content.

**Discovery.** MDSS walks the folder tree and reads each file's name, size and timestamps. On NetApp this is metadata, served from SSD, and it changes nothing. Real-Time Protection in polling mode repeats this walk continuously, starting a new one as soon as the previous one finishes. A tiered file looks exactly like any other file during discovery; MDSS cannot tell hot files from cold ones.

**Filtering.** The workflow filters (file type, size, "Include files modified after") are applied to the discovered metadata. A file that is filtered out is never read.

**Scanning.** Each remaining file is downloaded once from start to end and sent to MetaDefender Core. This is the only step that touches data blocks, with the effects from section 2: blocks on SSD become hot again, cold blocks are read from the object tier and stay cold.

Which files reach the scanning step depends on the scan type:

| Scan type | Files that are read |
| ---- | ---- |
| On-demand and scheduled scans | Every file in scope that passes the workflow filters |
| Real-Time Protection, polling mode | Only files created or changed after the real-time start date. The start date is the moment Real-Time Protection was enabled, unless "Pick files modified since" was set |
| On-access scanning through the NetApp ONTAP integration (Vscan) | The file a user is opening or closing. The user is reading it anyway |

---

## 4. Examples

**Example 1: a user saves a new file; Real-Time Protection is in polling mode.** At 09:00 a user saves `Q3-report.xlsx` (2 MB) to the share. Its blocks are written to SSD and are hot. Within seconds MDSS lists the folder, sees a file with a new modification time, waits until the file stops changing, downloads it and sends it to MetaDefender Core. The file was already hot, so the read changes nothing. Every later polling cycle only lists the folder and never reads the file again. If nobody opens the file, ONTAP marks it cold after the cooling period and tiers it, exactly as if MDSS were not there.

**Example 2: an application appends to a large file that is mostly cold.** A 4 GB application log on the share has not been read for months and sits on the cold tier. Once a month the application appends about 50 MB. Those 50 MB are hot on SSD; the other 3.95 GB are still cold. MDSS sees the new modification time and downloads the whole file: 50 MB from SSD and 3.95 GB from the object tier. Afterwards the 50 MB are still hot and the 3.95 GB are still cold. The download took longer than it would from SSD, and nothing was written back.

**Example 3: first on-demand scan of a mostly cold volume.** A 20 TB volume uses the Auto tiering policy and the Default retrieval policy. 6 TB is hot and 14 TB is cold. MDSS lists the whole tree (metadata, from SSD), then reads every file: 6 TB from SSD and 14 TB from the object tier. After the scan the volume still holds 6 TB hot and 14 TB cold. The cooling clock of the 6 TB restarted, so files that were about to tier will tier a little later. Plan for the read speed of the object tier and, on FSx, Azure NetApp Files or Google Cloud, for the cost of reading 14 TB from it.

**Example 4: the same scan with the On-read retrieval policy.** Same volume, but the cloud retrieval policy is On-read. Now every cold block MDSS reads is written back to SSD, so the scan tries to bring 14 TB onto an SSD tier that holds 10 TB. On FSx, ONTAP stops bringing data back once the SSD tier is 90 percent full and stops all tiering at 98 percent. The scan still finishes, but the SSD tier is full and the volume is in a state nobody wanted. Set the retrieval policy back to Default before scanning a tiered volume.

**Example 5: Real-Time Protection enabled with an old "Pick files modified since" date.** Real-Time Protection is enabled on 1 October with "Pick files modified since" set to 1 January 2020. The first polling pass treats every file changed since 2020 as new and reads it, cold files included. This behaves like Example 3. Leave the field empty to protect only files that change from now on.

---

## 5. Recommendations

- **Keep the cloud retrieval policy at Default** (or Never) on volumes that MDSS scans. Do not use On-read or Promote on them.
- **Know how much is cold before the first full scan.** ONTAP's inactive data reporting, the FSx console and the Azure NetApp Files metrics show the size of the cold tier. Expect that part of the scan to run at object-tier speed and, on cloud platforms, to be billed as object-store reads.
- **Skip old files without reading them** with the workflow filter "Include files modified after". Filters work on metadata, so files outside the range are never downloaded. Files not modified within the cooling period are usually the cold ones.
- **Use Real-Time Protection for ongoing coverage.** It reads only files that change, and changed files are hot by definition.
- **Leave "Pick files modified since" empty** unless you need to catch up on a known period.
- **Keep SSD headroom.** AWS recommends keeping the FSx SSD tier under 80 percent. Normal user activity after a scan can still bring cold data back.
- **Run large first scans outside business hours.** Cold reads share the object tier's bandwidth with users who open cold files.

---

## 6. Frequently asked questions

**Does MDSS move files from cold to warm, or from warm to cold?** No. MDSS cannot move data between tiers and cannot see a file's temperature. Discovery and polling read metadata only. Scanning reads data, which makes SSD blocks hot and leaves cold blocks cold.

**Will scanning undo the savings from tiering?** No, with the Default or Never retrieval policy. Cold data stays cold. Only the On-read and Promote policies write data back.

**Does the polling cycle keep my data hot?** No. Listing folders and reading file properties does not touch data blocks.

**Can MDSS skip cold files?** Not by temperature, because SMB and NFS do not expose it. Use the "Include files modified after" filter instead; files not modified within the cooling period are usually the cold ones.

**Is the NetApp ONTAP (Vscan) integration different?** On-access scanning runs when a user opens or closes a file, so the data is being read anyway. On-demand scans through that integration read files the same way as an SMB share and follow this article.

**What about the All tiering policy?** New files move to the object tier soon after they are written, so even Real-Time Protection may read them from there. They are read from start to end and stay cold.

---

## Further reading

- NetApp, [FabricPool tiering policies](https://docs.netapp.com/us-en/ontap/fabricpool/tiering-policies-concept.html)
- NetApp, [TR-4598 FabricPool best practices](https://www.netapp.com/media/17239-tr4598.pdf)
- AWS, [Volume storage capacity and data tiering for FSx for ONTAP](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/volume-storage-capacity.html)
- Microsoft, [Azure NetApp Files storage with cool access](https://learn.microsoft.com/en-us/azure/azure-netapp-files/cool-access-introduction)
- Google, [Manage auto-tiering for Google Cloud NetApp Volumes](https://docs.cloud.google.com/netapp/volumes/docs/configure-and-use/volumes/manage-auto-tiering)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
