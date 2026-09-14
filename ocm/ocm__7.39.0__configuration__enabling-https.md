<!-- source: https://www.opswat.com/docs/ocm/7.39.0/configuration/enabling-https -->

# Secure Connection

By default, the communication between a product and an OPSWAT Central Management server is not encrypted. If HTTPS is enabled, the server can enforce secure connections between clients and the server on SSL channels. This section describes how to enable SSL for OPSWAT Central Management.

Warning

Please beware that enabling HTTPS on the OPSWAT Central Management server can cause devices that have installed MetaDefender Endpoint to NOT be able to connect to this server. A new MetaDefender Endpoint installer will need to be redownloaded and re-installed on those devices.

## [Requirements](/docs/ocm/7.39.0/configuration/enabling-https#requirements)

In order to enable HTTPS on OPSWAT Central Management server, a trusted certificate issued by a certificate authority provider or a self-signed certificate must be provided.

Please refer to the section below for information on how to install a self-signed server certificate if a trusted certificate is not provided.

## [Enabling HTTPS for OPSWAT Central Management](/docs/ocm/7.39.0/configuration/enabling-https#enabling-https-for-opswat-central-management)

### [Via the management console](/docs/ocm/7.39.0/configuration/enabling-https#via-the-management-console)

To enable HTTPS on OPSWAT Central Management server via the management console :

1. Navigate to **Settings > Server Configuration > SECURITY.**
2. If you have not configured a certificate that you would like to use for secure connections on OPSWAT Central Management, you should follow the below steps to do that; otherwise you can go to step #3.

   1. Click **ADD NEW CERTIFICATE.**
   2. Fill in the required fields. Please beware that the specified files MUST be present on the OPSWAT Central Management server and should not be deleted afterwards; otherwise, OPSWAT Central Management will not start.

      1. **Certificate Name:** The display name of the certificate in the OPSWAT Central Management console.
      2. **Certificate File:** The file path of the certificate file.
      3. **Private Key File:** The file path of the private key file associated with the certificate. The private key must be PKCS8.
      4. **Password File (optional):** The file containing passphrases used to decrypt an encrypted private key file.
   3. Click **ADD**.

Add New Certificate

3. Check **Enable HTTPS**.
4. Select a certificate (added in step 2) that the server should use for secure connections.
5. Select the TLS versions that the server should allow for inbound requests.
6. Click **SAVE.**
7. OPSWAT Central Management will automatically restart and take a few minutes to load the new Secure Connection settings.

Secure Connection Settings

Known issue

Upon saving Secure Connection settings, customized settings in the nginx's configuration file that are not available on the management console, for example **ssl_ciphers**, will be restored to default values.

For Windows, getting the latest Windows Updates may be necessary to use a PKCS8-formatted private key.

Known issue

MetaDefender Core instances cannot download engine packages from OPSWAT Central Management if the latter only has TLSv1.3 enabled.

MetaDefender Core below version 5.4.1 does not support the TLSv1.3 protocol. As a workaround, please enable additional TLS protocols for OPSWAT Central Management.

Known issue

On Red Hat 7 system, TLSv1.3 should not be enabled alone as Red Hat 7 does not have built-in support for TLSv1.3.

If you are unable to access the OPSWAT Central Management console due to this issue, please modify the serverSettings.conf configuration file manually to revert this change.

### [Via the nginx's configuration file](/docs/ocm/7.39.0/configuration/enabling-https#via-the-nginxs-configuration-file)

To enable HTTPS on OPSWAT Central Management server via the nginx's configuration file :

1. Locate the **serverSettings.conf** file in the OPSWAT Central Management installation folder

   1. On Windows: C:\Program Files\OPSWAT\Central\nginx\conf\serverSettings.conf, by default.
   2. On Linux: /opt/ocm/nginx/conf/serverSettings.conf
2. Open the **serverSettings.conf** file for modification.
3. First, add **ssl** to the two listen lines.

   - listen 9000 **ssl;**
   - listen [::]:9000 **ssl**;
