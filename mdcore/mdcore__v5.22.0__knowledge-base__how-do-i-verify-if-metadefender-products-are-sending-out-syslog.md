<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-do-i-verify-if-metadefender-products-are-sending-out-syslog -->

# How do I verify if MetaDefender products are sending out syslog messages to the syslog server?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

After setting up syslog configuration, there are a few ways to verify that the MetaDefender product is sending syslog:

1. Check on the syslog server if it’s receiving syslog messages.
2. Set up packet capture on the server running MetaDefender product to see if syslog messages are being sent out on the configured syslog port and protocol (default is UDP port 514).

If there are no messages received on the syslog server, or if packet capture doesn’t show any traffic sent on syslog port, you may need to check your syslog configuration for the MetaDefender product to make sure it’s correct, and/or check network connection between the MetaDefender server and the syslog server.

To set up and analyze packet capture, please follow one of the following methods:

### [Method 1: Use a packet capture program](https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-verify-if-metadefender-products-are-sending-out-syslog-#method-1-use-a-packet-capture-program)

You can use a dedicated program to capture packets from the server, such as Wireshark.

### [Method 2: Use Windows built-in tool](https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-verify-if-metadefender-products-are-sending-out-syslog-#method-2-use-windows-built-in-tool)

Packet Monitor (pktmon) is a Windows built-in tool that you can use to capture packets. To use it, follow these steps:

1. In Powershell or Command Prompt, add the pktmon filter for syslog port: `pktmon filter add -p 514`
2. (Optional) List the current filters: `pktmon filter list`
3. Start packet capture, specifying that the entire packet should be logged with the argument “-pkt-size 0”: `pktmon start --capture --pkt-size 0`
4. After performing some actions on the MetaDefender product that send syslog messages, stop the capture: `pktmon stop`
5. The capture file “PktMon.etl” (by default will be saved in C:\Windows\System32) can be analyzed using tools like Microsoft Network Monitor or Wireshark.
6. (Optional) Export the capture to a human-readable format (the “output.txt” file will be in the same directory as “PktMon.etl”: `pktmon format PktMon.etl -o output.txt`

### [Method 3: Use Linux built-in tool](https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-verify-if-metadefender-products-are-sending-out-syslog-#method-3-use-linux-built-in-tool)

Tcpdump is a Linux built-in tool for packet capture. Run the following command in terminal to capture traffic on UDP port 514:

- `sudo tcpdump -I any udp port 514`

This command will display the captured packets in real-time in your terminal. If you want to save the captured packets to a file analysis, run the following command:

- `sudo tcpdump -i any udp port 514 -w capture_file.pcap`

To read and analyze the saved file, run the following command:

- `tcpdump -r capture_file.pcap`

Log message format

If the monitoring/analytics solution is configured to only ingest/forward log messages formatted in **Common Event Format (CEF)**, the log format will need to be configured to CEF as well in MetaDefender Core.

**Symptom**: if the monitoring/analytics solution is configured to only ingest logs in CEF, you may notice that MetaDefender Core is sending out syslog (when analyzing packet capture), but nothing shows up on the syslog server.

**Remediation**: follow the [MetaDefender Configuration](/docs/mdcore/v5.22.0/configuration/metadefender-configuration#logger) documentation to configure MetaDefender Core log message format to CEF, and it will send out syslog messages formatted in CEF as well.

- Windows:

  - Path: `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\logger`
  - Key: cef
  - Type: string value
  - Value: true
- Linux:

  - Path `/etc/ometascan/ometascan.conf`
  - Content:

Support:

If you are having issues or require further assistance regarding Verifying syslog configuration on MetaDefender Core, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
