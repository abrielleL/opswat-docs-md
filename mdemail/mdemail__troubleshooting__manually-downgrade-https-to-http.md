<!-- source: https://www.opswat.com/docs/mdemail/troubleshooting/manually-downgrade-https-to-http -->

# Manually downgrade HTTPS to HTTP

## Problem

In certain cases upgrading the REST interface from HTTP to HTTPS fails, resulting in an inconsistent state where the connection is accepted via HTTPS only, but the HTTPS handshake fails. In this case the web management console becomes unavailable.

## Example

When the REST interface is upgraded to HTTPS (for details see [Configuration/Transport Layer Security](/configuration/transport-layer-security)) using an expired certificate, then the configuration will succeed. Later, when the actual connection happens from a browser client, the browser will refuse to connect cause the certificate is expired.

## Solution

## Prerequisites

The resolution requires the following:

1. PsExec tool from Microsoft Sysinternals being installed,
2. Administrator privileges to edit the config file and reload REST backend.

Download PsExec

PsTools containing the PsExec tool can be downloaded from <https://docs.microsoft.com/en-us/sysinternals/downloads/psexec>.

## Resolution

To manually downgrade the REST interface from HTTPS to HTTP perform the following steps:

Service must be running

While performing this steps, it is important that the MetaDefender Email Gateway Security service must be running.

**DO NOT stop the MetaDefender Email Gateway Security service before performing these steps!**

### Revert TLS related configuration

1. As Administrator, open C:\Windows\Temp\mdemailsecurity\nginx.conf for editing
2. Search for the following directives inside the server section:

   1. listen
   2. ssl_certificate
   3. ssl_protocols

server {
listen 8058 ssl; listen [::]:8058 ssl;
ssl_certificate "C:/Windows/Temp/mdemailsecurity/https_cert.pem"; ssl_certificate_key "C:/Windows/Temp/mdemailsecurity/https_key.pem";
ssl_protocols TLSv1.2;

3. Modify both listen directives removing the ssl clause from them; and entirely delete the ssl_certificate and ssl_protocols directives

server {
listen 8058; listen [::]:8058;

4. Save C:\Windows\Temp\mdemailsecurity\nginx.conf.

### Reload REST backend with modified configuration

1. As Administrator launch the following command in a command shell:

<PsTools path>\PsExec.exe -s <Email Gateway Security installation directory>\nginx\nginx.exe -s reload -c c:\Windows\Temp\mdemailsecurity\nginx.conf

1. Example:

C:\PSTools\PsExec.exe -s "C:\Program Files\OPSWAT\MetaDefender Email Security\nginx\nginx.exe" -s reload -c C:\Windows\Temp\mdemailsecurity\nginx.conf

2. Check the command output for potential errors

   1. On success nginx.exe must exit with code 0. For example:

C:\Program Files\OPSWAT\MetaDefender Email Security\nginx\nginx.exe exited on LP10-D4119 with error code 0.

2. The following message does not indicate an error:

nginx: [warn] "user" is not supported, ignored in c:\Windows\Temp\mdemailsecurity\nginx.conf:1
### Open the web management console via HTTP

1. Open Email Gateway Security’s web management console pointing your browser to the location where the product’s REST interface is listening

   1. Remember to provide http as schema instead of https
   2. Example:

http://localhost:80058
### Disable HTTPS in web management console

1. Navigate to **Settings > Security** and make *Enable HTTPS connection* disabled

After performing all these steps, Email Gateway Security will be available via HTTP even after a service restart.
