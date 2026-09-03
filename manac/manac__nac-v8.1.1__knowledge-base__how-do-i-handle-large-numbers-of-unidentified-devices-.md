<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-handle-large-numbers-of-unidentified-devices- -->

# How do I handle large numbers of unidentified devices?

Sometimes you will find that there are great quantities of devices the NAC is unable to identify. This could be due to several factors on the network, or it might simply indicate that the NAC device ID database needs an update. Please use the steps below to minimize user impact, help determine the root cause and expedite the fix.

## [Instructions](/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-handle-large-numbers-of-unidentified-devices-#instructions)

1. If the problem is extremely pressing, please disable NAC enforcement while remediation is in progress. Instructions here: [How to de-integrate NAC from a Layer 2 / Layer 3 network (RBE/PBR)?](/docs/manac/nac-v8.1.1/knowledge-base/how-to-de-integrate-nac-from-a-layer-2---layer-3-net)
2. If you are unable to disable enforcement for whatever reason, or if the troubleshooting steps below are not sufficient, please open a Severity 1 Support case via [My OPSWAT](https://my.opswat.com/support). If you are currently using the chatbot in the portal, please ask it to create an urgent support case for you.
3. Next ensure that your DHCP servers are sending syslog events to the NAC. Step by step guidance here: [How do I troubleshoot DHCP Syslog Service issues?](/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-troubleshoot-dhcp-syslog-service-issues)
4. If DHCP syslog appears to be functioning, you can also check that your wireless hardware is sending the Framed-Ip-Address key as part of the RADIUS AAA process. If the Framed-Ip-Address is missing, steps to enable this will vary by wireless vendor.
5. If you do need to open a Support case, please update the case with one or more MAC addresses from affected devices, ideally along with their device type, as reported by your staff or end users, if possible.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
