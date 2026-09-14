<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-do-i-troubleshoot-syslog-issues-for-metadefender-managed-fil -->

# How do I troubleshoot syslog issues for MetaDefender Managed File Transfer?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to all MetaDefender Managed File Transfer (MFT) releases.

When configuring syslog, you may encounter some issues if MFT or the environment is configured wrong. Please follow this troubleshooting guide to remediate these issues.

Error

Syslog is configured on MFT server, but no logs have been received on the syslog server.

**Troubleshoot**: First, open MFT logs to determine if there are any relevant error messages to narrow down the potential causes. Please refer to [How do I find all the MFT logs and their functionality?](/docs/mdmft/v3.11.4/knowledge-base/how-do-i-find-all-the-mft-logs-and-its-functionality-) for more info on these logs.

Next, verify that MFT server is sending syslog:

1. The syslog port is open and reachable: 514.
2. Verify that the syslog configuration (IP address, port) is correct on MFT web management console.
3. Set up packet capture on the server running MetaDefender product to see if syslog messages are being sent out on the configured syslog port and protocol (default is UDP port 514).

   - You can use pktmon (Windows built-in), tcpdump (Linux built-in), or other packet capture software such as WireShark.

If there are no messages received on the syslog server, or if packet capture doesn’t show any traffic sent on syslog port, you may need to double check syslog configurations, and/or check network connection between the MFT server and the syslog server.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).
