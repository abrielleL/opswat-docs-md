<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/configuration/configuring-ssl -->

# Configuring SSL

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Update Downloader supports accessing Web UI and REST interface via HTTPS. This feature is not allowed by default, however. To allow the feature you should modify Update Downloader Server configuration by following the next steps:

Warning

MetaDefender Update Downloader only **accepts** the file named **ssl.conf.mddownloader** for HTTPS **enable only**

The user **needs** to take care of the permissions of the file **ssl.conf.mddownloader**.

For other configuration related to SSL like TLS version, ciphers, etc. Please use an other configuration file for example ssl.conf

## [HTTPS enable via ssl.conf.mddownloader](/docs/mddownloader/v3.5.0/configuration/configuring-ssl#https-enable-via-sslconfmddownloader)

1.Create file **ssl.conf.mddownloader** in the directory

- Linux /etc/ometadownloader/nginx.d
- Windows: in the directory <Installation Directory>\nginx.

2.Enter SSL-configuration according to Nginx. In order for the encrypted HTTPS connection to work, the certificate-key pair is required. This pair contains a certificate.crt file and a certificate_key.key file.

To allow simple SSL one needs to add the following lines only:

Linux:

ssl.conf.mddownloaderCopyssl on;
ssl_certificate /etc/ometadownloader/nginx.d/your.crt;
ssl_certificate_key /etc/ometadownloader/nginx.d/your.key;

Windows:

ssl.conf.mddownloaderCopyssl on;
ssl_certificate C:\Program Files\OPSWAT\Metadefender Update Downloader\nginx\your.crt;
ssl_certificate_key C:\Program Files\OPSWAT\Metadefender Update Downloader\nginx\your.key;

3. Service restart is required to take these changes into effect.

Note that certificate and key files **are provided** by the user who can store them **wherever** it is convenient. Please adjust the paths accordingly.

Note: When **choosing the location** for **.crt** and .key files, make sure they are readable by the service user as well as the directory **they are executed from.**

## [**Other SSL configurations**](/docs/mddownloader/v3.5.0/configuration/configuring-ssl#other-ssl-configurations)

The file ssl.conf.mddownloader is only for enable HTTPS, for other configurations like TLS version, cipher, please create another conf file, for example ssl.conf

ssl.confCopyssl_protocols TLSv1.3;Info

OPSWAT has **fully deprecated support for TLS 1.0 and TLS 1.1** across its product line

For more SSL-options please consult [Nginx documentation](http://nginx.org/en/docs).
