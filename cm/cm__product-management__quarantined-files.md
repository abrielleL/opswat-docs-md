<!-- source: https://www.opswat.com/docs/cm/product-management/quarantined-files -->

# Quarantined Files

Quarantined Files in My OPSWAT Central Management gives you one list of every file your MetaDefender Core instances have quarantined, across your whole Core fleet. From that list, you can:

- **Retrieve** a quarantined file as a password-protected ZIP archive, without signing in to the Core instance or opening a network path to it.
- **Protect** a file so automatic cleanup doesn't remove it.
- **Delete** files you no longer need.

Note This feature requires** MetaDefender Core version 5.23 or later**.

![](https://uploads.developerhub.io/prod/97qW/17v4lb4obqnryx5weirijj4eu6fsjkk610rzpoe0bv2v5nwcn43bcsjtmfrals3f.png)

- [Retrieve a Quarantined File](https://www.opswat.com/docs/cm/product-management/quarantined-files#retrieve-a-quarantined-file)
- [Protect a Quarantined File](https://www.opswat.com/docs/cm/product-management/quarantined-files#protect-a-quarantined-file)
- [Acting on Multiple Files At Once](https://www.opswat.com/docs/cm/product-management/quarantined-files#acting-on-multiple-files-at-once)
- [How Changes Reach the Core Instance](https://www.opswat.com/docs/cm/product-management/quarantined-files#how-changes-reach-the-core-instance)
- [How Long Quarantined Files Are Kept](https://www.opswat.com/docs/cm/product-management/quarantined-files#how-long-quarantined-files-are-kept)

## Prerequisites

| Requirements | Details |
| ---- | ---- |
| Supported Products | Supported for **MetaDefender Core** instances only. Other products (ICAP, MFT, Storage Security, Email Gateway Security, Sandbox) are not covered. |
| Supported Deployment | - Supported on every deployment model: **Cloud**, **Windows (MSI)**, **Linux (RPM)**, **OVA appliance**, and **High Availability**. - Supported for air-gapped on-premises environments: The Core instance delivers the file over its own connection to My OPSWAT Central Management, so no internet access is needed. |
| User Role Permission | - Quarantined Files has no permission of its own yet, so any user can protect, unprotect, and delete quarantined files within their inventory groups, regardless of their File Processing History role level. - My OPSWAT Central Management can be configured, per deployment, so that only Administrators can retrieve files. This restriction is off by default. It affects retrieval only; listing, protecting and deleting are unaffected. Note A dedicated Quarantined Files permission is planned for a later release. |
| Connected Core Instance | The Core instance must be connected to My OPSWAT Central Management to retrieve, protect, unprotect, or delete a file. |
| Archive Password for Retrieval | A retrieved file is always delivered inside a ZIP archive locked with a password **you** choose when you retrieve it. The password must: - be **1 to 64 characters** long, and - use only standard printable ASCII characters: English letters, digits, spaces, and common symbols. Accented letters and other non-ASCII characters aren't accepted, because they can make the archive fail to open in Windows Explorer. |

## Open Quarantined Files Page

1. In the left navigation, select **File Security** > **Quarantined Files**
2. Use Search by function or scroll the list to find the files. You can narrow the list using Filter or Timeframe.

Tip Can't find a file you expected? Check the timeframe first. For other common reasons, see [Troubleshooting](https://www.opswat.com/docs/cm/product-management/quarantined-files#troubleshooting).

![](https://uploads.developerhub.io/prod/97qW/ebphux9xznqx2hm6sg68lrnftuxs6vgk5ye3e2a6m4zg4n33wtcpoe4emg72zn3e.png)

| Columns | Details |
| ---- | ---- |
| **File Name** | The name of the quarantined file. Always shown. |
| **Protected** | Whether the file is protected from automatic cleanup. You can switch it on or off here. |
| **Source** | The IP address of the client that submitted the file for scanning. `::1` means the file was submitted from the Core host itself. |
| **SHA256** | The file's hash, shortened. Hover to see the full value, or select the copy icon. |
| **Processed By** | The Core instance that holds the file, by its current name. Always shown. |
| **Date Added** | When the file was first quarantined on that instance. Select the column header to switch between newest and oldest first. |

Please Note N/A means no value. For example, Source shows N/A when the Core instance didn't report it.

## View Quarantined File's Details

1. Select a row. The **File Details** panel opens on the right.
2. The panel shows: File name, Source, SHA256, Date added, and **Processing result** link (shown only when the original scan record is still available)

![](https://uploads.developerhub.io/prod/97qW/r89jpbn58itjw9ghdo3phfdjc6gc0fv67opzi85gbnkksg893eedzc88eripe9j2.png)

## Retrieve a Quarantined File

From the left menu, navigate to **File Security > Quarantined Files**

1. In the file's row, select **⋮** > **Save with Password**
2. In **Password**, enter a password for the archive
3. Select **Start Encryption**
4. Choose a folder to save the archive
5. Wait for the transfer to finish. Don't reload or close the browser tab until it finishes.
6. When the dialog shows **Saved**, select **Close. **
7. Verify success**,** open the archive with any ZIP tool, including Windows Explorer, using the password you set.

![](https://uploads.developerhub.io/prod/97qW/vqw44o1g65u7y5gn6a7clohr0gsxgtbggqev4fffs8qr5vcrm36qrdsugi0qzy4t.png)

Warning The retrieved file is still potentially malicious. Open the archive only in an environment set up for handling malware.

## Protect a Quarantined File

Protecting a file keeps it from being removed by automatic cleanup. The file is also marked as protected on the Core instance that holds it.

From the left menu, navigate to **File Security > Quarantined Files**

You can protect or unprotect a file in any of these ways:

| Navigation | Details |
| ---- | ---- |
| Switch Protected toggle on or off, then confirm | ![](https://uploads.developerhub.io/prod/97qW/lhd0lkpta1xuykn9ynuzj0mvawfflodocbnhonuakyf51uuxapxs379uoftk5sjt.png) |
| Select **⋮**, choose **Protect** or **Unprotect**, then confirm. | ![](https://uploads.developerhub.io/prod/97qW/tipdbdo7caf9mtuxkoo7ax9danqu2ys3h2a7nlbuzxdhcf6uqwa2hfyoyij0v1qt.png) |
| **From File Details:** switch **Protected**, then select **Save** | ![](https://uploads.developerhub.io/prod/97qW/pb2a6p5onzyhsp3o1arq0nuzfsw2o8sko4o86phmbpq002xw1ozrquqt098amqw8.png) |

## Delete a Quarantined File

Warning Deleting removes the file **from the Core instance's quarantine and from My OPSWAT Central Management**. It can't be undone.

From the left menu, navigate to **File Security > Quarantined Files**

1. In the file's row, select **⋮** > **Delete**.
2. The confirmation names the file. Check that it's the one you mean, then confirm.

![](https://uploads.developerhub.io/prod/97qW/7bhdngmjid08k9db2epvalfn1fls7yjm1i2smhmom4xyl9mmzepa6mbolzzm74f5.png)

## Act on Multiple Files At Once

1. Select the checkbox next to each file you want. To select the whole page, select the header checkbox
2. In **Select Action**, choose **Protect**, **Unprotect**, or **Delete**
3. Confirm

![](https://uploads.developerhub.io/prod/97qW/nt1rjytzspug0rlt1nqcalveyo26djxl3dnhvngy8z9xjg98f4ksz24qbf7xwn2x.png)

What to expect:

- You can act on up to **50 files** at a time.
- Each file is handled on its own.
- If some succeed and others fail, a summary shows how many succeeded and lists each file that failed, with the reason.
- Retrieval isn't available for several files at once. Retrieve files one at a time.

> **Event Logs**
>
> Every retrieval, protect, unprotect, and delete is recorded under **Logs > Admin Events**, with who did it, when, and the Core instance involved.
>
> A forced change is recorded as forced. Use these records to review activity for compliance or troubleshooting.

## How Changes Reach the Core Instance

Protect, unprotect, and delete are carried out **on the Core instance first**. My OPSWAT Central Management saves the change only after the instance confirms it. Here's what happens in each case:

| What the Core instance does | What happens | What you can do |
| ---- | ---- | ---- |
| Confirms the change | The change is made on both the Core instance and My OPSWAT Central Management | Nothing further |
| Refuses the change | Nothing changes in My OPSWAT Central Management | Select **Refresh** to see the file's current state |
| Refuses a protect or unprotect because it no longer holds the file | Nothing changes yet | Force the change, so an entry whose file is already gone from the instance can still be unprotected and cleaned up. (A **delete** in this situation succeeds on its own) |
| Doesn't answer, not connected, timed out, unreachable, or running a version that doesn't support the action | It's **not known** whether the change took effect. A dialog lists the affected files with the reason for each. Its **Enforce** column shows which files can be forced | Select **Force Protect**, **Force Unprotect**, or **Force Delete**, or select **OK** to leave the files unchanged |

Note A forced change updates **My OPSWAT Central Management only**. It doesn't contact the Core instance, so the two may disagree afterward. For example, a force-deleted file may still exist on the instance.

## How Long Quarantined Files Are Kept

**In My OPSWAT Central Management**

- The quarantine list is kept **separately from scan records**, so a file stays listed after its scan record has been cleaned up.
- The list is cleaned up on a schedule that follows your account's **data retention** setting. See [Data Storage](https://www.opswat.com/docs/cm/configurations/global-settings#endpoint-data) for more details.
- **Protected** files are never removed by this cleanup.
- This cleanup removes only the entry in My OPSWAT Central Management. It **never deletes the file on the Core instance**.

**On the Core instance**

- The Core instance applies its own quarantine retention, which My OPSWAT Central Management doesn't change.
- As a result, a listed file can occasionally be gone from the instance. Retrieving it then reports that the file is no longer stored. You can delete the out-of-date entry.

## Security

- **Your archive password stays private.** Central Management never generates, stores, or logs the archive password. The password is encrypted specifically for the target Core instance the moment you submit it, so only that instance can read it.
- **Files never arrive unprotected.** A retrieved file always arrives inside a password-protected archive, never as a bare file. It's still potentially malicious: open it only in an environment meant for handling malware.
- **Access follows your inventory groups.** In this release, your role's permissions don't restrict Quarantined Files; only the inventory groups the role permits do. Files on instances outside your groups aren't shown and can't be reached through a link.

## Troubleshooting

| Issues | Resolution |
| ---- | ---- |
| A file I expect isn't listed | A missing file is usually expected. Check these in order: 1. **Timeframe.** The list shows the last 7 days until you change the **Timeframe**. 2. **Inventory groups.** Files on Core instances outside your inventory groups are never listed. 3. **Scan type.** Files from batch scans are never listed. 4. **Core version.** Files from Core instances earlier than 5.23 are never listed. Look for them in **File Processing History**. 5. **Quarantine date.** Files quarantined before the feature was deployed are never listed. 6. **Product.** Files quarantined by products other than MetaDefender Core are never listed. |
| Save with Password is greyed out | Read the reason shown under the action. For example, the Core instance may not have finished quarantining the file. Actions are also unavailable while that file is transferring. |
| A retrieval request is refused or has to wait | The Core instance may have reached its limit of 2 simultaneous retrievals or about 20 requests per minute. Wait, then try again. |
| The transfer stopped before finishing | The browser tab was probably closed or reloaded. There's no resume; start the retrieval again from the beginning. |
| I forgot the archive password | The password can't be recovered. Retrieve the file again with a new password. |
| Retrieval says the file is no longer stored | The Core instance's own retention removed the file. Delete the out-of-date entry. |
| A protect, unprotect, or delete didn't take effect | The Core instance refused or didn't answer. See [How Changes Reach the Core Instance](https://www.opswat.com/docs/cm/product-management/quarantined-files#how-changes-reach-the-core-instance) |

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
