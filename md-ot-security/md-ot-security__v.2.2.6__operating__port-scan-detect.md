<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/port-scan-detect -->

# Port Scan Detect

The **Port Scan Detect** is accessible under **Settings → Port Scan Detect**

The Port Scan Detect feature protects against malicious port scan detection attacks. IP addresses that conduct overt scans (FIN/XMAS/NULL scans) are blocked immediately. Malicious activity can be configured for obscure scans. These can consist of a source IP scanning anomalous number of ports or the scanning of one specific port an irregular number of times. Users can manually block IP addresses by adding them to a blocklist or unblock them by adding them to a allowlist. IPs that have been blocked past a specific amount of time can be unblocked via a clean-up process.

## [Configurations](/docs/md-ot-security/v.2.2.6/operating/port-scan-detect#configurations)

The **Configurations** is accessible under **Settings → Port Scan Detect → Configurations**

Port Scan uses thresholds and values to determine when to react to malicious activity. The thresholds are integer count values, time in seconds, or specific ports. Thresholds surpassed by any given host are treated as malicious activity.

Edit the following values as necessary:

- **Blocklist Rules Enforcement**: Enable/disable blocklist rules.
- **Maximum Port Scan Before Block**: Maximum number of port scans detected before IP is blocked.
- **Duration of IP Block** – (Seconds): Duration of IP block (in second) after triggering port scan threshold.
- **New Connection Time Interval**: Time elapsed before IP (in second) is considered a new connection.
- **Maximum Port Scans from Single IP Address:** Maximum number of port scans from a single IP address before it is blocked.
- **Maximum Overall Port Scan Before Blocklist Enabled:** Maximum number of port scans from all IP addresses before blocklist is enabled.
- **Ignored Ports**: List of ports to ignore for port scan detection.
- **Monitored Hot Ports**: List of commonly targeted ports closely monitored for port scan activity.

## [Blocked IPs](/docs/md-ot-security/v.2.2.6/operating/port-scan-detect#blocked-ips)

The **Blocked IPs** is accessible under **MetaDefender Industrial Firewall & IPS** **Configuration** → **Settings → Port Scan Detect → Blocked IPs**

The Blocked IP section contains IP addresses that are blocked by Port Scan Detect. You can unblock these addresses manually.

User can select IP then click on Unblock Selected button to unblock IP.

## [Allowlisted IPs](/docs/md-ot-security/v.2.2.6/operating/port-scan-detect#allowlisted-ips)

The **Allowlisted IPs** is accessible under **MetaDefender Industrial Firewall & IPS** **Configuration** → **Settings → Port Scan Detect → Allowlisted IPs**

The allowlist contains recognized IP addresses that are considered privileged by the organization. Activity from these IP addresses is not considered malicious.

User can add or delete Allowlisted IP addresses manually. User also can search IP address.

## [Blocklisted IPs](/docs/md-ot-security/v.2.2.6/operating/port-scan-detect#blocklisted-ips)

The **Blocklisted IPs** is accessible under **MetaDefender Industrial Firewall & IPS** **Configuration** → **Settings → Port Scan Detect → Blocklisted IPs.**

The blocklist contains IP addresses that are blocked or denied during monitoring. Activity from these IP addresses is considered malicious.

User can add or delete Blocklisted IP addresses manually. User also can search IP address.
