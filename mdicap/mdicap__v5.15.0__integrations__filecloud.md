<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/integrations/filecloud -->

# FileCloud

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This documentation is based on FileCloud version 23.1 and is the minimum configuration required to integrate with MetaDefender ICAP Server. For more information, please consult the FileCloud documentation available here: [https://www.filecloud.com/supportdocs/fcdoc/23.1client/server/filecloud-administrator-guide/third-party-integrations-settings/enable-antivirus-scanning/use-icap-antivirus-scanning](https://docs.airlock.com/gateway/7.8/#data/configureica.html)

## [Prerequisites](https://docs.opswat.com/mdicap/integrations/citrix-adc-vpx#prerequisites)

- FileCloud is installed and licensed
- MetaDefender ICAP Server is installed and license is activated

  - For installation and configuration quick guidelines see:

    - [1. Quick Start with MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/installation)
    - [2. Installing or Upgrading MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/installing-or-upgrading-metadefender-icap-server)
    - [3. Configuring MetaDefender ICAP Server](https://docs.opswat.com/metadefender-icap-server/v5.1.1/configuration/metadefender-icap-server-configuration)
    - 4. MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [MetaDefender ICAP Server Licensing](https://docs.opswat.com/metadefender-icap-server/v5.1.1/installation/metadefender-icap-server-licensing).
- MetaDefender Core is installed and license is activated
- Web browser access to the FileCloud Admin Portal. (Please refer to the FileCloud documentation for details on how to access the FileCloud Admin Portal. This guide was written with a presumption that you have already completed the initial setup and configuration of FileCloud.

## [Integration Steps](https://docs.opswat.com/mdicap/integrations/citrix-adc-vpx#integration-steps)

1. Open a browser and log on to the FileCloud *Admin Portal*.
2. On the left navigation panel, click *Settings*.
3. Select the *Third Party Integrations* tab.
4. In the *Anti-Virus* tab, from the Anti-Virus type drop down list, select *ICAP AV*.

5. Configure the following fields:

   1. Server Local IP address (in most cases, leave the default value of 0.0.0.0. If you are using a separate FileCloud policy with ICAP, enter the Private (LAN) IP of the FileCloud server. Please consult FileCloud documentation for more information).
   2. ICAP Remote Hostname - the IP or hostname of the ICAP server.
   3. ICAP Port - by default this is 1344.

6. If using SSL/TLS on the ICAP Server, check the Secure ICAP checkbox.

7. File Size Limit - by default this is set to 25MB. To scan larger files, increase this value.

8. Configure the ICAP Service Name with OMSScanReq-AV.

9. Configure debug logging if required.

10. Click Save, then click the ICAP Test button at top of the page to test the configuration.
