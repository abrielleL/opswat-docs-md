<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/nextcloud-files -->

# Nextcloud Files

This documentation is based on Nextcloud Files version 30 and is the minimum configuration required to integrate with MetaDefender ICAP Server. For more information, please consult the Nextcloud [documentation](https://nextcloud.com/support/).

## [Prerequisites](/docs/mdicap/v5.14.1/integrations/nextcloud-files#prerequisites)

- Nextcloud is installed
- Nextcloud app Antivirus for Files is installed. More information is available [here](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/antivirus_configuration.html).
- MetaDefender ICAP Server is installed and license is activated

  - For installation and configuration quick guidelines see:

    - [1. Quick Start with MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/installation)
    - [2. Installing or Upgrading MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/installing-or-upgrading-metadefender-icap-server)
    - [3. Configuring MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/configuration/metadefender-icap-server-configuration)
    - 4. MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [MetaDefender ICAP Server Licensing](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/metadefender-icap-server-licensing).
- MetaDefender Core is installed and license is activated
- Web browser access to the Nextcloud admin portal. This guide was written with a presumption that you have already completed the initial setup and configuration of Nextcloud.

## [Integration Steps](/docs/mdicap/v5.14.1/integrations/nextcloud-files#integration-steps)

In the Nextcloud Antivirus for Files app, update the fields highlighted below:

- Host: The IP address of the MetaDefender ICAP Server
- Port: Default ICAP protocol port = 1344
- ICAP Mode: REQMOD
- ICAP Service: OMSScanReq-AV
- Stream length: This value sets the maximum number of bytes to send (maximum file size). The setting 1073741824000 bytes sets a maximum file size of 1 TB. This setting must be lower than the value set with *memory_limit* settings, or physical memory if no *memory_limit* is set.

For more information on configuring Nextcloud Files, please see the [Nextcloud configuration guide](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/antivirus_configuration.html).

## [Additional Information](/docs/mdicap/v5.14.1/integrations/nextcloud-files#additional-information)

NOTE

The Nextcloud ICAP client (Antivirus for Files) does not currently send the filename when making ICAP requests. Thus, file names will not be displayed within the MetaDefender ICAP Server or MetaDefender Core Processing History.

NOTE

The Nextcloud ICAP client (Antivirus for Files) does not support receiving modified content in the response. See [here](https://github.com/nextcloud/files_antivirus/issues/271) for more information.
