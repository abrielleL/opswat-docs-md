<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic -->

# Sensor - Network Diagnostic

**Network Diagnostic** setting is accessible under **Settings > Network Diagnostic**

Network diagnostics involve using specific tools and techniques to identify and resolve connectivity issues, measure performance, and ensure proper communication across devices. Below are some commonly used tools and their applications:

## [**1. Ping Test**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#1-ping-test)

### [**Purpose:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#purpose)

To verify network connectivity between two devices and measure the latency (response time).

### [**How It Works:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#how-it-works)

The ping command sends ICMP (Internet Control Message Protocol) Echo Requests to a target address and listens for Echo Replies.

### [**Steps to Perform:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#steps-to-perform)

1. Clicking on the Ping Test tab.
2. Run the Ping followed by the target IP address or hostname:

1. Analyze the output:

   - **Successful Reply:** Indicates connectivity.
   - **Packet Loss:** Signifies a problem in the network.
   - **Latency (ms):** Measures the time taken for packets to travel to the destination and back.

### [**Key Metrics:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#key-metrics)

- **Latency (ms):** Lower values indicate faster response times.
- **Packet Loss (%):** Any packet loss suggests network issues.

## [**2. Trace Route**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#2-trace-route)

**Purpose:**

To identify the path taken by packets to reach their destination and pinpoint delays or failures in the route.

### [**How It Works:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#how-it-works)

The traceroute command (Linux/macOS) sends packets with increasing Time-to-Live (TTL) values to record each hop.

### [**Steps to Perform:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#steps-to-perform)

1. Clicking on the Trace Route tab.
2. Run the Trace Route followed by the target IP address:

3. Examine the output:

   - Each line represents a network device (hop).
   - Look for high latency or "request timed out" messages to identify problematic hops.

### [**Use Case:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#use-case)

- Troubleshooting slow network performance.
- Identifying a specific network device causing delays.

## [**3. Telnet**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#3-telnet)

### [**Purpose:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#purpose)

To test connectivity to a specific port on a remote device and troubleshoot services running on that port.

### [**How It Works:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#how-it-works)

The telnet command establishes a connection to a target IP and port to verify accessibility.

### [**Steps to Perform:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#steps-to-perform)

1. Clicking on the Telnet tab.
2. Run the telnet with the target IP and port:

1. Interpret the result:

   - **Successful Connection:** Indicates the port is open and accessible.
   - **Connection Refused/Timeout:** Indicates the port is closed or blocked by a firewall.

### [**Use Case:**](/docs/md-ot-security/v4.0.0/settings/sensor-network-diagnostic#use-case)

- Verifying access to services like HTTP (port 80), HTTPS (port 443), or SSH (port 22).
- Debugging blocked or inaccessible ports.
