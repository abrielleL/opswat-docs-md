<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-do-core-instances-fluctuate-between--operational--and--signi -->

# Why do Core instances fluctuate between "Operational" and "Significant Issues" status in on-prem Central Management?

> Check version:
> MetaDefender Core, Central Management 10 

> **Issue summary:** MetaDefender Core instances enrolled in Central Management (CM10) may repeatedly switch between Operational and Significant Issues even when basic connectivity is healthy.

This page explains the likely cause of this behavior, how to recognize it, and the recommended configuration change to reduce false health-state transitions.

# When this happens

- The same Core instance alternates between healthy and warning status at short intervals.
- Scan processing continues normally and the instance remains reachable.
- Network tests show stable connectivity and acceptable latency between MetaDefender Core and CM10.

# Why the status changes

MetaDefender Core periodically validates configuration state with Central Management by requesting configuration hash information. If CM10 is under heavier load, these requests can take longer to complete.

When the response does not arrive within the expected timeout window, Core may temporarily mark the instance as Significant Issues. After the validation succeeds, the status returns to Operational.

> **Typical trigger:** This is often a timing and load issue rather than a direct network failure.

# Common load conditions behind the delay

- A large number of enrolled Core instances reporting to the same CM10 environment
- Frequent configuration synchronization activity
- Ongoing report storage and repeated configuration pushes

# Recommended resolution

Reduce synchronization pressure on CM10 by increasing the polling interval on MetaDefender Core.

1. Open the **MetaDefender Core** management console.
2. Go to **Settings** > **Central Management**.
3. Find the section labeled **Product status, actions and data are sent to My OPSWAT Central Management**.
4. Locate the synchronization interval setting.
5. Increase the interval from a more aggressive value such as **15 seconds** to a less frequent value such as **60 seconds**.
6. Save and apply the change.

> **Expected result:** After reducing polling frequency and allowing CM10 load to normalize, affected Core instances should maintain a more stable Operational state.

# Quick diagnosis guide

| Observation | What it suggests | Recommended next step |
| ---- | ---- | ---- |
| Status flips repeatedly but scans continue normally | Likely delayed CM10 validation response rather than service interruption | Review and increase the CM synchronization interval |
| Connectivity and latency checks are healthy | Network path is probably not the main cause | Focus on CM10 load and synchronization frequency |
| Issue appears during periods of high management activity | CM10 may be responding too slowly to validation requests | Reduce polling pressure and monitor status stability |

# Support

> If the issue continues after increasing the polling interval, open a support case with [https://support.opswat.com](https://support.opswat.com).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
