<!-- source: https://www.opswat.com/docs/mdss/operations/cross-domain-transfer--data-diode -->

# Cross-Domain Transfer (Data Diode)

Move files across a one-way security boundary using MetaDefender Storage Security on both sides of an OPSWAT NetWall diode. The diode transfers files over SMB; MDSS accesses each SMB share by mounting it as an NFS storage unit.

## [Overview](/docs/mdss/operations/cross-domain-transfer--data-diode#overview)

A data diode enforces one-way data flow: traffic goes from the low side (source) to the high side (destination) and never back. This physical isolation is why diodes protect critical environments — there is no return path, and no delivery acknowledgement.

## [How It Works (Concepts & Architecture)](/docs/mdss/operations/cross-domain-transfer--data-diode#how-it-works-concepts--architecture)

The architecture is symmetric. The diode owns the cross-boundary mechanics over SMB; MDSS reads and writes its share through an NFS mount of that same SMB share. Complete flow:

1. Low-side MDSS pulls from a source storage (SharePoint, S3, or any integrated storage), scans/remediates, and writes approved files to the low-side share.
2. The NetWall diode polls that share over SMB, transmits each file across the optical link, and writes it to the high-side share.
3. High-side MDSS reads the high-side share, scans/remediates, and forwards files to the destination.

The diode is the SMB client on both sides and owns all cross-boundary mechanics: polling, transfer, and cleanup. MDSS only writes to the low-side share and reads from the high-side share, treating each as an ordinary NFS storage unit.

### [SMB vs FTP](/docs/mdss/operations/cross-domain-transfer--data-diode#smb-vs-ftp)

**SMB is recommended.** It multiplexes transfers, sustains higher bandwidth, and has sub-second timestamps that MDSS uses to detect when a file is fully written. NetWall's native FTP transport is supported but under increased concurrent load the FTP channel resets without self-recovery.

## [Requirements](/docs/mdss/operations/cross-domain-transfer--data-diode#requirements)

- An OPSWAT NetWall diode configured for native SMB file transfer. Set up the share on the diode per the [NetWall Windows file share guide](https://www.opswat.com/docs/netwalldiode/v1.5.0/configuration/diode-filetransfer#windows-file-share).
- Two SMB shares, one per side, reachable by the diode and the local MDSS host. Any standards-compliant SMB server works (e.g. Samba).
- Two MDSS instances, one per side, see [Planning your deployment](https://www.opswat.com/docs/mdss/getting-started/planning-your-deployment). Low-side MDSS reaches the source storage; high-side MDSS reaches the destination.

The diode speaks SMB, but MDSS connects to each share as an NFS storage unit: mount the SMB share on the MDSS host, then add it to MDSS as NFS. Do this on both sides:

- [Add an SMB share as an NFS storage unit (Windows deployment)](https://www.opswat.com/docs/mdss/integrations/windows-deployment--how-to-add-a-smb-share-as-a-nfs-storage-unit)
- [Add an SMB share as an NFS storage](https://www.opswat.com/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage)

Throughput is bounded by the diode license tier (e.g. 100 Mbps; gigabit raises file transfer to 500 Mbps) and by disk I/O on the shares.

## [Set Up the Low Side (Sender)](/docs/mdss/operations/cross-domain-transfer--data-diode#set-up-the-low-side-sender)

1. Mount the SMB share into low-side MDSS and add it as a NFS storage unit (see [Requirements](/docs/mdss/operations/cross-domain-transfer--data-diode#requirements)).
2. Create a workflow whose copy or move destination is that storage unit.
3. Start a scan on the desired storage unit with that workflow. Files are written to the share, and the diode polls them automatically.

## [Set Up the High Side (Receiver)](/docs/mdss/operations/cross-domain-transfer--data-diode#set-up-the-high-side-receiver)

1. Mount the SMB share into high-side MDSS as an NFS storage unit (see [Requirements](/docs/mdss/operations/cross-domain-transfer--data-diode#requirements)).
2. Set the discovery debounce environment variable so MDSS never scans a file the diode is still writing; it skips any file modified within the window:`NFS_DISCOVERY_DEBOUNCE_TIME_SECONDS=30` 30s suits typical files; raise it for large files that take longer to cross the link.
3. Create a workflow whose copy or move destination is your target storage (e.g. SharePoint)
4. Start a real-time (RTP) scan on the storage unit with that workflow. As the diode writes files in, MDSS discovers, scans, and forwards them.

## [Monitor](/docs/mdss/operations/cross-domain-transfer--data-diode#monitor)

- MDSS surfaces progress only for running scans, the low-side scans and the high-side RTP scan, from the UI.
- Use the diode's own monitoring for transfer status, queue depth, and channel health across the link.
- There is no delivery acknowledgement back to the low side. End-to-end reconciliation means comparing source vs. destination inventories.

## [Troubleshooting](/docs/mdss/operations/cross-domain-transfer--data-diode#troubleshooting)

**Files get scanned mid-write, or scans come back partial.** MDSS picked up a file before the diode finished writing it. Bump `NFS_DISCOVERY_DEBOUNCE_TIME_SECONDS` past how long your biggest file takes to cross.

**Transfers die after the first 10–15 files.** This shows up on old SMB servers (Samba 4.12.x). Upgrade to a modern version, if it is not an option, turning off oplocks and leases helps but the real fix is the newer server.

**Low-side share keeps filling up.** The diode is supposed to delete each file once it's across. If files pile up, check that its account can actually delete on the share and that it's still polling.

**Files vanish under heavy load.** When the destination can't keep up with the incoming rate, the high-side diode buffers to disk. Once that buffer is full, new files are dropped — silently, because a diode has no way to tell the sender to slow down. Give the destination enough headroom, cap per-file size, and split very large files on the source side.

## [Limitations](/docs/mdss/operations/cross-domain-transfer--data-diode#limitations)

- **No delivery confirmation.** A diode has no return channel, so a full high-side buffer drops files silently. Size the destination and diode disk for peak load.
- **Retransmit on HA failover.** NetWall supports active/standby HA, but if the active high-side node fails with files still buffered, those files are lost and must be re-sent from the source today a manual reprocess. Plan source-side retention.
- **FTP is supported but not recommended.** channel resets under concurrent load and timestamps are minute-resolution. Use SMB.
