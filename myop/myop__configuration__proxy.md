<!-- source: https://www.opswat.com/docs/myop/configuration/proxy -->

# Proxy

My OPSWAT On-premises can be configured to send its traffic through a forward proxy. Administrators can configure proxy settings in the **Proxy** section of the **Settings >** **Server** tab navigated from the left navigation menu.

- **Use external proxy for http and https connection:** Enable the use of a proxy
- **Server Address, Port**: The address of the proxy server.
- **Username, Password**: The credentials to access the proxy server. Optional if the server does not require credentials.
- **Use the same proxy for HTTPs connections :** If selected, HTTPS connections will use the same proxy server as HTTP connections.
- **Bypass Proxy Server**: The bypass list includes any domains/IP addresses that should be accessed directly. Supported bypass list format:

  - An IP range (CIDR notation). For example: 192.168.203.1/16.
  - The broadcast and network addresses are not included in the bypass list.
  - Wildcard character * is supported as prefix or suffix. For example: 192.168.* or *.opswat.com

Info

My OPSWAT On-premises currently only supports the basic authorization scheme for a proxy credentials.
