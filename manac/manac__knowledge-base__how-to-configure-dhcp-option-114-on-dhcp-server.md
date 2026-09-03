<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-to-configure-dhcp-option-114-on-dhcp-server -->

# How to configure DHCP option 114 on Windows DHCP server

### [Overview](/docs/manac/knowledge-base/how-to-configure-dhcp-option-114-on-dhcp-server#overview)

IETF [RFC-8910](https://datatracker.ietf.org/doc/html/rfc8910) defines a standardized method for networks to notify clients of the presence of a captive portal. This is accomplish via a special DHCP option (114) which points clients to an [RFC-8908](https://datatracker.ietf.org/doc/html/rfc8908)-compliant "Captive Portal API" endpoint via which clients can request their "captive" status, and if captive, discover to what URL a browser window should be opened. Taking advantage of this captive portal detection method can make the captive portal experience smoother for end-users on compatible devices.

MetaDefender NAC 8.2.0 and later exposes a RFC-8908-compliant API endpoint to which DHCP option 114 can be pointed: <https://portal.myweblogon.com:8443/captive-portal/api>.

To implement this functionality on Windows Server 2019 and later, follow the instructions below.

## [How to configure DHCP option 114 on Windows Server](/docs/manac/knowledge-base/how-to-configure-dhcp-option-114-on-dhcp-server#how-to-configure-dhcp-option-114-on-windows-server)

1. On the server running DHCP, open the DHCP MMC.
2. Expand DHCP and select DHCP server name.
3. Right click **IPv4** or **IPv6**, select "**Set Predefined Options**"

4. In **Predefined Options and Values** window, click **Add**.

5. Then in **Option Type** window please insert the information as below:

Name: 114 Captive Portal URL

Data Type: String

Code: 114

6. Click OK, this option has been added on the DHCP server and you can configure this option on specific scope.

String value: [https://portal.myweblogon.com:8443/captive-portal/api](https://portal.myweblogon.com/captive-portal/api)
