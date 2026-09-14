<!-- source: https://www.opswat.com/docs/mdcloud/integrations/metadefender-icap-cloud -->

# MetaDefender ICAP Cloud

In addition to the standard on-premise MetaDefender ICAP Server, OPSWAT also offers a SaaS-based ICAP service, hosted alongside our MetaDefender Cloud SaaS.

## [Integration Requirements](/docs/mdcloud/integrations/metadefender-icap-cloud#integration-requirements)

Integrating your ICAP client (load balancer, WAF, ingress controller, etc) with MetaDefender ICAP Cloud follows the same process as integrating with an ICAP server hosted on-premise. However, there are a few extra steps required to authenticate and secure the communication.

### [Connection Information](/docs/mdcloud/integrations/metadefender-icap-cloud#connection-information)

#### [Domain](/docs/mdcloud/integrations/metadefender-icap-cloud#domain)

[https://icap.metadefender.com](https://icap.metadefender.com/)

#### [Ports](/docs/mdcloud/integrations/metadefender-icap-cloud#ports)

To create a secure connection between your network and MetaDefender ICAP Cloud, the following ports are used:

- 11344 - for standard ICAP clients using ICAP protocol (TLS-enabled ICAPS)
- 8543 - for NGINX integration using HTTPS (TLS-enabled)

## [Authentication](/docs/mdcloud/integrations/metadefender-icap-cloud#authentication)

To authenticate to the MetaDefender ICAP Cloud service, a custom X-header will need to be added to allow access to the API: **X-MDCLOUD-APIKEY.** The value of the key will be the API Key received from [My OPSWAT](https://docs.opswat.com/mdcloud/integrations/onboarding-process-for-metadefender-cloud-api-users#create-a-new-opswat-account). Depending on the type of integration, add the custom header as required:

- HTTP header or ICAP header when integrating with a traditional ICAP client, or...
- HTTPS request header when integrating with NGINX

Please consult the documentation for your ICAP client (the integrated network security device) for information on adding this header.

## [Filtering](/docs/mdcloud/integrations/metadefender-icap-cloud#filtering)

Unlike the traditional MetaDefender ICAP Server, where licensing is per instance, MetaDefender ICAP Cloud is a consumption-based licensing model which counts each object scanned against the purchased limit. Depending on the configuration of your web application, you may need to add filtering rules to your network security device to limit which files are being sent for scanning.

For example, you may want to limit .txt or .html files from being scanned, as they count against your consumption, but since they are text-based files, are not scanned.

Please consult the the documentation for your ICAP client (the integrated network security device) for information on adding filtering rules.
