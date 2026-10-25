<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg -->

# Symantec Blue Coat ProxySG

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Prerequisites](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#prerequisites)

- [Configuring MetaDefender ICAP Server](https://app.developerhub.io/metadefender-icap-server/v5.14.1/configuration/metadefender-icap-server-configuration)
- [Enable persistent connections](/docs/mdicap/v5.15.0/configuration/other-settings) (recommended) - Blue Coat is reusing connections to the ICAP server, so it is highly recommended to enable persistent connections on the ICAP side or the Blue Coat might detect some ICAP connection drop errors under high load.

### [ProxySG Management Console](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#proxysg-management-console)

The ProxySG configuration should be done from the ProxySG Management Console interface. Below is the minimum configuration required for MetaDefender ICAP Server integration with ProxySG. Please refer to the ProxySG manual for advanced proxy configuration. Open a web browser and load the ProxySG Management Console. (Please refer to the ProxySG manual for details about how to open the [ProxySG Management Console](https://bto.bluecoat.com/sites/default/files/tech_briefs/Generic_ICAP_Integation.4.pdf).) The ProxySG configuration should be done from the ProxySG Management Console interface. Below is the minimum configuration required for MetaDefender Core ICAP integration with ProxySG. Please refer to the ProxySG manual for advanced proxy configuration. Open a web browser and load the ProxySG Management Console. (e.g. https://<ip address>:8082 Please refer to the ProxySG manual for details about how to open the ProxySG Management Console.)

### [Disable Automatic Cache Refresh](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#disable-automatic-cache-refresh)

1. Select the 'Freshness' tab and select the 'Disable refreshing' option
2. Select the 'Acceleration Profile' tab and uncheck the following options

   1. Pipeline embedded objects in client request
   2. Pipeline redirects for client request
   3. Pipeline embedded objects in prefetch request
   4. Pipeline redirects for prefetch request
3. Click 'Apply' to save these settings

### [Adding REQMOD Service (Upload Mode)](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#adding-reqmod-service-upload-mode)

1. Within the 'Configuration' tab, navigate to 'External Services'->'ICAP'
2. Click 'New'
3. Enter a service name for the Metascan service (in this example we use 'MetascanReqmod') and click 'OK'
4. In the services list, select 'MetascanReqmod' and click 'Edit'
5. Update the following values

   1. In ICAP Service

      1. Set Service URL to 'icap://<Metascan Server>/OMSScanReq-AV'
      2. Select 'Use vendor's "virus found" page'
   2. In ICAP Service Ports

      1. Check 'This service supports plain ICAP connections
      2. Set the 'Plain ICAP port' value to your Metascan's ICAP port (1344 by default)
   3. In ICAP v1.0 Options

      1. Check 'Request modification'
      2. Check 'Send Client address'
6. Click 'OK'
7. Click 'Apply' to save the configuration

### [Adding RESPMOD Service (Download Mode)](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#adding-respmod-service-download-mode)

1. Within the 'Configuration' tab, navigate to 'External Services'->'ICAP'
2. Click 'New'
3. Enter a service name for the Metascan service (in this example we use 'MetascanRespmod') and click 'OK'
4. In the services list, select 'MetascanReqmod' and click 'Edit'
5. Update the following values

   1. In ICAP Service

      1. Set Service URL to 'icap://<Metascan Server>/OMSScanResp-AV'
      2. Select 'Use vendor's "virus found" page'
   2. In ICAP Service Ports

      1. Check 'This service supports plain ICAP connections
      2. Set the 'Plain ICAP port' value to your Metascan's ICAP port (1344 by default)
   3. In ICAP v1.0 Options

      1. Check 'Response modification'
      2. Check 'Send Client address'
6. Click 'OK'
7. Click 'Apply' to save the configuration

### [Create MetaDefender REQMOD Policy](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#create-metadefender-reqmod-policy)

1. Within the 'Configuration' tab, navigate to 'Policy'->'Visual Policy Manager'
2. Click the 'Launch' button
3. In the 'Blue Coat Visual Policy Manager' window, navigate to 'Policy'->'Add Web Content Layer'
4. Enter a layer name (in this example we use 'MetaDefender ICAP Server ReqMod') and click 'OK'
5. In the newly created 'MetaDefender ICAP Server ReqMod' tab, right click on 'Use Default Caching' and choose 'Set...'
6. In the 'Set Action Object' window, click 'New' and select 'Set ICAP Request Service...'
7. In the 'Add ICAP Request Service Object' window, set the following values

   1. Set 'name' to 'MetaDefender ICAP Server Request Service'
   2. In 'Available services', select 'MetascanReqMod' and click 'Add'
8. Click 'OK' to finish and 'Apply' to save

### [Create MetaDefender RESPMOD Policy](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#create-metadefender-respmod-policy)

1. Within the 'Configuration' tab, navigate to 'Policy'->'Visual Policy Manager'
2. Click the 'Launch' button
3. In the 'Blue Coat Visual Policy Manager' window, navigate to 'Policy'->'Add Web Content Layer'
4. Enter a layer name (in this example we use 'MetaDefender ICAP Server RespMod') and click 'OK'
5. In the newly created 'MetaDefender ICAP Server RespMod' tab, right click on 'Use Default Caching' and choose 'Set...'
6. In the 'Set Action Object' window, click 'New' and select 'Set ICAP Response Service...'
7. In the 'Add ICAP Response Service Object' window, set the following values

   1. Set 'name' to 'MetaDefender ICAP Server Response Service'
   2. In 'Available services', select 'MetascanRespMod' and click 'Add'
8. Click 'OK' to finish and 'Apply' to save

## [Configure Blue Coat SSL](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#configure-blue-coat-ssl)

### [Enabling Blue Coat To Intercept SSL traffic](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#enabling-blue-coat-to-intercept-ssl-traffic)

By default SSL (HTTPS) connections are not intercepted by Blue Coat and therefore data in them are not scanned by the MetaDefender ICAP Server. If you would like to scan files which were sent using secure connection, then you can optionally configure Blue Coat to decrypt SSL connections.

### [How To Configure](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#how-to-configure)

Please refer to [Blue Coat documentation](https://bto.bluecoat.com/webguides/proxysg/security_first_steps/index.htm#Solutions/SSL/ssl_solution.htm).

### [Limitations](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#limitations)

- If the ICAP server is not connected directly to Blue Coat or it is not in a private network, then the connection between Blue Coat and ICAP won't be secure anymore and the decrypted data could be in danger. (<https://symwisedownload.symantec.com/resources/sites/SYMWISE/content/live/DOCUMENTATION/11000/DOC11474/en_US/SGOSAdmin71.pdf> "Securing access to an ICAP Server")
- Valid SSL certificates are needed for Blue Coat and user experience could be altered by certification notifications.

### [How to overcome certificate issues](/docs/mdicap/v5.15.0/integrations/symantec-blue-coat-proxysg#how-to-overcome-certificate-issues)

1. When creating a keyring and certificate explained in the [Blue Coat documentation](https://bto.bluecoat.com/webguides/proxysg/security_first_steps/index.htm#Solutions/SSL/ssl_solution.htm) please give attention to that the **Common name***"must match the ProxySG name or IP address that the client expects"*
2. After the keyring and the certificate is ready go to **Statics → Advanced → SSL → Download a ProxySG Certificate as a CA certificate** in ProxySG Management Console
3. Select the previously created certificate and download/install it to the browser in use
4. This certificate should be set under **Proxy Settings → SSL Proxy** and under the **SSLInterception** which was created during configuring SSL interception
