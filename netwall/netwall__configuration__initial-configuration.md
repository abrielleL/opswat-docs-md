<!-- source: https://www.opswat.com/docs/netwall/configuration/initial-configuration -->

# Initial Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page Important

A security dongle must be inserted in the BLUE and RED servers to change configuration.

### [MetaDefender Security Gateway Default IP](/docs/netwall/configuration/initial-configuration#metadefender-security-gateway-default-ip)

MetaDefender Unidirectional Security Gateway comes with a default IP of 10.10.10.10 to access the management UI. This is applicable for both sides BLUE and RED, so notice that you have to configure both sides.

Configure a laptop/desktop with a 10.10.10.X network address. Open a web browser and type <https://10.10.10.10> to access the web UI. Once in the login page, insert valid user/password.

Warning

Default credentials are opswat/a1aaaa. Please, change it as soon as possible

After login, user would need to accept the EULA.

### [IP Addresses](/docs/netwall/configuration/initial-configuration#ip-addresses)

After accepting the EULA, user will be redirected automatically to Settings page, where he/she will be prompted to insert the management IP and other connection details.

1. Fill in Management IP (for instance 192.168.30.244).
2. Fill in Net Mask (for instance 255.255.255.0)
3. Fill in Gateway (for instance 192.168.30.1)
4. Optionally, fill in DNS and NTP fields.
5. Check/Uncheck SSH Enabled checkbox to enable/disable SSH in the corresponding NetWall server
6. Check/Uncheck Forward Syslog to RED to enable/disable the sending of NetWall BLUE syslog to NetWall RED automatically.
7. Click Update to save the changes.

When changing Management IP, the system will reboot. Simply wait until the device reboots.

Also, user can click on the Login tab so the login UI can be customized:

- **System name:** Message displayed on a banner in the login page and in every screen.
- **Pre-login Message:** Message displayed at the login UI, before loging in.
- **Post-login Message:** Message displayed at the bottom of every screen after loging in.

### [Telemetry Data Collection](/docs/netwall/configuration/initial-configuration#telemetry-data-collection)

Important

MetaDefender Optical Diode collects and sends anonymized, aggregated usage and performance data to OPSWAT to help improve product performance and reliability. This feature is enabled by default over port 4317 and telemetry data is sent encrypted over TLS. A firewall configuration rule change is required to send telemetry data to OPSWAT.

Following the Management IP reboot, a dialogue box will appear. The dialogue box will only appear once upon initial setup. Use the tick box to **enable/disable** telemetry data collection. Telemetry data collection must be **enabled/disabled** on both the BLUE and RED sides.

Telemetry data collection must be **enabled/disabled** on both the BLUE and RED sides.

### [Set up DNS and NTP Servers](/docs/netwall/configuration/initial-configuration#set-up-dns-and-ntp-servers)

Once you have configured the management IP you can access the web UI to configure DNS and NTP servers.

### [DNS servers](/docs/netwall/configuration/initial-configuration#dns-servers)

1. Go to Configuration-> Settings
2. Click on Edit button
3. Type the IP address of the DNS server
4. Type the IP address of the DNS server 2 for an alternative DNS server
5. Click on Update button to save the changes

### [NTP servers](/docs/netwall/configuration/initial-configuration#ntp-servers)

1. Go to Configuration-> Settings
2. Click on Edit button
3. Type the IP address of the NTP server. Network Time Protocol (NTP) lets the clocks synchronize between computer systems through packet-switched, variable-latency data networks
4. Type the IP address of the NTP server 2 for an alternative NTP server
5. Click on Update button to save the changes

## [NTP Forwarding from BLUE to RED](/docs/netwall/configuration/initial-configuration#ntp-forwarding-from-blue-to-red)

This feature provides the ability to pass Network Time Protocol (NTP) from Blue to Red. It must be configured on both BLUE and RED

### [NTP Forwarding (BLUE)](/docs/netwall/configuration/initial-configuration#ntp-forwarding-blue)

