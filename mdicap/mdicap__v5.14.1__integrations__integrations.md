<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/integrations -->

# Integrations

## [ICAP URL](/docs/mdicap/v5.14.1/integrations/integrations#icap-url)

| Mode | URL | Example |
| --- | --- | --- |
| Request Modification Mode (REQMOD, OPTIONS) | icap://<IP address>:<port>/OMSScanReq-AV | e.g, icap://10.0.50.36:1344/OMSScanReq-AV |
| Response Modification Mode (RESPMOD, OPTIONS) | icap://<IP address>:<port>/OMSScanResp-AV | e.g, icap://10.0.50.36:1344/OMSScanResp-AV |

## [Validated ICAP Clients](/docs/mdicap/v5.14.1/integrations/integrations#validated-icap-clients)

MetaDefender ICAP Server is *broadly compatible* with any ICAP client which implements the standard ICAP interface. Integration documentation for 3rd party ICAP clients is provided to facilitate deployment but should not be considered exhaustive. Please refer to the documentation provided by your ICAP client software for additional information.

The list below reflects ICAP clients which OPSWAT has tested in-house or on-premise and validated to work with MetaDefender ICAP Server. If your ICAP client is not listed, please consult the documentation provided by the vendor. In most cases, the ICAP Server configuration needed to support an unlisted client is the same as for a validated client in the list below (primarily setting the ICAP Server URL within the ICAP client software - see above).

| Vendor | Product Name | Product Type | Scanning | Sanitized/Redacted content |
| --- | --- | --- | --- | --- |
| [F5](https://www.f5.com) | BigIP LTM | Load Balancer | Yes | Yes |
| [F5](https://www.f5.com) | BigIP ASM | Web Application Firewall | Yes | No |
| [F5](https://www.f5.com) | BigIP SSLO | SSL Inspection | Yes | Yes |
| [Citrix](https://www.citrix.com) | Netscaler ADC VPX | Web Application Firewall | Yes | Yes |
| [VMware](https://www.vmware.com) | Avi Vantage | Web Application Firewall | Yes | Yes |
| [A10 Networks](https://a10networks.com/) | SSLi | SSL Inspection | Yes | Yes |
| [Symantec BlueCoat](https://broadcom.com) | ProxySG | Secure Web Gateway | Yes | Yes |
| [IBM](https://www.ibm.com/docs/en/secure-proxy/6.2.0?topic=scenarios-icap-anti-virus-scanning) | Sterling Secure Proxy | Secure Web Gateway | Yes | Yes |
| [McAfee](https://www.mcafee.com) | Web Gateway | Secure Web Gateway | Yes | Yes |
| [Squid](http://www.squid-cache.org) | Web Gateway | Secure Web Gateway | Yes | Yes |
| [ARA Networks](http://www.aranetworks.com) | Jaguar 5000 | Secure Web Gateway | Yes | Yes |
| [Fortinet](https://www.fortinet.com) | Fortigate | NextGen Firewall | Yes | Yes |
| [Dell EMC](https://www.dell.com) | Isilon | Storage | Yes | No |
| [Nutanix](https://www.nutanix.com) | Files | Storage | Yes | Yes |
| [Huawei](https://www.huawei.com/) | OceanStore (FILEMOD) | Storage | Yes | Yes |
| [GoAnywhere](https://www.goanywhere.com) | Managed File Transfer | Managed File Transfer | Yes | No (can workaround by custom workflow) |
| [Progress](https://www.ipswitch.com/) | MOVEit | Managed File Transfer | Yes | No |
| [Forcepoint](https://www.forcepoint.com/) | Secure Web Gateway | Secure Web Gateway | Yes * | No |
| [Axway](https://www.axway.com/) | B2Bi | Managed File Transfer | Yes | Yes |
| [GlobalScape](https://www.globalscape.com/) | EFT | Managed File Transfer | Yes | Yes |
| [Airlock](https://www.airlock.com/) | Secure Access Hub Gateway | Secure Web Gateway | Yes | Yes |
| [NGINX](https://www.nginx.com/) | NGINX Plus, NGINX Community | Ingress Control | Yes | Yes |
| [Claroty](https://claroty.com/) | Secure Remote Access (SRA) | Remote Access | Yes | Yes |
| [FileCloud](https://www.filecloud.com/) | FileCloud Server | Managed File Transfer | Yes | Yes |
| [Cyolo](https://cyolo.io/) | Secure Remote Access (SRA) | Secure Web Gateway | Yes | No |
| [XONA](https://www.xonasystems.com/) | Critical System Gateway | Secure Remote Access | Yes | No |
| [Checkpoint](https://www.checkpoint.com/) | Security Gateway | NextGen Firewall | Yes | No |
| [Nextcloud](https://nextcloud.com/) | Nextcloud Files | Managed File Transfer | Yes | No |
| [Radware](https://portals.radware.com/ProductDocumentation/Alteon_WBM_Application_Guide_34_5_3_0/Alteon_WBM_Application_Guide/Application%20Redirection_struct.21.24.htm) | Alteon | Web Application Firewall | Yes | No |
| [BlackBerry](https://docs.blackberry.com/en/id-comm-collab/blackberry-workspaces/blackberry-workspaces-server/12_0/administration-guide/gry1443704644720/gry1443704693925) | BlackBerry Workspaces | Enterprise File Sync and Share | Yes |  |

Info

The Forcepoint ICAP client only supports REQMOD (PUT) requests.
