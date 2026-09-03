<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-to-use-system-proxy-settings-and-bypass-list-with-opswat-cen -->

# How do I use system proxy settings and a proxy bypass list with OPSWAT Central Management 7.5.0 and subsequent releases?

Using [the proxy configuration in the OPSWAT Central Management console](/docs/ocm/configuration/proxy-configuration) is recommended over system proxy settings.

Check Your Product:

This article applies to all OPSWAT Central Management V7.5.0+ releases deployed on Windows or Linux systems.

Starting with V7.5.0, OPSWAT Central Management incorporates a feature that allows users to configure OPSWAT Central Management’s proxy server separately from their system settings.

Starting with V7.5.0, OPSWAT Central Management can now also automatically adopt the operating system settings’ proxy bypass list, although bypass list configuration is not yet supported.

To properly configure your proxy settings with the help of these features, please follow the guidelines below.

## [Setting the system proxy](/docs/ocm/knowledgebase/how-to-use-system-proxy-settings-and-bypass-list-with-opswat-cen#setting-the-system-proxy)

### [**On Windows**](/docs/ocm/knowledgebase/how-to-use-system-proxy-settings-and-bypass-list-with-opswat-cen#on-windows)

Open a **Command Prompt** or **Powershell** as administrator, then enter the command **netsh winhttp set proxy proxy-server=“<name>” bypass-list= “<list>”**

ExampleCopynetsh winhttp set proxy proxy-server=“192.168.2.2:8080” bypass-list=“.ourdomain.com;.yourdomain.com”Please Note:

The supported proxy server format is: **<domain/ip>:<port>**

For example: **proxy.test.com:8080**

The supported bypass list format is: **<domain/ip1>;<domain/ip2>**, and the domain must follow convention by including wildcard characters (**.***) as suffixes or prefixes. For example: **192.168.202.;*.yourdomain.com**

### [**On RHEL**](/docs/ocm/knowledgebase/how-to-use-system-proxy-settings-and-bypass-list-with-opswat-cen#on-rhel)

Set the environment variables of **http_proxy** and **no_proxy** by opening the file **/etc/bashrc** and adding the corresponding export lines.

ExampleCopyExport http_proxy=192.168.2.2.8080 export no_proxy=192.168.202.*,*.yourdomain.comPlease Note:

The supported http_proxy format is: **<domain/ip>:<port>**, without specifying protocol.

For example: **http_proxy=proxy.test.com.8080**

The supported no_proxy format is: **<domain/ip1>,<domain/ip2>**, and the domain must follow Java’s convention by including wildcard characters (**.***) as suffixes or prefixes. For example: **192.168.202.;*.yourdomain.com**

Pro Tip:

On both Windows and Linux, OPSWAT Central Management requires a service restart, such as via the **Restart** button on its tray icon, to apply any changes to system settings.

## [Default settings](/docs/ocm/knowledgebase/how-to-use-system-proxy-settings-and-bypass-list-with-opswat-cen#default-settings)

- Following setup via the wizard, OPSWAT Central Management releases subsequent to 7.5.0 use their own proxy server configuration instead of the system settings’ proxy server. If the configuration is not enabled on the OPSWAT Central Management Console, the system will use no proxy server at all.
- Following setup, system settings’ proxy bypass list settings will be honored.
- Remember to restart the service via the tray icon **Restart** button, in order to apply any configuration changes.

## [Changing proxy settings for OPSWAT Central Management](/docs/ocm/knowledgebase/how-to-use-system-proxy-settings-and-bypass-list-with-opswat-cen#changing-proxy-settings-for-opswat-central-management)

### [**To change the current proxy server in use:**](/docs/ocm/knowledgebase/how-to-use-system-proxy-settings-and-bypass-list-with-opswat-cen#to-change-the-current-proxy-server-in-use)

1. Navigate to the **OPSWAT Central Management Console>Server Configuration>Proxy**.
2. Make the necessary changes to the proxy settings:

- (Optional) If the proxy server requires basic authentication, enter the required credentials (including **Username** and **Password**) into the provided fields.
- For a proxy that does not require authentication, the setting of credentials is not required.

Please Note:

OPSWAT Central Management currently only supports the basic authentication scheme.

3. Clic**k Save**.
4. OPSWAT Central Management’s UI will now refresh itself and save the new proxy server settings.

### [**To modify the current proxy bypass list in use:**](/docs/ocm/knowledgebase/how-to-use-system-proxy-settings-and-bypass-list-with-opswat-cen#to-modify-the-current-proxy-bypass-list-in-use)

1. Make changes to the bypass list according to the guidelines in the **Setting system proxy** section at the start of this article.

Please Note:

The Windows system requires that administrators specify a proxy server in order to modify the bypass list. However, OPSWAT Central Management will use its own proxy server settings, as configured by the user in **OPSWAT Management Console>Server Configuration>Proxy**.

2. **Restart** OPSWAT Central Management so that the new bypass list settings can take effect.

Support:

If you have followed the instructions above but have been unable to **Use System Proxy Settings And A Proxy Bypass List With OPSWAT Central Management**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
