<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/why-don---t-the-metadefender-optical-diode-interfaces--diode1--a -->

# Why don’t the MetaDefender Optical Diode interfaces "diode1" and "diode2" show TX/RX statistics?

This article applies to MetaDefender Optical Diode.

### [Symptom / Question](/docs/netwalldiode/v1.14.0/knowledge-base/why-don---t-the-metadefender-optical-diode-interfaces--diode1--a#symptom--question)

In the **Optical Diode management UI**, the interfaces `diode1` (transmit) and `diode2` (receive) appear under **Advanced → Networking → Interfaces**, but:

- They **do not display TX/RX packet or byte counters**
- Administrators want to know whether this is expected and whether the optical channel exposes any traffic statistics (throughput, frames, signal metrics, etc.)

---

### [Short answer](/docs/netwalldiode/v1.14.0/knowledge-base/why-don---t-the-metadefender-optical-diode-interfaces--diode1--a#short-answer)

- **Yes, it is expected** that `diode1` and `diode2` do **not** show per-interface TX/RX counters.
- The optical link is a **hardware-enforced, one-way, non-routable channel**, and its internal packet-level statistics are **not exposed in the UI**.
- Monitoring is intended to be done at **higher layers** (streams, file transfers, system performance counters, SNMP/PI tags), not at the raw optical interface level.

---

### [Why there are no TX/RX counters on `diode1` / `diode2`](/docs/netwalldiode/v1.14.0/knowledge-base/why-don---t-the-metadefender-optical-diode-interfaces--diode1--a#why-there-are-no-txrx-counters-on-diode1--diode2)

1. **Unidirectional, non-routable design** MetaDefender Optical Diode connects the BLUE (source) and RED (destination) zones using a **single optical fiber** that carries data in a **non-routable, one-way protocol**.

   - Data flows only from BLUE to RED.
   - No MAC or IP information is exchanged across the optical channel.

This design is central to the security model and is explicitly described in product documentation and datasheets.

2. **Optical link is not treated as a normal NIC** The **Advanced → Networking** section is intended to show IP interfaces, routes, and related settings for the appliance OS networking stack (management/data NICs).

The optical path (`diode1`/`diode2`) is:

- A **specialized hardware channel**, not a standard Ethernet/IP interface. - Used internally by the appliance to move application-level payloads from BLUE to RED. - Not exposed with typical NIC statistics (TX bytes, RX bytes, errors, etc.) in the UI.

As a result, seeing **blank or missing TX/RX counters** for `diode1` and `diode2` is **normal and by design**, not a malfunction.

3. **Security & simplicity of exposure** Because the diode is a **deterministic isolation device**—meant to strictly enforce one-way flow and prevent any leakage of network-level information—its design deliberately avoids exposing low-level link details beyond what is required for operations.

Instead of treating the optical link as a router/switch port with SNMP-style interface counters, the product exposes:

- **Diagnostics tools** (ping, TCP connect, route, etc.) for regular network interfaces. - **High-level system and process statistics** under Advanced → Statistics (Processes, File System, Memory, System Counters).

---

### [What statistics *are* available for the Optical Diode?](/docs/netwalldiode/v1.14.0/knowledge-base/why-don---t-the-metadefender-optical-diode-interfaces--diode1--a#what-statistics-are-available-for-the-optical-diode)

Even though `diode1`/`diode2` do not show TX/RX counters, you can still monitor performance and health:

1. **System statistics in the Web UI** Under **Advanced → Statistics**, you can view information on:

   - Processes
   - File system usage
   - Memory statistics
   - System counters

These give an overview of appliance health and performance rather than per-port optical metrics.

2. **Stream / transfer-level monitoring** Depending on the configured use case (file transfers, database replication, telemetry, etc.), you can monitor:

   - Whether **streams are active and successfully transferring data**
   - Effective **throughput at the application level** (e.g., file transfer performance, protocol-specific stats)

Product documentation and integration guides focus on **throughput options and supported transfer modes** (100 Mbps, 1 Gbps, 10 Gbps, etc.) rather than raw optical port counters.

3. **External monitoring via SNMP / PI tags** For operational monitoring, the diode supports exposing status and performance metrics to external monitoring systems:

   - Knowledge-base articles describe how to **export status/performance metrics of NetWall/Data Diodes using AVEVA PI tags**, allowing operators to track health and throughput over time.

These mechanisms are the recommended way to monitor diode performance, instead of relying on per-interface TX/RX counters.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

MetaDefender
