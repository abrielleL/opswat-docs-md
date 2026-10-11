<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/how-to-troubleshoot-slow-historical-data-retrieval-from-the-avev -->

# How to troubleshoot slow historical data retrieval from the AVEVA PI Server?

> **Check Your Version:** This article applies to MetaDefender NetWall used with the OPSWAT PI Connector.

## **Issue**

Historical data transfer from the Blue side to the Red side is slower than expected. Symptoms include delayed backfill of historical values, slow snapshot updates, and general performance degradation that becomes more noticeable under higher load or during large backfill operations.

## **Possible Causes**

This issue may occur in either of the following situations:

- The AVEVA PI Data Archive on the Red side is taking longer than expected to process historical-data requests. The Red Flanker measures this time but does not control it.
- The PI Buffer Subsystem is not enabled on the Red Flanker, so writes to the destination PI Server are not buffered.

Retrieval time is measured from the moment the Red Flanker issues the AVEVA PI AF SDK call `PIPoint.RecordedValues()` until the call returns. This call retrieves historical data from the PI Data Archive. If the call itself is slow, the delay is occurring inside the PI Data Archive, not in the OPSWAT components.

## **Troubleshooting Steps**

### **1. Enable the PI Buffer Subsystem on the Red Flanker**

Confirm that the PI Buffer Subsystem is enabled on the Red Flanker node. Buffering allows writes to the destination PI Server to be queued rather than blocking on each write, and is required for the reference performance figures below to apply.

### **2. Collect the PiHistoryStore statistics**

The `PiHistoryStore` statistics are generated once per minute and recorded in both syslog and the Windows Event Log on the Red Flanker. Collect several consecutive samples covering a period when the slowness is observed.

The following sample is from an OPSWAT reference environment and is shown here as a **healthy baseline**, not as an example of the problem:

> 09:26:28.67  PI_STATS 3460-pi HistoryStoresTotal 18082
>
> 09:26:28.67  PI_STATS 3460-pi HistoryStoresPerSecond 0.0
>
> 09:26:28.67  PI_STATS 3460-pi Last History Store Time 7/28/2026 9:22:30 AM
>
> 09:26:28.67  PI_STATS 3460-pi Collective Main Connection Status: Primary
>
> 09:26:28.67  PI_STATS 3460-pi PiHistoryStore(09:25:53) 3460-pi Blocks:12116 Fetches:12115 elapsed 13.01secs, Red Fetch longest:11ms, avg:1.07ms, total:12.96secs, BlueSort 1ms
>
> 09:26:28.67  PI_STATS 3460-pi PiHistoryStore(09:25:53) longest red fetch length:84 avg:28.37 # of values fetched:343672 Total Blue Values:343672

In this sample:

- 12,116 history blocks containing 343,672 values were transferred from the Blue side to the Red side.
- The Red Flanker performed 12,115 historical-data reads and retrieved 343,672 values.
- The longest individual read took 11 milliseconds; the average read took 1.07 milliseconds.
- The reads consumed 12.96 seconds of read time within a 13.01 second sampling interval.
- Each read returned an average of 28.37 values, and the largest returned 84 values.

### **3. Compare your figures against the reference baseline**

| Metric | Reference environment | Indicates slow PI Data Archive response |
| ---- | ---- | ---- |
| Average read time (`avg`) | ~1 ms | Tens of milliseconds — for example, ~42 ms |
| Longest read time (`longest`) | ~11 ms | Consistently above ~50 ms |
| Average values per read (`avg` length) | ~28 values | Higher averages increase per-read cost |

An average read time in the tens of milliseconds against a reference of roughly 1 millisecond means the PI Data Archive is taking substantially longer to satisfy each request. Larger average read lengths also raise the cost of each individual read, so consider both figures together.

### **4. Tuning Historical Backfill for best results**

If the comparison in step #3 looks good, please refer to the following documentation for guidance on tuning the configuration to optimize performance:[Optimizing AVEVA Pi Historical Backfill - MetaDefender Optical Diode](https://www.opswat.com/docs/netwalldiode/optimizing-aveva-pi-historical-backl/optimizing-aveva-pi-historical-backl#potential-historical-data-issues-when-using-diodes)

### **5. Escalate to AVEVA with supporting evidence (If Needed)**

If the `PIPoint.RecordedValues()` call consistently takes significantly longer than the reference results, open a support case with AVEVA and provide:

- PI Server logs covering the same period
- Red Flanker event logs covering the same period

AVEVA Support can determine why historical-data retrieval is taking longer than expected.

## **Reference Environment**

The reference figures above were produced in an OPSWAT environment with the following characteristics:

- The PI System contains approximately 264,000 tags.
- Two physical computers connected through a 1 Gbps network.
- One computer runs the OPSWAT Red Flanker and acts as the PI API node.
- The other computer runs the PI Server.
- The PI Buffer Subsystem is enabled.

## **Recommendation**

Capture `PiHistoryStore` statistics routinely rather than only during an incident, so a healthy baseline for your own environment is available for comparison.

> **Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
