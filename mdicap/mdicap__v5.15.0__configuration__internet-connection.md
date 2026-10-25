<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/configuration/internet-connection -->

# Internet connection

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender ICAP Server requires internet connection for [online license activation.](/docs/mdicap/v5.15.0/installation/activating-metadefender-icap-server-licenses)

## [For ICAP version v5.5.1 and newer](/docs/mdicap/v5.15.0/configuration/internet-connection#for-icap-version-v551-and-newer)

Since MetaDefender ICAP Server v5.5.1, proxy configuration is possible via management console UI, and with proxy authentication support. MetaDefender ICAP erver no longer relies on system configurations to obtain the proxy setting, but it will control the thing itself.

Select "**custom Configuration**" to setup the proxy

### [Proxy Server Configuration](/docs/mdicap/v5.15.0/configuration/internet-connection#proxy-server-configuration)

| Properties | Description | Option |
| --- | --- | --- |
| SERVER | Proxy server host address | IP address / Domain all accepted |
| PORT | Proxy server port | Some default common ports: 3128 (Squid), 49152 (ProxySG) |

### [Proxy User Authentication](/docs/mdicap/v5.15.0/configuration/internet-connection#proxy-user-authentication)

| Properties | Option |
| --- | --- |
| USERNAME | Username for proxy authentication |
| PASSWORD | Password for proxy authentication |

### [Exclusion List](/docs/mdicap/v5.15.0/configuration/internet-connection#exclusion-list)

Define a list of destination addresses to be excluded from going through pre-configured proxy server (use semicolons ; to separate entries).

Applied to connections triggered by MetaDefender ICAP Server for following activities:

- User MD Cloud as backend for scanning
- Scan by Metadefender Core
- License Handling
- Connect to OPSWAT Central Management
- Single Sign On integration (Fetch metadata from URL and login)

Supported formats:

- Lowercase-only
- IP range (CIDR notation). For example: 192.168.203.1/16
- Valid IP address or host name. Wildcard character * is supported as prefix and/or suffix.

  - For example: 192.168.; *.opswat.

## [For ICAP version lower than v5.5.1](/docs/mdicap/v5.15.0/configuration/internet-connection#for-icap-version-lower-than-v551)

### [Proxy configuration](/docs/mdicap/v5.15.0/configuration/internet-connection#proxy-configuration)

#### [Linux](/docs/mdicap/v5.15.0/configuration/internet-connection#linux)

Set variable https_proxy in file /etc/default/mdicapsrv.

#### [Windows](/docs/mdicap/v5.15.0/configuration/internet-connection#windows)

**From version v5.2.0**

- 1. Press **Windows + R** to open the Windows Run prompt
- 2. Type in **sysdm.cpl** and click **OK**.

- 3. Open the **Advanced** tab and click on the **Environment Variables** button in the System Properties window.

- 4. Add the new System variable

- 5. Input your proxy address and save

If you need to use HTTPS proxy server for the activation:
Variable name: https_proxy
Variable value: https://<proxy address>:<proxy_port>

**For older than v5.2.0**

Under Windows use the netsh tool to set the proxy, e.g.: netsh winhttp set proxy <ADDRESS>

In some cases setting the proxy with netsh is not sufficient. In that case set the proxy by starting Internet Explorer with SYSTEM rights and configure the proxy in the settings. To do this please follow this [article](http://social.technet.microsoft.com/wiki/contents/articles/13710.how-to-configure-proxy-settings-for-configuration-manager-primary-sites-that-manage-cloud-services.aspx).

Info

You might need to configure Windows proxy to bypass local addresses if you can't access Web Management Console from the host itself. Consult netsh documentation for additional configuration options.

### [No Proxy configuration](/docs/mdicap/v5.15.0/configuration/internet-connection#no-proxy-configuration)

To avoid traffic between MD ICAP Server and MD Core go through proxy by setting on [Proxy configuration](/docs/mdicap/v5.15.0/configuration/internet-connection#proxy-configuration), set **no_proxy** variable in file **/etc/default/mdicapsrv**

For example: MD ICAP Server under proxy setting want to connect o 2 MD Core servers with domain **https: //local.core. awesomecompany .net:8008** and IP address: [**http://10.40.50.111:8008**](http://10.40.50.111:8008) then domain **https: //local.core. awesomecompany .net:8008** and [**http://10.40.50.111:8008**](http://10.40.50.111:8008) should be set to variable **no_proxy** as below:

#### [Linux](/docs/mdicap/v5.15.0/configuration/internet-connection#linux)

no_proxy=10.40.50.111/32,.core.awesomecompany.netInfo

From MD ICAP Server 5.1.0 the cidr must be set with IP Address (10.40.50.111/32), with older version do not need follow cidr

**E.g for older version than MD ICAP Server v5.1.0**

no_proxy=10.40.50.111,.core.awesomecompany.net

###
