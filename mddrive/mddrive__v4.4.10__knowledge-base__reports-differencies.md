<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/knowledge-base/reports-differencies -->

# Scan report differences when using MetaDefender Drive 64 GB vs MetaDefender Drive 2 1 TB

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [Overview](/docs/mddrive/v4.4.10/knowledge-base/reports-differencies#overview)

When running a Full Threat Scan on the **same endpoint** and **same disks**, you may see differences in the scan report when using:

- **MetaDefender Drive – 64 GB**

**MetaDefender Drive 2 – 1 TB**

Typical differences:

- The **1 TB Drive 2 finishes the scan faster**
- The **1 TB Drive 2 may process more data and/or show more findings**

This is an **environment‑specific behavior** and is not considered a regression.

#### [Why are the results different?](/docs/mddrive/v4.4.10/knowledge-base/reports-differencies#why-are-the-results-different)

The main reason is the **hardware difference** between the two drives:

1. **Drive 2 is faster**

   - MetaDefender Drive 2 (1 TB) uses **newer and faster flash chips and controller** than the older 64 GB drive.
   - MetaDefender Drive reads engine databases, configuration, and temporary data from the USB drive while scanning.
   - Because the 1 TB drive is faster, it can:

     - Read/write data more quickly
     - Stream files to the scanning engines more efficiently
   - Result: **shorter scan time** for the same machine and same selected disks.
2. **Drive 2 has larger storage capacity**

   - The 1 TB drive has **much more available space** than the 64 GB drive.
   - This allows:

     - More room for engines, signatures, and temporary scan data
     - Better support for **larger scans and log files** without running out of space
   - In some environments, this can mean **more data can be fully scanned and logged**, which may lead to:

     - More files processed
     - More detections visible in the final report
