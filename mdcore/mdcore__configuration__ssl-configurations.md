<!-- source: https://www.opswat.com/docs/mdcore/configuration/ssl-configurations -->

# SSL Configurations

Starting from version 5.13.0, the `ssl on` directive is deprecated and can no longer be used for configuring SSL. Please utilize the Web UI console to configure HTTPS connections.

When upgrading from an older version to 5.13.0, MetaDefender Core will automatically migrate the SSL configuration to a new file named `ssl.conf.mdcore` to manage SSL settings. To configure SSL, please use this file but we recommend to use the Web UI console instead manually modify this file.

If the customer is already using `ssl.conf` for SSL configuration, there is no need to worry as it will be updated automatically during the upgrade.

Before upgrading, ensure that the file `ssl.conf` has permission set to `777`. After the upgrade, remember to adjust the file permissions accordingly.

Info

The `ssl.mdcore.conf` file can only use for 3 directives

- `ssl on`
- `ssl_certificate`
- `ssl_certificate_key`

`ssl_protocols` and `ssl_ciphers` (and other directives) MUST added in a conf file in `built-in` folder (please check **Advanced SSL configurations** section)

1.) Create a file called `ssl.conf.mdcore` (**MetaDefender Core only accept this name**)

- On Windows, under ***<Installation Directory>\nginx***

ssl on;
ssl_certificate "C:/Program Files/OPSWAT/Metadefender Core/nginx/your.crt";
ssl_certificate_key "C:/Program Files/OPSWAT/Metadefender Core/nginx/your.key";

- On Linux:
- Create folder `/etc/ometascan/nginx.d` if not existed, and make sure to grant read and write access for metascan user on this folder and all files inside.
- Create file `ssl.conf.mdcore` (MetaDefender Core only accept this name) in the directory `/etc/ometascan/nginx.d`
- Enter SSL-configuration:

ssl on;
ssl_certificate /etc/ometascan/nginx.d/your.crt;
ssl_certificate_key /etc/ometascan/nginx.d/your.key;

2.) A restart of the “OPSWAT Metadefender Core” service is required.

## [Advanced SSL configurations](/docs/mdcore/configuration/ssl-configurations#advanced-ssl-configurations)

Warning

**For advanced SSL configurations like: TLS version and SSL ciphers, please create a conf file in built-in folder, for example:**

- Windows: `<installation folder>/nginx/built-in/advanced_ssl.conf`
- Linux: `/etc/ometascan/nginx.d/built-in/advanced_ssl.conf`

1.) Explicitly allow specific TLS versions, optionally with preferred ciphers. For example:

ssl_protocols tlsv1.2;
ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256;

2.) Use SSL private key and(or) certificate which is encrypted with a passphrase. Strongly recommended to put the passphrase file(s) into a secured vault where only MetaDefender Core can access.

A reference for typical practice: <https://www.nginx.com/blog/protecting-ssl-private-keys-nginx-hashicorp-vault/>

ssl_password_file "C:/keys/private.pass";

**For more SSL-options please consult** [Nginx documentation](http://nginx.org/en/docs/http/ngx_http_ssl_module.html).

Warning

'\n' sequences in paths

Using the standard Windows path separator backslash '' may give unexpected results if directory or file names start with 'n'. The reason is that the sequence '\n' is interpreted as a new line by nginx.

For example the following directive

`ssl_certificate "C:\Program Files\OPSWAT\Metadefender Core\nginx\your.crt";`

will appear at nginx as

`ssl_certificate "C:\Program Files\OPSWAT\Metadefender Core`

`ginx\your.crt";`

As a workaround instead of backslash '' use

1. Forward slash '/' or
2. Double backslash ''.

Note that certificate and key files are to provided by the user who can store them whenever it is convenient. Please adjust the paths accordingly.

Note: When choosing location for cert and key files, make sure the files are in a location which is readable to the service user.
