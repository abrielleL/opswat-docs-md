<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/engine-config-api -->

# API

Configure backend REST API server access.

Proxy usage

See: [How to install Sandbox with Proxy support](https://docs.opswat.com/filescan/installation-with-proxy)

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #2 - Modify the server configuration by adding or modifying the following properties:**

transform.cfgCopy# Secret
apiKey0.secret=
# Server
listenServerPort=22001
# Proxy
proxyHost=proxy.example.com
proxyPort=3128
proxyUser=optional_user
proxyPassword=optional_password
nonProxyHosts=localhost
proxyType=HTTP

**Step #3 - Save the file and restart the** `sandbox` **service**

## [Property Details](/docs/filescan/3.1.1/configuration/engine-config-api#property-details)

| Property Name | Default value | Description |
| --- | --- | --- |
| apiKey0.secret | <generated> | API key, used in HTTP Header: 'secret'. |
| listenServerPort | 22001 | HTTP port |
| proxyHost |  | Host of proxy server |
| proxyPort |  | Port of proxy server |
| proxyUser |  | Optional proxy basic auth user |
| proxyPassword |  | Optional proxy basic auth password |
| nonProxyHosts | localhost | A list of hosts which should be reached directly |
| proxyType | HTTP | Proxy type, can be: *'HTTP', 'DIRECT', 'SOCKS'* |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
