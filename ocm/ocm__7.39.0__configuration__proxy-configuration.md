<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/proxy-configuration -->

# Proxy Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page

OPSWAT Central Management can be configured to send its traffic through a forward proxy. Administrators can configure proxy settings in the **Proxy** tab at **Settings >** **Server Configuration.**

- **Enable proxy:** Enable the use of proxy
- **Use the system/external proxy:** Swap between using the system proxy settings available on the machine or the proxy settings configured only for OPSWAT Central Management.
- **External proxy only:**

  - **different settings/same settings:** Determine if each protocol should have their own proxy server settings or if they should share the same settings.
  - **Username,** **Password:** The credentials to access the proxy server. Optional if the server does not require credentials.
  - **Proxy Address, Port:** The address of the proxy server.
  - **Bypass Proxy Server:** The bypass list includes the domain that should be accessed directly and not via proxy.

Info

OPSWAT Central Management currently only supports the basic authorization scheme for proxy credentials.

Info

Supported bypass list format:

- IP range (CIDR notation).
  For example: 192.168.203.1/16.
  **Note:** The broadcast and network addresses are not included in the bypass list.
- Valid IP address or host name. Wildcard character * is supported as prefix and/or suffix.
  For example: 192.168.*;*.opswat.*

**Note:** Each entry should be separated by the semi-colon character ';'.

## [System proxy settings](/docs/ocm/7.39.0/configuration/proxy-configuration#system-proxy-settings)

In the setup wizard after a fresh installation, OPSWAT Central Management will attempt to locate the current system proxy settings and bypass list:

- On Windows, via the netsh winhttp command.
- On Ubuntu, via the environment variables http_proxy, https_proxy and no_proxy set in the EnvironmentFile configuration for OPSWAT Central Management's service file (/var/lib/ocm/ocm.service).
- On Red Hat Enterprise Linux, via the environment variables http_proxy, https_proxy and no_proxy set in /etc/bashrc.

Info

The environment variable http_proxy will be used for both http and https protocols, if its counterpart https_proxy is not detected.

The system proxy settings will be saved to OPSWAT Central Management's proxy configuration.

Warning

OPSWAT Central Management requires a restart to adopt newly changed system settings.

Warning

The supported format for proxy server is <host>:<port>, for example, proxy.test.com:1111.
Please use OPSWAT Central Management's external proxy settings on the console if your system proxy server does not fit this format.
