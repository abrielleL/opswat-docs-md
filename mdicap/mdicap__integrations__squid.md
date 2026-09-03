<!-- source: https://www.opswat.com/docs/mdicap/integrations/squid -->

# Squid

There is a bug with RESPMOD (REQMOD is working well) of Squid from version 5.5 to 6.11 then the file > 65563 bytes can not be download (<https://bugs.squid-cache.org/show_bug.cgi?id=5463>)

Please use Squid version **4.13** or **6.13** or **7.0.1** (Which has already included the bug fix)

## [Basic Configuration](/docs/mdicap/integrations/squid#basic-configuration)

Squid configuration should be done by modifying “squid.conf” (e.g, /etc/squid3/squid.conf). Below is an example of a simplified version of configuration for Squid. For more detailed documentation, please refer to the Squid manual.

1. **Enable acl localnet.**

Search for “acl localnet” section, uncomment all “acl localnet” lines. Below is an example of how the configuration might look:

acl localnet src 10.0.0.0/8
acl localnet src 172.16.0.0/12 # RFC1918 possible internal network
acl localnet src 192.168.0.0/16 # RFC1918 possible internal network
acl localnet src fc00::/7 # RFC 4193 local private network range
acl localnet src fe80::/10 # RFC 4291 link-local (directly plugged) machines
acl SSL_ports port 443
acl Safe_ports port 80 # http
acl Safe_ports port 21 # ftp
acl Safe_ports port 443 # https
acl Safe_ports port 70 # gopher
acl Safe_ports port 210 # wais
acl Safe_ports port 1025-65535 # unregistered ports
acl Safe_ports port 280 # http-mgmt
acl Safe_ports port 488 # gss-http
acl Safe_ports port 591 # filemaker
acl Safe_ports port 777 # multiling http
acl CONNECT method CONNECT

2. **Allow localnet and localhost access** by adding the following lines. (under the "Recommended minimum Access Permission configuration" section)

http_port 3128
http_access allow localnet
http_access allow localhost
http_access deny all

3. **Enable ICAP and set the Preview Size to 0**. (these values don't exist, so you simply add them anywhere in the file)

icap_enable on
icap_send_client_ip on
icap_preview_enable on
icap_preview_size 0
icap_service_failure_limit -1

4. **Enable ReqMod** (upload mode)...these don't exist, so add them anywhere

icap_service metascan_req reqmod_precache bypass=0 icap://<MetaDefender ICAP Server>:1344/OMSScanReq-AV
adaptation_access metascan_req allow all

5. **Enable RespMod** (download mode) again, these don't exist, so add them anywhere

icap_service metascan_resp respmod_precache bypass=0 icap://<MetaDefender ICAP Server>:1344/OMSScanResp-AV
adaptation_access metascan_resp allow all

**Persistent connections**

By default, Squid is using persistent connections to the MetaDefender ICAP Server, this feature can be controlled explicitly by the following directive:

icap_persistent_connections on/off

If persistent connections are enabled in Squid, the same setting should be applied to the ICAP side or Squid might report some ICAP errors. See [3. Configuring MetaDefender ICAP Server](/docs/mdicap/configuration/metadefender-icap-server-configuration).

**Restart Squid to apply the new configuration.**

Note

If you are using Squid 3.1 there is a bug in Squid that drops the connection to the ICAP server. You will notice messages in Squid's cache.log file similar to the following:

`essential ICAP service is down after an options fetch failure: icap://<MetaDefender ICAP Server>:1344/OMSScanReq-AV [down,!opt]`

This may cause you to get Squid error messages when trying to access websites.

To fix this, either upgrade to Squid 3.2 or higher, or add icap_persistent_connections off to your squid.conf file.

## [Scanning HTTPS content](/docs/mdicap/integrations/squid#scanning-https-content)

Learn how to configure Squid to scan HTTPS content below. This allows Squid to send HTTPS content to the MetaDefender ICAP Server for scanning purposes.

### [Requirements](/docs/mdicap/integrations/squid#requirements)

- Version: Tested with 3.5.19
- Squid has to be compiled with SSL support. For further information, please see: <http://docs.diladele.com/>

### [Configuration](/docs/mdicap/integrations/squid#configuration)

Tell Squid to listen on the following ports by modifying the line

http_port 3128

to this:

http_port 3128 ssl-bump generate-host-certificates=on dynamic_cert_mem_cache_size=4MB cert=<SQUIDFOLDER>\etc\ssl\myc.pem

In addition, the following lines have to be inserted:

sslcrtd_program <SQUIDFOLDER>\lib\squid\security_file_certgen.exe -s <SQUIDFOLDER>\var\cache\squid_ssldb -M 4MB
 
ssl_bump stare all
ssl_bump bump allWith Squild version older than v4

replace **security_file_certgen.exe** by **ssl_crtd.exe**

## [Certificate](/docs/mdicap/integrations/squid#certificate)

Generate a new root certificate for Squid:

openssl.exe req -new -newkey rsa:1024 -days 1000 -nodes -x509 -keyout myc.pem -out myc.pem

After generating a new certificate, the certificate storage should be reinitialized by deleting the <SQUIDFOLDER>\var\cache\squid_ssldb folder and running:

<SQUIDFOLDER>\lib\squid\ssl_crtd.exe -c -s <SQUIDFOLDER>\var\cache\squid_ssldb

The certificate has to be installed as a root certificate in the browser. Squid has to be restarted after the changes.
