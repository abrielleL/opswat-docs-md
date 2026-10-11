<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/ssl-certificates -->

# SSL Certificates

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**MetaDefender Sandbox** (previously known as OPSWAT Filescan Sandbox) uses the **NGINX** web server and its configuration is defined in `/srv/backend/nginx/conf/production/default.conf`

Warning

Any modifications to `/srv/backend/nginx/conf/production/default.conf` will be **overwritten if you upgrade** your Sandbox installation!

Always **create a backup** of this file if you modify it!

Alternatively, choose a solution below that does not require modifications to this file!

The following self-signed certificate and key files are used by default:

ssl_certificate /app/nginx/certs/nginx-selfsigned.crt;
ssl_certificate_key /app/nginx/certs/nginx-selfsigned.key;

The `/app/nginx/certs` path only exists within the Sandbox docker containers, and the corresponding files are actually located in `/home/sandbox/sandbox/webservice/nginx/certs` (the path might differ if you installed Sandbox to a different target directory).

It is possible to modify the configuration to point to your certificate and key files, but it is **recommended to overwrite** the self-signed certificate and key with your own files instead! If you do that, **you can upgrade Sandbox without losing these settings.**

Please create a backup of the self-signed certificate and key files first:

BashCopysudo su sandbox
cd /home/sandbox/sandbox/webservice/nginx/certs
sudo mv nginx-selfsigned.crt nginx-selfsigned-BACKUP.crt
sudo mv nginx-selfsigned.key nginx-selfsigned-BACKUP.key

Then overwrite these files with your **full certificate chain and private key files in PEM format** (the original file extension does not matter). For example, if your custom files are located in `~/my.domain.com` :

BashCopysudo cp ~/my.domain.com/fullchain.pem /home/sandbox/sandbox/webservice/nginx/certs/nginx-selfsigned.crt
sudo cp ~/my.domain.com/privkey.pem /home/sandbox/sandbox/webservice/nginx/certs/nginx-selfsigned.key

Make sure that the certificate is readable by all users and the private key is owned by your `sandbox` user:

BashCopysudo chmod a+r /home/sandbox/sandbox/webservice/nginx/certs/nginx-selfsigned.crt
sudo chown sandbox:sandbox /home/sandbox/sandbox/webservice/nginx/certs/nginx-selfsigned.key

After these preparations, please restart the Sandbox webservice (this should only take a minute):

BashCopy/home/sandbox/sandbox/stop_sandbox.sh
/home/sandbox/sandbox/start_sandbox.sh

At this point, you should be able to reach your Sandbox instance at `https://my.domain.com` on port 443.

---

### [Special considerations for private key files with a passphrase](/docs/filescan/3.2.0/configuration/ssl-certificates#special-considerations-for-private-key-files-with-a-passphrase)

NGINX also supports PEM private key files that require a passphrase to use.

In this case, the `ssl_password_file` option should be added in `/srv/backend/nginx/conf/production/default.conf` as described in the [NGINX documentation](http://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_password_file)

For example:

BashCopyssl_password_file /etc/keys/global.pass;

As the `default.conf` file must be changed for this, it is strongly encouraged to create a **backup** of this file **before you upgrade Sandbox**!

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