4. Then, uncomment the code block starting from **ssl_certificate** to **error_page** by removing **#** at the beginning of each line.
5. Finally, update the correct file paths for the certificate files

   1. <PATH_TO_CERT_FILE> with the file path of the certificate file, for example "C:\OCM_Keys\your.crt> C:\OCM_Keys\your.crt"
   2. <PATH_TO_KEY_FILE> with the file path of the certificate key file, for example: "C:\OCM_Keys\your.key"
   3. **(Optional)** ssl_ciphers determines the cipher suites used by nginx. The default configuration uses a macro that prefer cipher suites that supports forward secrecy.

listen 9000 ssl;
listen [::]:9000 ssl;
##############################################################
# Configuring HTTPS servers in here
#
ssl_certificate <PATH_TO_CERT_FILE>;
ssl_certificate_key <PATH_TO_KEY_FILE>;
ssl_protocols TLSv1.2 TLSv1.3;
ssl_ciphers EECDH+ECDSA+AESGCM:EECDH+aRSA+AESGCM:EECDH+ECDSA+SHA256:EECDH+aRSA+SHA256:EECDH+ECDSA+SHA384:EECDH+ECDSA+SHA256:EECDH+aRSA+SHA384:EDH+aRSA+AESGCM:EDH+aRSA+SHA256:EDH+aRSA:EECDH:!aNULL:!eNULL:!MEDIUM:!LOW:!3DES:!MD5:!EXP:!PSK:!SRP:!DSS:!RC4:!SEED;
ssl_session_cache shared:SSL:10m;
ssl_session_timeout 10m;
error_page 497 https://$host:$server_port$request_uri;
#
##############################################################Warning

On Windows system, using the standard Windows path separator backslash **** may have unexpected results if the file path contains directories or file names that start with certain special characters such as **'\n'** or **'\t'**. The reason is that these characters are interpreted as special characters by nginx.

For example, the following directive:

`ssl_certificate "C:\OCM_Keys\nginx\your.crt";`

will be interpreted by nginx as:

`ssl_certificate "C:\OCM_Keys`

`ginx\your.crt";`

As a workaround solution, instead of backslash (), please use:

1. Forward slash '/' or
2. Double backslash ''.

For example:

`ssl_certificate "C:\\OCM_Keys\\nginx\\your.crt";`

