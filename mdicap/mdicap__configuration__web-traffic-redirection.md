<!-- source: https://www.opswat.com/docs/mdicap/configuration/web-traffic-redirection -->

# Web traffic redirection

View as Markdown Ask ChatGPT about this page Ask Claude about this page

As a final step –when all the previous steps in this chapter are done– the web traffic must be redirected to flow through MetaDefender ICAP Server.

Info

MetaDefender ICAP Server's ICAP service is listening on port 1344 by default.

For further details about integrating MetaDefender ICAP Server with various ICAP clients see [4.4 Web Proxy Integrations](/docs/mdicap/integrations/integrations) and [4.5 Other Integration](/docs/mdicap/integrations/integrations).

## [Example](/docs/mdicap/configuration/web-traffic-redirection#example)

In case of Squid proxy installed on the same machine as ICAP Server the following configuration must be appended to the squid.conf file:

Sqiud example
icap_enable on
icap_send_client_ip on
icap_preview_enable on
icap_preview_size 0
icap_service_failure_limit -1
icap_service metascan_req reqmod_precache bypass=0 icap://127.0.0.1:1344/OMSScanReq-AV
adaptation_access metascan_req allow all
icap_service metascan_resp respmod_precache bypass=0 icap://127.0.0.1:1344/OMSScanResp-AV
adaptation_access metascan_resp allow all
icap_persistent_connections on
