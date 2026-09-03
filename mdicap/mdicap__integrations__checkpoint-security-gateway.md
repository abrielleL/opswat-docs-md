<!-- source: https://www.opswat.com/docs/mdicap/integrations/checkpoint-security-gateway -->

# Check Point Security Gateway

## [Prerequisites](/docs/mdicap/integrations/checkpoint-security-gateway#prerequisites)

This documentation is based on Check Point Security Gateway R81 and is the minimum configuration required to integrate Check Point and MetaDefender ICAP Server. For more information, please contact [Check Point Support](https://support.checkpoint.com/).

- Check Point Security Gateway R81 and above
- MetaDefender ICAP Server v5.x (or later) is installed and license is activated
- For installation and configuration quick guidelines see:

  - 1. Quick Start with MetaDefender ICAP Server
  - 2. Installing or Upgrading MetaDefender ICAP Server
  - [3. Configuring Metadefender ICAP Server](/docs/mdicap/configuration/metadefender-icap-server-configuration)
  - 4.MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [MetaDefender ICAP Server Licensing](/docs/mdicap/installation/metadefender-icap-server-licensing)
- MetaDefender Core is installed and license is activated
- Command line access to Check Point Security Gateway - [Expert Mode](https://sc1.checkpoint.com/documents/R81/WebAdminGuides/EN/CP_R81_Gaia_AdminGuide/Topics-GAG/Expert-Mode.htm). Please refer to the Check Point documentation for details on how to access the command line.

## [Integration Steps](/docs/mdicap/integrations/checkpoint-security-gateway#integration-steps)

- Access the command line in Expert mode
- Review and agree to the ICAP user-disclaimer

CommandCopy[Expert@GW:0]# IcapDisclaimer.sh

- Backup the default ICAP configuration file

CommandCopy[Expert@GW:0]# cp -v $FWDIR/conf/icap_client_blade_configuration.C{,_BKP}

- Configure the ICAP Client parameters in the configuration file

CommandCopy[Expert@GW:0]# vi $FWDIR/conf/icap_client_blade_configuration.C

- Save the configuration

CommandCopy[Expert@GW:0]# fw fetch localhost
## [Sample ICAP Client configuration file](/docs/mdicap/integrations/checkpoint-security-gateway#sample-icap-client-configuration-file)

The sample configuration provided below is for reference only and must be modified according to the network environment and ICAP funcitonality . The configuration will enable REQMOD with GET, PUT and POST methods for port 8080 and 8443 traffic. The variable *src_ip_ranges* has also been configured for network-level filtering. Please refer to the Check Point documentation for more information on the [ICAP client configuration file](https://sc1.checkpoint.com/documents/R81/WebAdminGuides/EN/CP_R81_ThreatPrevention_AdminGuide/Topics-TPG/ICAP_Client_Configuration_File.htm).

TextCopy(
:enabled ("true")
:filter_http_method (
: (
:method ("GET")
)
: (
:method ("PUT")
)
: (
:method ("POST")
)
)
:http_services (
: (
:port (8080)
)
: (
:port (8443)
)
)
:inspect_html_response ("false")
:trickling_mode (2)
:user_check_interaction_name ("Blocked Message - Access Control")
:log_level (3)
:icap_servers (
: (
:name ("icap_server_1")
:ip ("10.1.0.20") ********* (OPSWAT ICAP SERVER - IP only)
:ip6 ("2001:db8:6:f101::15")
:port (1344)
:service ("echo") # “reqmod” or “echo”
:proto ("icap")
:modification_mode (“reqmod”) # “reqmod” or ”both”
:transp ("3rd_cpas")
:failmode (open)
:timeout (60)
:max_conns (50)
:user_check_action (1)
:x_headers (
:x_client_ip ("false")
:x_server_ip ("false")
:x_authenticated_user (“true”)
:authentication_source ("Local")
:base64_username_encode ("true")
)
)
)
:rules_type ("include")
:network_filter_rules_ip4 (
: (
:src_ip_ranges (
: (
:min_ip ("10.0.0.6")
:max_ip ("10.0.0.10")
)
)
:dst_ip_ranges (
: (
:min_ip (“any”)
:max_ip (“any”)
)
)
)
)
:network_filter_rules_ip6 (
: (
:src_ip_ranges (
: (
:min_ip ("")
:max_ip ("")
)
)
:dst_ip_ranges (
: (
:min_ip ("")
:max_ip ("")
)
)
)
)
)
## [Additional Configuration](/docs/mdicap/integrations/checkpoint-security-gateway#additional-configuration)

To include X-Headers in ICAP requests, you must enable Identity Awareness in the Check Point Security Gateway UI, General Properties, Network Security tab:

To enable inspection of SSL-encrypted traffic, import the SSL certificate using the Check Point Security Gateway UI: **HTTPS Inspection**.
