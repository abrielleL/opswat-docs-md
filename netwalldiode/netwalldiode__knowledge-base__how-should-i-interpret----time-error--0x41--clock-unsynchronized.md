<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/how-should-i-interpret----time-error--0x41--clock-unsynchronized -->

# How should I interpret “TIME_ERROR: 0x41: Clock Unsynchronized” on an Optical Diode, and what should I do about it?

This article applies to MetaDefender Optical Diode / NetWall Diode.

### [What the message means](/docs/netwalldiode/knowledge-base/how-should-i-interpret----time-error--0x41--clock-unsynchronized#what-the-message-means)

`kernel reports TIME_ERROR: 0x41: Clock Unsynchronized` indicates the system time is reporting that the clock is **not currently synchronized** to a valid upstream time source (i.e., NTP has not locked yet or lost sync). The underlying `TIME_ERROR` status is commonly described as “clock not synchronized.”

---

### [Is it critical?](/docs/netwalldiode/knowledge-base/how-should-i-interpret----time-error--0x41--clock-unsynchronized#is-it-critical)

In most real deployments, this is **not automatically a critical fault**:

- It is frequently seen **during NTP startup or early convergence** (especially right after boot/service restart). In that situation it is typically **warning/informational**.
- It becomes an operational concern if it is **persistent** (repeating continuously over long periods), because time drift impacts log/audit accuracy and troubleshooting correlation (even if file transfer still works).

**Practical guidance:** if the message is **rare/transient**, it is unlikely to be the root cause of intermittent transfer failures by itself; still, it should be corrected as a best practice.

---

### [Why we still recommend fixing it](/docs/netwalldiode/knowledge-base/how-should-i-interpret----time-error--0x41--clock-unsynchronized#why-we-still-recommend-fixing-it)

Even when it is not the direct cause of your transfer issue, time sync is important because:

- It improves **cross-node correlation** (BLUE vs RED events line up reliably).
- It reduces confusion during incident analysis and support escalation.

OPSWAT’s documentation explicitly supports configuring time and notes that **manual time setting triggers a reboot on both BLUE and RED**, which makes stable NTP configuration the preferred approach.

---

### [Recommended remediation](/docs/netwalldiode/knowledge-base/how-should-i-interpret----time-error--0x41--clock-unsynchronized#recommended-remediation)

#### [Preferred: Configure NTP (recommended)](/docs/netwalldiode/knowledge-base/how-should-i-interpret----time-error--0x41--clock-unsynchronized#preferred-configure-ntp-recommended)

1. Configure **reachable NTP servers** appropriate for each zone (BLUE and RED may need different NTP sources depending on segmentation).
2. Verify the node reaches a synchronized state (message stops recurring after convergence).

#### [Fallback: Manual time (only when NTP is impossible)](/docs/netwalldiode/knowledge-base/how-should-i-interpret----time-error--0x41--clock-unsynchronized#fallback-manual-time-only-when-ntp-is-impossible)

- Use manual time only if NTP is not feasible.
- Plan a maintenance window: OPSWAT documents that **setting time manually will reboot both BLUE and RED nodes**.

Info

Since version v1.13.0, MetaDefender Optical Diode supports the transfer of NTP from Blue to Red. The function is called "NTP Forwarding" and it can be activated in settings.

---

### [How to confirm it’s “transient” vs “persistent”](/docs/netwalldiode/knowledge-base/how-should-i-interpret----time-error--0x41--clock-unsynchronized#how-to-confirm-its-transient-vs-persistent)

- **Transient:** a few occurrences around boot or service restart, then quiet. This aligns with “normal during startup.”
- **Persistent:** repeated occurrences over extended time → investigate NTP reachability, NTP server IPs, firewall rules to NTP sources, and whether a time service is being stopped/restarted.

Info

If Further Assistance is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).

MetaDefender
