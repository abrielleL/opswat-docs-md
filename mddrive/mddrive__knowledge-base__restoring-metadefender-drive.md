<!-- source: https://www.opswat.com/docs/mddrive/knowledge-base/restoring-metadefender-drive -->

# MetaDefender Drive Fails to Boot

## [Issue](/docs/mddrive/knowledge-base/restoring-metadefender-drive#issue)

MetaDefender Drive fails to boot, and/or the operating system detects it as a corrupted storage partition.

## [Solution](/docs/mddrive/knowledge-base/restoring-metadefender-drive#solution)

To recover a possibly corrupted MetaDefender Drive, try the following methods in order.

### [1. Using MetaDefender Drive Toolkit](/docs/mddrive/knowledge-base/restoring-metadefender-drive#1-using-metadefender-drive-toolkit)

**If you can't boot your MetaDefender Drive or you do not have access to the internet:** Follow the instructions to [create and flash a drive using MetaDefender Drive Toolkit](https://www.opswat.com/docs/mddrive/getting-started/create-drive).

**If you can boot your MetaDefender Drive with internet access:** Check if an update is available for the Drive software by going to **Settings** → **Update** and clicking **Check for Updates**.

### [2. Wipe the Drive with Windows Disk Management or diskpart, then restore with the Toolkit](/docs/mddrive/knowledge-base/restoring-metadefender-drive#2-wipe-the-drive-with-windows-disk-management-or-diskpart-then-restore-with-the-toolkit)

If the issue wasn't resolved using MetaDefender Drive Toolkit, the MetaDefender Drive's partition table is likely corrupted, which can prevent the Toolkit from detecting or writing to it. Wiping the Drive's partitions with the built-in Windows tools clears the corruption so the Toolkit can recreate the Drive. Use one of the two well-understood Windows tools below, then re-run the Toolkit.

> **Warning — this erases all data on the Drive**
>
> Wiping removes **all** data on the MetaDefender Drive, including scan reports, configuration, and any stored files. **Save anything you need off the Drive first.** Make sure you select the MetaDefender Drive and **not** another disk — selecting the wrong disk will erase that disk.

**Before you begin:**

- Copy any reports or other data you want to keep from the MetaDefender Drive to another location.
- Unplug other external/USB drives so you don't accidentally select the wrong disk.
- Insert the MetaDefender Drive and note its **capacity** so you can identify it in the steps below.

#### [Option A — Windows Disk Management (graphical)](/docs/mddrive/knowledge-base/restoring-metadefender-drive#option-a--windows-disk-management-graphical)

1. Right-click the **Start** button and choose **Disk Management** (or press **Win + R**, type `diskmgmt.msc`, and press **Enter**).
2. In the lower pane, locate the MetaDefender Drive. Identify it by its **capacity** and its **Removable** type — do not use your system disk.
3. Locate the partition names **MetaDefender Drive**, right-click it and choose **Delete Volume**. You can also repeat until the entire disk shows a single block of **Unallocated** space, but it is not necessary.
4. Leave the space **Unallocated** — do **not** create a new simple volume. Close Disk Management.
5. Restore the Drive using the Toolkit (see **Method 1**).

> **Note**
>
> If **Delete Volume** is grayed out for a partition (for example, a protected or recovery partition), use **Option B (diskpart)** instead, which removes the partition table directly.

#### [Option B — diskpart (command line — removes the partition table)](/docs/mddrive/knowledge-base/restoring-metadefender-drive#option-b--diskpart-command-line--removes-the-partition-table)

Use this option if Disk Management cannot delete one of the partitions. Here is the screenshot of illustrating the method. Detail commands are below.

1. Press **Start**, type `cmd`, right-click **Command Prompt**, and choose **Run as administrator**.
2. Start diskpart:

   diskpart
3. List the disks and find the MetaDefender Drive by its **Size**:

   list disk
4. Select the MetaDefender Drive, replacing `N` with its disk number. **Double-check the number before continuing:**

   select disk N
5. Confirm you selected the correct device before wiping it:

   detail disk
6. Remove the partition table and all partitions:

   clean
   > Use `clean` (fast — removes the partition table). Do **not** use `clean all` unless you intend a full, multi-hour zero-wipe of every sector.
7. Exit diskpart:

   exit
8. Restore the Drive using the Toolkit (see **Method 1**).

After the Drive is wiped, repeat **Method 1 (MetaDefender Drive Toolkit)** to recreate and flash the Drive image so it becomes bootable again. If the Toolkit still cannot detect the Drive after wiping, see [Toolkit Fails to Detect Some Drives](https://www.opswat.com/docs/mddrive/knowledge-base/failed-to-detect-or-interact-with-drives).
