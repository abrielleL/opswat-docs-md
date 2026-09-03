<!-- source: https://www.opswat.com/docs/mdinsights/feeds/metadefender-insights-c2 -->

# MetaDefender InSights C2

> ## [About MetaDefender InSights C2 feeds](/docs/mdinsights/feeds/metadefender-insights-c2#about-metadefender-insights-c2-feeds)
>
> InSights C2 is a focused set of threat intelligence indicators that includes OPSWAT's most novel analysis on malware command and control (C2) infrastructure, exfiltration and stage retrieval. Monitoring for communication with adversary C2 endpoints is a highly effective means of surfacing compromised assets in IT and OT environments, and can enable quicker incident detection times and inform better scoping and response to threats.

### [Indicator types](/docs/mdinsights/feeds/metadefender-insights-c2#indicator-types)

InSights C2 comprises the following types of threat indicators:

- IP addresses
- Domain names

### [Target use case](/docs/mdinsights/feeds/metadefender-insights-c2#target-use-case)

InSights C2 is optimized for direct blocking and alerting of domain and IP addresses in operational security uses, and is valuable for SOCs, incident responders and threat hunters in identifying and remediation of compromised assets. We recommend to utilize InSights C2 threat feeds to monitor network traffic outbound from enterprise LANs and at the network perimeter to monitor traffic traversing the edge toward the public internet. Organizations may also apply InSights C2 data to application logs such as EDR network connection (netconn) logs or proxy server access logs.

#### [Placement considerations](/docs/mdinsights/feeds/metadefender-insights-c2#placement-considerations)

Many organizations utilize network security monitoring (NSM) and network intrusion detection system (NIDS) sensors to monitor network traffic for C2 sessions.

Effective network traffic and session monitoring application can be challenging given common enterprise architecture. While considering placement at the network edge for all outbound traffic flows, organizations must retain the ability to identify devices that are attempting to interact with C2 servers. We recommend evaluating and applying monitoring in these specific cases to ensure the ability to preserve awareness of originating clients that attempt to establish outbound connections:

**At perimeter firewalls and NAT gateways**

- The most effective placement for network security monitoring sensors at the network edge is on the internal side of firewalls or NAT gateways. Placement outside the firewall typically results in two problems:

  - Difficulty identifying originating client IP addresses, since connections have passed through NAT on their way to the internet.
  - Overwhelming amounts of noise and backscatter on external network interfaces, which can overwhelm sensor resources and would normally be filtered before reaching network sensing interfaces placed internally.

**At web proxy servers**

- Ensure monitoring points in front of web proxies to ensure the ability to capture originating client IP addresses that attempt connections to infrastructure listed in InSights C2 feeds.
- An effective approach with explicit proxies is to capture proxy access logs and apply monitoring to key fields such as the request hostname and origin IP address (remote web server).
- Environments with transparent proxies should consider placing network monitoring sensors in front of proxy servers. This is typically placement in the network segment that is a choke point in front of the proxies, relative to routers or switches which intercept and redirect outbound traffic to the proxies. Network sensors placed only at the network edge will only see the proxied request sent by the proxy to the origin server, leaving analysts struggling to identify originating client identities.

Types of web proxy servers

HTTP proxy servers are often deployed in two possible configurations:

**Explicit proxies** are configured on the clients, and may be explicitly set through policy in web browsers, [PAC files](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_PAC_file), or environment variables. In an explicit proxy configuration, clients make connections to the proxy server, make their request to the proxy, and the proxy server then opens a second connection to the origin server and passes the client request.

**Transparent proxies** are typically configured in network infrastructure, using technologies such as layer 4 traffic policy rules or [WCCP](https://en.wikipedia.org/wiki/Web_Cache_Communication_Protocol) to intercept outbound client connections on web ports and redirecting those connections to terminate at the organization's proxy servers. Clients do not require explicit configurations and are unaware that their outbound traffic is being intercepted for monitoring.

**At DNS caches**

- DNS caching resolvers are a type of proxy, similar to web proxies. Similar to web proxies, ensure monitoring positions in front of DNS resolvers to ensure the ability to identify client request origins.

**At VPN and remote access gateways**

- Ensure that traffic traversing into the enterprise network from remote access clients is monitored inside any VPN servers and concentrators.
- Placement must be inside the VPN gateway, after traffic is decrypted.
- Configuring VPN systems to tunnel all traffic, including that destined to the public internet, ensures that outbound C2 connections from remote access clients traverses the monitored network segments and can be successfully identified.

### [Methodology](/docs/mdinsights/feeds/metadefender-insights-c2#methodology)

This feed is primarily composed of the output of our threat intelligence analysts’ work product as well as proprietary sources and curated open source intelligence (OSINT) collection.

### [Target systems](/docs/mdinsights/feeds/metadefender-insights-c2#target-systems)

Our InSights C2 feed is ideal for integration into frontend security monitoring, incident response and threat hunting workflows where data quality and high confidence alerts are of prime importance.
