<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/cyolo-pro -->

# Cyolo PRO

This documentation is based on Cyolo PRO v4.3 and is the minimum configuration required to integrate the Cyolo Secure Remote Access (SRA) solution and MetaDefender ICAP Server. For more information, please consult the Cyolo documentation here: <https://support.cyolo.io/hc/en-us/articles/15538536132241-File-Scan-Integration-Using-ICAP>

## [Prerequisities](/docs/mdicap/v5.14.1/integrations/cyolo-pro#prerequisities)

- Cyolo PRO v4.3 or greater is installed and licensed
- MetaDefender ICAP Server v5.x or greater is installed and license is activated
- For installation and configuration quick guidelines see:

  - [1. Quick Start with MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/installation)
  - [2. Installing or Upgrading MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/installing-or-upgrading-metadefender-icap-server)
  - [3. Configuring MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/configuration/metadefender-icap-server-configuration)
  - 4. MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [MetaDefender ICAP Server Licensing](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/metadefender-icap-server-licensing).
- MetaDefender Core v5.x or greater is installed and license is activated
- Web browser access to the Cyolo web GUI. (Please refer to the Cyolo documentation for details on how to access the Cyolo GUI. This guide was written with a presumption that you have already completed the device management configuration on the Cyolo SRA device and it is currently functioning properly as a proxy.

## [Integration Steps](/docs/mdicap/v5.14.1/integrations/cyolo-pro#integration-steps)

In the Cyolo UI, navigate to **Integrations** --> **ICAP**.

Select **Add** to create a new ICAP server, or edit an existing connection if applicable.

### [**Configuration**](/docs/mdicap/v5.14.1/integrations/cyolo-pro#configuration)

- **Server Name:** Input a descriptive name for the MetaDefender ICAP Server.
- **Sites:** Choose the sites which will utilize the ICAP connection.
- **Host**: The IP of the MetaDefender ICAP Server.
- **Max File Size:** User selected. Note that you can also set file size limits within MetaDefender.
- **Port:** The default port is 1344 for non-SSL connections. The default port is 11344 for SSL connections.
- **Service Name:** OMSScanReq-AV

Once you have entered the information, click **Done**.

#### [ICAP Client Compatibility](/docs/mdicap/v5.14.1/integrations/cyolo-pro#icap-client-compatibility)

Info

Cyolo PRO supports multiscanning only. It does not currently support receiving modified content in the response (e.g. files sanitized by CDR or files redacted by DLP).
