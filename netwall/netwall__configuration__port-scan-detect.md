<!-- source: https://www.opswat.com/docs/netwall/configuration/port-scan-detect -->

# Port Scan Detect

The Port Scan Detect feature protects against malicious port scan detection attacks. IP addresses that conduct overt scans (FIN/XMAS/NULL scans) are blocked immediately. Malicious activity can be configured for obscure scans. These can consist of a source IP scanning anomalous number of ports or the scanning of one specific port an irregular number of times. Users can manually block IP addresses by adding them to a blocklist or unblock them by adding them to an allowlist. IPs that have been blocked past a specific amount of time can be unblocked via a clean-up process.

## <Configuration>

Port Scan uses thresholds and values to determine when to react to malicious activity. The thresholds are integer count values, time in seconds, or specific ports. Thresholds surpassed by any given host are treated as malicious activity.

Use the following procedure to change the thresholds:

1. Open the **Configuration** menu, then select **Port Scan Detect** > **Configuration**. The *Configuration* pane displays.

Edit the following values as necessary:

- **Port Scan Threshold**: Threshold count of hits per unique port during analysis of host activity.
- **Single IP Scan Threshold**: Threshold count of ports scanned during analysis of host activity.
- **Overall Port Scan Threshold**: Threshold count of collective activity during analysis of host activity. Collective activity is based on combinations of actions, for example if one host hits port 23 four times and ports 80,443,8080,9000,9090 each once.
- **Last Seen Delta (Integer Seconds)**: Port Scan Detection processes will block hosts that have *last been seen* within (less than) this value.
- **Lockout Time (Integer Seconds)**: If a host has been blocked for a period longer than this value, it will be unblocked.
- **Ports to Ignore**: Comma delimited string of ports to ignore while processing live network traffic. A range of ports is supported if the format is properly used (x-y). Example (note no white spaces when specifying a range): ports to ignore:22,443,80-90,8080,8443-8448,502.
- **Hot Ports**: Comma delimited string of ports to immediately create a block action (of the relevant src ip) upon encountering.
- **Enabled**: Click to enable/disable the scans.

Notes

- Ports to Ignore: will always include ports 6446 and 443.
- The same port cannot be in both **Ports To Ignore** and **Hot Ports** at the same time.
## [Unblock IPs](/docs/netwall/configuration/port-scan-detect#unblock-ips)

The Blocked IP Management table lists IP addresses that are blocked by Port Scan Detect. You can unblock these addresses manually.

Warning

IP Addresses on the blocklist cannot be unblocked using this feature. Use the “Delete Blocked IP” procedure to unblock the IP address.

1. Open the **Configuration** menu and select **Port Scan Detect** > **Blocked IPs**. The *Blocked IPs Management* pane displays.
2. Click in the box to select the IPs that you will unblock.
3. Open the **Action** menu and click **Unblock Selected**.
4. Click **Submit** to confirm your action. A green banner indicates success.

## [Allowed IPs](/docs/netwall/configuration/port-scan-detect#allowed-ips)

The allowlist contains recognized IP addresses that are considered privileged by the organization. Activity from these IP addresses is not considered malicious.

### [Add Allowed IP](/docs/netwall/configuration/port-scan-detect#add-allowed-ip)

1. Open the **Configuration** menu and select **Port Scan Detect** > **Allow list IPs**. The *Allow__list IP Management* pane displays.
2. Open the **Action** menu and click **Add Custom IPs**. A detail window displays.
3. Enter the **IP address** in the box.
4. Click the **Submit** button.

### [Delete Allowed IP](/docs/netwall/configuration/port-scan-detect#delete-allowed-ip)

1. Open the **Configuration** menu and select **Port Scan Detect** > **Allowlist IPs**. The *Allowlist IP Management* pane displays.
2. Select an IP you want to delete.
3. Open the **Action** menu and click **Delete Selected.**
4. Click **Submit** to confirm your decision.

## [Blocked IPs](/docs/netwall/configuration/port-scan-detect#blocked-ips)

The blocklist contains IP addresses that are blocked or denied during monitoring. Activity from these IP addresses is considered malicious.

### [Add IP to Blocklist](/docs/netwall/configuration/port-scan-detect#add-ip-to-blocklist)

1. Open the **Configuration** menu and select **Port Scan Detect** > **Blocklist IPs**. The *Blocklist IP Management* pane displays.
2. Open the **Action** menu and click **Add Custom IPs**. A detail window displays.
3. Enter the **IP address** in the box.
4. Click the **Submit** button.

### [Delete IP in the Blocklist](/docs/netwall/configuration/port-scan-detect#delete-ip-in-the-blocklist)

1. Open the **Configuration** menu and select **Port Scan Detect** > **Blocklist IPs**. The *Blocklist IP Management* pane displays.
2. Select an IP you want to delete.
3. Open the **Action** menu and click **Delete Selected.**

Click the **Submit** button to confirm your action.
