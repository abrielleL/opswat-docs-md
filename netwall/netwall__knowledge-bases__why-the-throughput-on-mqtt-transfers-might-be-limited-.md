<!-- source: https://www.opswat.com/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited- -->

# Why the throughput on MQTT transfers might be limited?

This article applies to MetaDefender Optical Diode / NetWall Diode.

### [Key concept: “Platform throughput” vs “achieved application throughput”](/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited-#key-concept-platform-throughput-vs-achieved-application-throughput)

OPSWAT lists Optical Diode 1U throughput configurations as **100 Mbps, 1 Gbps, or 10 Gbps**. That defines the platform/license tier capability.

However, achieved throughput can be limited by:

- The **licensed throughput tier**
- The **physical interface speed** in use (1 Gb RJ45 vs 10 Gb SFP)
- Broker/server performance, encryption, message sizing, and connector overhead (environment-dependent)

---

### [Most common reason for a ~1 Gb/s ceiling: link/interface is 1 Gb](/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited-#most-common-reason-for-a-1-gbs-ceiling-linkinterface-is-1-gb)

OPSWAT’s setup documentation shows:

- **10Gb SFP ports** (e.g., “SFP3 10Gb Ethernet”, “SFP4 slot 10Gb Ethernet”)
- **RJ45 LAN ports listed as 1Gb** (e.g., LAN1 is 1Gb)

If your MQTT path (broker-facing connectivity) is on a **1Gb RJ45 port**, ~1 Gb/s is a practical ceiling regardless of tuning.

**Check:**

- Which physical ports are used for MQTT/broker connectivity on BLUE and RED
- End-to-end link negotiation (10Gb vs 1Gb) on switches/media converters

---

### [Second most common reason: unit is operating at the 1 Gbps tier](/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited-#second-most-common-reason-unit-is-operating-at-the-1-gbps-tier)

Even with 10Gb interfaces present, if the appliance is provisioned/licensed at **1 Gbps**, you should not expect sustained 2+ Gb/s. Confirm your purchased throughput level (100M / 1G / 10G).

---

### [Practical checklist to target 2+ Gb/s (in order)](/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited-#practical-checklist-to-target-2-gbs-in-order)

#### [1) Confirm throughput tier](/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited-#1-confirm-throughput-tier)

- Verify the deployed Optical Diode 1U throughput configuration is **10 Gbps** (not 1 Gbps).

#### [2) Confirm 10Gb physical path end-to-end](/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited-#2-confirm-10gb-physical-path-end-to-end)

- Use the **10Gb SFP** interfaces for the broker-facing path (where applicable)
- Ensure intermediate devices (switches/media converters) are also 10Gb and negotiating at 10Gb

#### [3) Confirm the connector in use and its tuning scope](/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited-#3-confirm-the-connector-in-use-and-its-tuning-scope)

- If performance work is being discussed, align the conversation to **MQTT connector tuning** when MQTT is the protocol in use.

#### [4) Validate broker-side capacity](/docs/netwall/knowledge-bases/why-the-throughput-on-mqtt-transfers-might-be-limited-#4-validate-broker-side-capacity)

- Ensure the MQTT broker(s) and destination infrastructure can accept the intended sustained rate (CPU, disk/logging, retention, network stack). (Environment-dependent; confirm with broker vendor metrics.)

Support:

If Further Assistance is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
