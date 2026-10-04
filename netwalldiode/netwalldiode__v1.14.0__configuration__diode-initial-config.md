<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/configuration/diode-initial-config -->

# MetaDefender Optical Diode Initial Configuration

A security dongle must be inserted in the BLUE and RED servers to change configuration.

### [Optical Diode Default IP](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#optical-diode-default-ip)

MetaDefender Optical Diode (hereinafter Optical Diode) comes with a default IP of 10.10.10.10 to access the management UI. This is applicable for both sides BLUE and RED, so notice that you have to configure both sides.

Configure a laptop/desktop with a 10.10.10.X network address. Open a web browser and type <https://10.10.10.10> to access the Web UI. Once in the login page, insert valid user/password.

Warning

Default credentials are opswat/a1aaaa. Please change credentials as soon as possible

After login, accept the EULA Terms of Service.

### [IP Addresses](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#ip-addresses)

After accepting the EULA, user will be redirected automatically to Settings page. You will be prompted to insert the management IP and other connection details.

1. Fill in Management IP (for example 192.168.30.244).
2. Fill in Net Mask (for example 255.255.255.0)
3. Fill in Gateway (for example 192.168.30.1)
4. Click **Update** to save the changes.

When changing Management IP, the system will reboot. Simply wait until the device reboots.

### [Set up DNS and NTP Servers](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#set-up-dns-and-ntp-servers)

Once you have configured the management IP you can access the web UI to configure the DNS and NTP servers.

### [DNS Servers](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#dns-servers)

1. Go to **Configuration-> Settings**
2. Click on **Edit** button
3. Type the IP address of the DNS server
4. Type the IP address of the DNS server 2 for an alternative DNS server
5. Click on **Update** button to save the changes

### [NTP Servers](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#ntp-servers)

1. Go to **Configuration-> Settings**
2. Click on **Edit** button
3. Type the IP address of the NTP server. Network Time Protocol (NTP) lets the clocks synchronize between computer systems through packet-switched, variable-latency data networks
4. Type the IP address of the NTP server 2 for an alternative NTP server
5. Click on **Update** button to save the changes

## [NTP Forwarding BLUE to RED](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#ntp-forwarding-blue-to-red)

### [NTP Forwarding (BLUE)](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#ntp-forwarding-blue)

This feature provides the ability to synchronize Network Time Protocol (NTP) from Blue to Red. It must be configured on both BLUE and RED

1. Go to **Configuration -> Settings**
2. Click on **Edit** Button
3. Click on the NTP Forwarding box
4. Select **Update** to save configuration

### [NTP Forwarding (RED)](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#ntp-forwarding-red)

1. Go to **Configuration -> Settings**
2. Click on **Edit button**
3. Leave the NPT Server and NTP Server #2 boxes blank
4. Click on the NTP Forwarding box
5. Select **Update** to save configuration

Important

The external NTP client on the RED network must be configured to use the RED Optical Diode as an NTP server.

## [Additional Settings](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#additional-settings)

1. Check/Uncheck **SSH Enabled** checkbox to enable/disable SSH in the corresponding NetWall server
2. Check/Uncheck **Forward Syslog to RED** (BLUE server only) to enable/disable the forwarding of NetWall BLUE syslog to RED automatically.
3. Check/Uncheck **Disable HTTP Redirect for Management UI** enable/disable HTTP Port in the corresponding NetWall server

## [Login Banner](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#login-banner)

Click the Login tab to customize Pre and Post login banner messaging.

- **System name:** Message displayed on a banner in the login page and in every screen.
- **Pre-login Message:** Message displayed at the login UI, before logging in.
- **Post-login Message:** Message displayed at the bottom of every screen after logging in.

## [Set Time (Manual Configuration)](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#set-time-manual-configuration)

Warning

Setting the time manually will cause the Optical Diode to reboot. This will happen in both servers BLUE and RED.

There can be situations when configuring an NTP server is not possible (BLUE side with no Internet access, for instance). In this situations, admins can configure the Time manually:

1. Go to Configuration-> Settings.
2. Click on Edit button.
3. Select the time zone in the dropdown list.
4. Click on Time field and select day and time in the deployed calendar, then Apply.
5. Click on Update button to save the changes.

## [Optical Diode CLI](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#optical-diode-cli)

Alternatively, you can set up the Management IP and L3 Routes using the Optical Diode CLI connecting a monitor and a keyboard to each server, BLUE and RED.

Remember you can check available commands by typing **?**

Login with valid credentials and set up L3 route and management IP. After that, you can access to the management UI using the configured management IP and configure DNS and NTP servers.

### [Set up Routes](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#set-up-routes)

`eagle> config`

`eagle (config)> routes`

`eagle (config.routes)> add`

`eagle (config.routes.add)> gateway 192.168.X.X`

`eagle (config.routes.add)> target_range 0.0.0.0/0`

`eagle (config.routes.add)> save`

### [Set up Management IP and Port](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#set-up-management-ip-and-port)

`eagle> management`

`eagle (mgmt)> ipaddress 192.168.X.X/24`

It will ask you to reboot, type 'y' and press 'enter'.

## [Optical Diode Dashboard](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#optical-diode-dashboard)

Once correctly set up and configured, the user can check MetaDefender Optical Diode's status in the Health Information section in MetaDefender Optical Diode RED Dashboard, where it can be checked if MetaDefender Optical Diode BLUE is correctly connected. It also can be checked if the redundant path is correctly connected (only in the 1U version).

## [OPSWAT Central Management Integration](/docs/netwalldiode/v1.14.0/configuration/diode-initial-config#opswat-central-management-integration)

Central Management is a centralized console that you can perform global operations such as manage MetaDefender products and OPSWAT Client, view managed anti-malware engines, manage virus definition and engine updates, and check licensing status. For more information, please visit <https://docs.opswat.com/ocm>

To configure OCM is optional and very simple. The first time a user logs in in the Web UI a pop up to fill in the required information will appear.

Important

You need to configure OCM integration independently in BLUE and RED appliances.

You need a security dongle inserted in the appliance to change the configuration of OCM integration.

- Server API URL: URL of your OCM Server's API
- Registration code: This registration code will be provided in the OPSWAT Central Management console.

Once the required information in indicated, click on Enroll Now button.

MetaDefender
