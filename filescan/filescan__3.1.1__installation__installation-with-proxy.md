<!-- source: https://www.opswat.com/docs/filescan/3.1.1/installation/installation-with-proxy -->

# Proxy Usage

We recommend using a **transparent proxy**! A transparent proxy can hide its settings, hence it is safer and requires no additional configuration on the target machine.

Warning

If your proxy setup breaks SSL connections (end-to-end encryption for HTTPS), then the Sandbox installation will NOT succeed, **unless the proxy’s CA certificate is trusted by the system**.

Please refer to the **“Using Self-Signed Certificates”** section for instructions.

If you cannot install the required CA certificates, or outbound HTTPS traffic is blocked, the Sandbox installation will NOT succeed and you should perform an **Offline Installation** instead.

Info

This feature is available from Sandbox version 1.9.3

## [Proxy server configuration](/docs/filescan/3.1.1/installation/installation-with-proxy#proxy-server-configuration)

The following URLs are recommended to bypass on the proxy server:

- [https://api.metadefender.com/](https://api.metadefender.com/v4/) (For OPSWAT Reputation lookup)
- <https://activation.dl.opswat.com/> (To reach the OPSWAT license server)

## [Sandbox server configuration](/docs/filescan/3.1.1/installation/installation-with-proxy#sandbox-server-configuration)

The following configuration is necessary for the installer and the product to work properly behind a **non-transparent HTTP proxy**.

### [Before Sandbox installation](/docs/filescan/3.1.1/installation/installation-with-proxy#before-sandbox-installation)

Set the following configuration settings before installation.

Warning

These settings are **only used during the installation** process to prepare the environment for the Sandbox service!

If the proxy settings are **changed** after the installation, please **apply the changes mentioned in the next section** OR **repeat the installation process** to make sure that the Sandbox service uses the updated configuration!

#### [System-wide proxy configuration](/docs/filescan/3.1.1/installation/installation-with-proxy#system-wide-proxy-configuration)

Update the `/etc/environment` config, copy the proxy variables to the end of the file as described below. This will be used by tools like WGET, CURL, APT.

Warning

Always set the `NO_PROXY` variable to **precisely** **match** the example below. The IP address ranges: `172.16.0.0/12` and `192.168.0.0/16` are used by Docker, do not reuse them for other purposes.

Please use **your own proxy URL** instead of the example *proxy.example.com:3128.*

Info

The proxy format is `<protocol>://<user>:<password>@<domain or IP address>:<port>` where <user> and <password> are URL encoded strings.

http_proxy=http://proxy.example.com:3128
https_proxy=https://proxy.example.com:3128
HTTP_PROXY=http://proxy.example.com:3128
HTTPS_PROXY=https://proxy.example.com:3128
NO_PROXY=localhost,172.16.0.0/12,192.168.0.0/16,fsio,broker,transform,reverse_proxy

Once the file is updated log out and log in again for these changes to take effect:

BashCopyexit
#### [Using self-signed certificates](/docs/filescan/3.1.1/installation/installation-with-proxy#using-self-signed-certificates)

If your proxy setup uses self-signed certificates, complete the following steps **before the installation**.

Ensure that the following directory exists: `/usr/local/share/ca-certificates` If it does not exist, please create it:

BashCopysudo mkdir -p /usr/local/share/ca-certificatesInfo

**On Red Hat–based systems, use:** `/etc/pki/ca-trust/source/anchors/`

Copy your self-signed certificate file(s) into this directory.

During installation, the installer will automatically detect and import all certificates found in this folder.

Warning

If you update your self-signed certificate files in this folder in the future, you should also re-run the Sandbox installer to import the updated certificates!

#### [Docker proxy configuration](/docs/filescan/3.1.1/installation/installation-with-proxy#docker-proxy-configuration)

Create the docker daemon proxy configuration file.

http-proxy.confCopysudo mkdir -p /etc/systemd/system/docker.service.d
sudo touch /etc/systemd/system/docker.service.d/http-proxy.conf

Update the proxy settings similarly to the system-wide proxy configuration:

[Service]
Environment="HTTP_PROXY=http://proxy.example.com:3128"
Environment="HTTPS_PROXY=https://proxy.example.com:3128"
Environment="NO_PROXY=localhost,172.16.0.0/12,192.168.0.0/16,fsio,broker,transform,reverse_proxy"

Optionally, if the docker daemon is already installed on your system, restart it:

BashCopysudo systemctl daemon-reload
sudo service docker restart

Install Sandbox as described on the [Online Installation](/docs/filescan/3.1.1/installation/quick-installation) page.

Warning

**Online** license activation is not working when a proxy is used!

Please follow the "**Offline license activation**" section of the [License Activation](/docs/filescan/3.1.1/installation/license-activation) page.

### [Proxy configuration change after Sandbox installation (optional)](/docs/filescan/3.1.1/installation/installation-with-proxy#proxy-configuration-change-after-sandbox-installation-optional)

Info

Sandbox components will use the proxy settings stored in `/home/sandbox/.docker/config.json` (this file is created/updated by the Sandbox installer).

It is possible to change the proxy configuration used by Sandbox components (Docker containers) without reinstalling Sandbox. If your **proxy configuration changed**, please modify the settings in `/home/sandbox/.docker/config.json` (the path may differ if you installed Sandbox under a different user):

/home/sandbox/.docker/config.jsonCopy{
"proxies": {
"default": {
"httpProxy": "http://proxy.example.com:3128",
"httpsProxy": "https://proxy.example.com:3128",
"noProxy": "localhost,172.16.0.0/12,192.168.0.0/16,fsio,broker,transform,reverse_proxy"
}
}
}

Then please restart the sandbox service to remove and restart all Docker containers:

BashCopysudo service sandbox restart

You can check the currently used proxy configuration for a given Docker container, e.g. for `transform` :

BashCopydocker inspect --format='{{range .Config.Env}}{{println .}}{{end}}' transform

This is the expected output:

BashCopyHTTP_PROXY=http://proxy.example.com:3128
http_proxy=http://proxy.example.com:3128
HTTPS_PROXY=https://proxy.example.com:3128
https_proxy=https://proxy.example.com:3128
NO_PROXY=localhost,172.16.0.0/12,192.168.0.0/16,fsio,broker,transform,reverse_proxy
no_proxy=localhost,172.16.0.0/12,192.168.0.0/16,fsio,broker,transform,reverse_proxy
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
UNAME=sandbox

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