1. Go to Configuration -> Settings
2. Click on Edit Button
3. Click on the NTP Forwarding box
4. Select Update to save configuration

### [NTP Forwarding (RED)](/docs/netwall/configuration/initial-configuration#ntp-forwarding-red)

1. Go to Configuration -> Settings
2. Click on Edit button
3. Make sure that there are no NPT servers listed in the settings
4. Click on the NTP Forwarding box
5. Select Update to save configuration

## [Additional Settings](/docs/netwall/configuration/initial-configuration#additional-settings)

1. Check/Uncheck **SSH Enabled** checkbox to enable/disable SSH in the corresponding NetWall server
2. Check/Uncheck **Forward Syslog to RED** (BLUE server only) to enable/disable the forwarding of NetWall BLUE syslog to RED automatically.
3. Check/Uncheck **Disable HTTP Redirect for Management UI** enable/disable HTTP Port in the corresponding NetWall server

## [Login Banner](/docs/netwall/configuration/initial-configuration#login-banner)

Click the Login tab to customize Pre and Post login banner messaging.

- **System name:** Message displayed on a banner in the login page and in every screen.
- **Pre-login Message:** Message displayed at the login UI, before logging in.
- **Post-login Message:** Message displayed at the bottom of every screen after logging in.

## [Set Time (Manual Configuration)](/docs/netwall/configuration/initial-configuration#set-time-manual-configuration)

Warning

Setting the time manually will cause MetaDefender Security Gateway to reboot. This will happen in both servers BLUE and RED.

There can be situations when configuring an NTP server is not possible (BLUE side with no Internet access, for instance). In this situations, admins can configure the Time manually:

1. Go to Configuration-> Settings
2. Click on Edit button
3. Select the time zone in the dropdown list
4. Click on Time field and select day and time in the deployed calendar, then Apply.
5. Click on Update button to save the changes

## [Security Gateway CLI](/docs/netwall/configuration/initial-configuration#security-gateway-cli)

Alternatively, you can set up the Management IP and L3 Routes using MetaDefender Security Gateway CLI connecting a monitor and a keyboard to each server, BLUE and RED.

Remember you can check available commands typing **?**

Login with valid credentials and set up L3 route and management IP. After that, you can access to the management UI using the configured management IP and configure DNS and NTP servers.

### [Set up Routes](/docs/netwall/configuration/initial-configuration#set-up-routes)

`eagle> config`

`eagle (config)> routes`

`eagle (config.routes)> add`

`eagle (config.routes.add)> gateway 192.168.X.X`

`eagle (config.routes.add)> target_range 0.0.0.0/0`

`eagle (config.routes.add)> save`

### [Set up Management IP and Port](/docs/netwall/configuration/initial-configuration#set-up-management-ip-and-port)

`eagle> management`

`eagle (mgmt)> ipaddress 192.168.X.X/24`

It will ask you to reboot, type 'y' and press 'enter'.

## [Security Gateway Dashboard](/docs/netwall/configuration/initial-configuration#security-gateway-dashboard)

Once correctly set up and configured, the user can check MetaDefender Security Gateway status in the Health Information section, where it can be checked if MetaDefender Security Gateway RED is correctly connected. A similar status icon can be checked in MetaDefender Security Gateway RED Dashboard.

## [OPSWAT Central Management Integration](/docs/netwall/configuration/initial-configuration#opswat-central-management-integration)

Central Management is a centralized console that you can perform global operations such as manage MetaDefender products and OPSWAT Client, view managed anti-malware engines, manage virus definition and engine updates, and check licensing status. For more information, please visit <https://docs.opswat.com/ocm>

To configure OCM is optional and very simple. The first time a user logs in in the Web UI a pop up to fill in the required information will appear.

Important

You need to configure OCM integration independently in BLUE and RED appliances.

You need a security dongle inserted in the appliance to change the configuration of OPSWAT Central Management.

- Server API URL: URL of your OCM Server's API
- Registration code: This registration code will be provided in the OPSWAT Central Management console.

Once the required information in indicated, click on Enroll Now button.
