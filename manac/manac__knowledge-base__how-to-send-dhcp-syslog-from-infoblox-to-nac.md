<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-to-send-dhcp-syslog-from-infoblox-to-nac -->

# How to send DHCP Syslog from Infoblox to NAC

1. Access to Infoblox Dashboard -> **System** -> **System Properties**

2. Choose **Monitoring**

3. Configure value

   1. Check the box "Log to External Syslog Servers"
   2. Address "IP address of NAC"
   3. Port "514"
   4. Logging Category - > Select DHCP Process
