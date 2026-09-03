<!-- source: https://www.opswat.com/docs/netwalldiode/knowledge-base/why-is-port-123-not-allowed-when-configuring-udp-streams-on-the- -->

# Why is Port 123 not allowed when configuring UDP Streams on the Blue side?

**Check Your Version:**

This article applies to **MetaDefender Optical Diode** deployments.

When attempting to set the Protocol to UDP and the Port to 123 on the Blue side, the Optical Diode will block the configuration with the message: *"Port 123 not allowed"*.

### [**Why is this port restricted?**](/docs/netwalldiode/knowledge-base/why-is-port-123-not-allowed-when-configuring-udp-streams-on-the-#why-is-this-port-restricted)

**Port 123** on the **Blue side** is reserved by the Optical Diode operating system to synchronize its own internal clock with a **Network Time Protocol (NTP)** server. Because the system requires this port for its own time management, it cannot be assigned to a user-defined UDP data stream.

Additionally, the Red side of the Optical Diode cannot currently act as an NTP server for other devices on the network.

### [**Workaround: Port Mapping Strategy**](/docs/netwalldiode/knowledge-base/why-is-port-123-not-allowed-when-configuring-udp-streams-on-the-#workaround-port-mapping-strategy)

To transmit data destined for Port 123 on your secure network (Red side), you can use a port mapping strategy to bypass restriction.

Since the Blue side cannot ingest traffic directly on Port 123, you must configure your external source to target an alternative "proxy" port (for example, 1234), which you can then map back on the Red side on port 123.

**Recommended Configuration Flow:**

1. **Data Source (External):** Configure your external script, application, or device to send its data to the **Blue Interface IP** using an available non-reserved port (e.g., **UDP 1234**).
2. **Blue Side (Ingress):** Configure the UDP Stream to receive data on that same port (**Port 1234**).
3. **Red Side (Egress):** Configure the UDP Stream to send the data out to the destination IP on **Port 123**.

This configuration allows traffic to arrive at the destination on the correct port (123) while respecting the Blue side's system reservation.

**Future Enhancement**

We are currently exploring enhancements to support passing NTP traffic directly from the Blue side to the Red side in future releases.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

MetaDefender
