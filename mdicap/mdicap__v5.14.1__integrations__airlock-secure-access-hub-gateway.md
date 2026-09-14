<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/airlock-secure-access-hub-gateway -->

# Airlock Secure Access Hub Gateway

This documentation is based on Airlock Secure Access Hub Gateway v7.8 and is the minimum configuration required to integrate Airlock Gateway and MetaDefender ICAP Server. For more information, please consult the Airlock documentation here[: https://docs.airlock.com/gateway/7.8/#data/configureica.html](https://docs.airlock.com/gateway/7.8/#data/configureica.html)

## [Prerequisites](https://docs.opswat.com/mdicap/integrations/citrix-adc-vpx#prerequisites)

- Airlock Gateway is installed and licensed
- MetaDefender ICAP Server is installed and license is activated
- For installation and configuration quick guidelines see:

  - [1. Quick Start with MetaDefender ICAP Server](metadefender-icap-server/v5.1.1/installation/installation)
  - [2. Installing or Upgrading MetaDefender ICAP Server](metadefender-icap-server/v5.1.1/installation/installing-or-upgrading-metadefender-icap-server)
  - [3. Configuring MetaDefender ICAP Server](metadefender-icap-server/v5.1.1/configuration/metadefender-icap-server-configuration)
  - 4. MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [MetaDefender ICAP Server Licensing](metadefender-icap-server/v5.1.1/installation/metadefender-icap-server-licensing).
- MetaDefender Core is installed and license is activated
- Web browser access to the Airlock Gateway web GUI. (Please refer to the Airlock documentation for details on how to access the Airlock GUI. This guide was written with a presumption that you have already completed the device management configuration on the Airlock Gateway device and it is currently functioning properly as a proxy.

## [Integration Steps](https://docs.opswat.com/mdicap/integrations/citrix-adc-vpx#integration-steps)

In the Airlock Secure Access Hub Gateway GUI, navigate to **System Setup** -> **Network Services:**

In Network Services page, add an ICAP Server under **ICAP Server – Antivirus, SOAP/XML filtering, etc.:**

- In the **Name** field, add an identifiable name for the ICAP Server. You will use this name when mapping to your WAF in later steps.
- In the **ICAP Service URL** field, input the URL of the MetaDefender ICAP Server. By default, MetaDefender ICAP Server uses the standard port 1344.

In the Airlock Secure Access Hub Gateway GUI, navigate to **Application Firewall** -> **Reverse Proxy:**

In the Reverse Proxy page, select **Mapping:**

In the **ICAP Request Client View** section of the **ICAP** tab, select the ICAP server name specified in earlier steps. This maps the ICAP Server network service to the reverse proxy.

## [ICAP Client Compatibility](/docs/mdicap/v5.14.1/integrations/airlock-secure-access-hub-gateway#icap-client-compatibility)

Airlock Secure Access Hub Gateway supports all of the scan methods available in MetaDefender Core:

- Multiscanning
- Deep CDR
- Proactive DLP
- Vulnerability Assessment