3. Restart the OPSWAT Central Management server by clicking the **Restart** menu on the OPSWAT Central Management tray icon.
4. After the service is restarted, open the OPSWAT Central Management console, for example [**https://localhost:9000**](https://localhost:9000), to check whether the console can be loaded successfully
5. Click **SAVE** to save changes.

Upgrade from version 7.2.0

OPSWAT Central Management version 7.2.0 or earlier stores the HTTPS configuration in nginx.conf. If you are upgrading from one such version to 7.2.0 or above, the installer should automatically generate ssl.conf from your modified nginx.conf file and reset nginx.conf to its default state. In case the generation process failed and the default ssl.conf is installed instead, please follow the instructions below to recover your HTTPS configuration.

1. Navigate to nginx configuration backup folder (located in C:\ProgramData\OPSWAT\Central\bak, by default).
2. Locate the nginx.conf file
3. Locate the HTTPS configuration block to enable HTTPs via nginx above.
4. Copy the configuration block to the active ssl.conf file (located in C:\Program Files\OPSWAT\Central\nginx\conf, by default).
5. Restart OPSWAT Central Management to apply new settings.
Upgrade from version 7.34.0

OPSWAT Central Management version 7.3.0 to 7.34.0 stores the HTTPS configuration in ssl.conf.

From version 7.35.0, the HTTPS configuration is now stored in serverSettings.conf.

If you are upgrading to 7.35.0 or above, the setup should automatically update serverSettings.conf from your modified ssl.conf file. In case the generation process failed and the default serverSettings.conf is installed instead, please follow the instructions below to recover your HTTPS configuration.

1. Navigate to nginx configuration backup folder

   1. On Windows: C:\ProgramData\OPSWAT\Central\bak, by default.
   2. On Linux: /etc/opt/ocm
2. Locate the ssl.conf file
3. Locate the HTTPS configuration block to enable HTTPs via nginx above.
4. Refer to the configuration block to edit the active serverSettings.conf file

   1. On Windows: C:\Program Files\OPSWAT\Central\nginx\conf\serverSettings.conf, by default.
   2. On Linux: /opt/ocm/nginx/conf/serverSettings.conf
5. Restart OPSWAT Central Management to apply new settings.
## [Disabling HTTPS configuration](/docs/ocm/7.39.0/configuration/enabling-https#disabling-https-configuration)

### [Via the management console](/docs/ocm/7.39.0/configuration/enabling-https#via-the-management-console)

To disable HTTPS on OPSWAT Central Management server via the management console :

1. Navigate to **Settings > Server Configuration > SECURITY.**
2. Uncheck **Enable HTTPS.**
3. Click **SAVE**.
4. OPSWAT Central Management will automatically restart and take a few minutes to load the new Secure Connection settings.

Updating Server URL

Upon disabling the HTTPS configuration, the [Server URL](/docs/ocm/7.39.0/configuration/setting-up-domain) will be automatically changed to use the **http://** prefix. For certain network configurations where HTTPS access is provided externally (such as via a reverse proxy), the Server URL will need to be manually configured to use the **https://** prefix.

### [Via the nginx's configuration file](/docs/ocm/7.39.0/configuration/enabling-https#via-the-nginxs-configuration-file)

To disable HTTPS on OPSWAT Central Management server via the nginx's ssl.conf configuration file :

1. Locate the serverSettings.conf file in the OPSWAT Central Management installation folder

   1. On Windows: C:\Program Files\OPSWAT\Central\nginx\conf\serverSettings.conf, by default
   2. On Linux: /opt/ocm/nginx/conf/serverSettings.conf
2. Open the serverSettings.conf file for modification.
3. Remove **ssl** from the two listen lines.

   - listen 9000;
   - listen [::]:9000;
4. Restart the OPSWAT Central Management server by clicking the **Restart** menu on the OPSWAT Central Management tray icon.
5. After the service is restarted, open the OPSWAT Central Management console, for example [**http://localhost:9000**](http://localhost:9000), to check whether the console can be loaded successfully.

   - Please note that HTTP Strict Transport Security enabled, you may still be redirect to <https://localhost:9000>, which now no longer exists.
6. Update the [Server URL](/docs/ocm/7.39.0/configuration/setting-up-domain) to match the new settings if needed.
7. Click **SAVE** to save changes.

listen 9000;
listen [::]:9000;
##############################################################
# Configuring HTTPS servers in here
#
ssl_certificate <PATH_TO_CERT_FILE>;
ssl_certificate_key <PATH_TO_KEY_FILE>;
ssl_protocols TLSv1.2 TLSv1.3;
ssl_ciphers EECDH+ECDSA+AESGCM:EECDH+aRSA+AESGCM:EECDH+ECDSA+SHA256:EECDH+aRSA+SHA256:EECDH+ECDSA+SHA384:EECDH+ECDSA+SHA256:EECDH+aRSA+SHA384:EDH+aRSA+AESGCM:EDH+aRSA+SHA256:EDH+aRSA:EECDH:!aNULL:!eNULL:!MEDIUM:!LOW:!3DES:!MD5:!EXP:!PSK:!SRP:!DSS:!RC4:!SEED;
ssl_session_cache shared:SSL:10m;
ssl_session_timeout 10m;
error_page 497 https://$host:$server_port$request_uri;
#
##############################################################
## [Enable HTTP Strict Transport Security](/docs/ocm/7.39.0/configuration/enabling-https#enable-http-strict-transport-security)

HTTP Strict Transport Security (HSTS) enforces the use of HTTPS protocol for all incoming connections. To enable HSTS for OPSWAT Central Management, please follow the below steps:

1. Locate the **ssl.conf** file in the OPSWAT Central Management installation folder

   1. On Windows: C:\Program Files\OPSWAT\Central\nginx\conf\ssl.conf, by default.
   2. On Linux: /opt/ocm/nginx/conf, by default.
2. Locate the configuration line **add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;**

   1. If that line exists but starts with a comment sign (#), remove the comment sign.
   2. If that line does not exist, add it to the bottom of the configuration file.
3. Restart the OPSWAT Central Management server by clicking the **Restart** menu on the OPSWAT Central Management tray icon.
