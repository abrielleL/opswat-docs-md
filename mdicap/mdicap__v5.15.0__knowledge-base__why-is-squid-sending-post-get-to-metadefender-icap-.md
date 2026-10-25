<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/why-is-squid-sending-post-get-to-metadefender-icap- -->

# Why is Squid sending POST/GET to MetaDefender ICAP?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender ICAP Server 5.4.0 and above releases deployed on Windows and Linux systems.

By default, Squid does not issue ICAP requests using REQMOD or RESPMOD unless these are explicitly configured. This can cause Squid to send plain HTTP methods (e.g., GET, POST) to the ICAP server, which expects ICAP-specific requests and responses. Additionally, when using Firefox with Squid, misconfigured SOCKS proxy settings can cause similar “400 Bad Request” errors.

#### [Why this matters for MetaDefender ICAP Server](/docs/mdicap/v5.15.0/knowledge-base/why-is-squid-sending-post-get-to-metadefender-icap-#why-this-matters-for-metadefender-icap-server)

MetaDefender ICAP only processes traffic sent with ICAP methods. When improperly configured, Squid may simply pass traffic through without modification or in some cases (like Squid 5.x defaults), send plain HTTP methods (GET/POST) to the ICAP port. This is what leads to the “400 Bad Request” errors.

### [**Legacy Squid 3.x Configuration:**](/docs/mdicap/v5.15.0/knowledge-base/why-is-squid-sending-post-get-to-metadefender-icap-#legacy-squid-3x-configuration)

HtmlCopyicap_enable on
icap_send_client_ip on
icap_send_client_username on
icap_preview_enable on
icap_preview_size 1024
icap_service service_req reqmod_precache 0 icap://<MetaDefender ICAP Server>:1344/reqmod
icap_service service_resp respmod_precache 0 icap://<MetaDefender ICAP Server>:1344/respmod
icap_class class_avreq service_req
icap_class class_avresp service_resp
icap_access class_avreq allow all
icap_access class_avresp allow all
### [**Squid 5.x / 6.x / 7.x Configuration**](/docs/mdicap/v5.15.0/knowledge-base/why-is-squid-sending-post-get-to-metadefender-icap-#squid-5x--6x--7x-configuration)

HtmlCopyicap_enable on
icap_send_client_ip on
icap_preview_enable on
icap_preview_size 0
icap_service metascan_req reqmod_precache bypass=0 icap://<MetaDefender ICAP Server>:1344/reqmod
adaptation_access metascan_req allow all
icap_service metascan_resp respmod_precache bypass=0 icap://<MetaDefender ICAP Server>:1344/respmod
adaptation_access metascan_resp allow all
#### [Firefox SOCKS Proxy Settings Solution](/docs/mdicap/v5.15.0/knowledge-base/why-is-squid-sending-post-get-to-metadefender-icap-#firefox-socks-proxy-settings-solution)

When using Firefox through a Squid proxy connected to an ICAP server, misconfigured SOCKS proxy settings can cause “400 Bad Request” errors in the ICAP workflow. This happens because Firefox, when set to use a SOCKS proxy, may tunnel all traffic (including HTTP) over the SOCKS protocol instead of sending plain HTTP to Squid. Squid then receives traffic in an unexpected format, which prevents it from applying ICAP services properly and leads to protocol errors.

To avoid this, ensure that Firefox is configured to send HTTP/S traffic directly to Squid’s listening IP and port (e.g., HTTP Proxy: <squid-ip>, Port: 3128) without enabling SOCKS. If SOCKS is enabled but unnecessary, disable it by clearing the “SOCKS Host” field and unchecking “Proxy DNS when using SOCKS” in Firefox’s network settings. This ensures that Squid receives standard HTTP requests, allowing it to correctly pass them to the ICAP server using REQMOD or RESPMOD.

Please Note:

There is a known bug in Squid versions 5.5 through 6.11, where using RESPMOD fails for files larger than ~65KB. It’s recommended is to instead use Squid 4.13, 6.13, or 7.0.1

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
