<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/why-does-the-opswat-icap-nginx-module-fail-to-install-or-load-on -->

# Why does the OPSWAT ICAP NGINX module fail to install or load on a custom-compiled NGINX build?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [Symptoms](/docs/mdicap/v5.15.0/knowledge-base/why-does-the-opswat-icap-nginx-module-fail-to-install-or-load-on#symptoms)

When attempting to install the OPSWAT ICAP NGINX module RPM, the installation fails with a package dependency similar to the following:

Requires: nginx-r1.28.1

If the module is then extracted manually from the RPM and added to the NGINX configuration using:

load_module modules/ngx_http_ometascan_module.so;

NGINX validation or reload fails with an error similar to:

sudo /usr/nginx/sbin/nginx -t
nginx: [emerg] module "/usr/nginx/modules/ngx_http_ometascan_module.so" is not binary compatible in /usr/nginx/nginx.conf:5
#### [Cause](/docs/mdicap/v5.15.0/knowledge-base/why-does-the-opswat-icap-nginx-module-fail-to-install-or-load-on#cause)

This issue occurs when the OPSWAT NGINX ICAP module RPM is installed on a system where NGINX was not installed from the matching RPM package, but was instead compiled manually from source. In this case, the RPM dependency check fails, and even if the module shared object (`.so`) is extracted manually, NGINX may still reject it because the module is not binary-compatible with the running NGINX build.

The `not binary compatible` error occurs because the OPSWAT module is built with `--with-compat`, which enables a relaxed signature check, NGINX build was not compiled with `--with-compat`. As a result, NGINX enforce a strict build-signature match that the custom build flags did not satisfy. Recompiling NGINX with `--with-compat` is the supported approach for custom or binary NGINX builds.

#### [Resolution](/docs/mdicap/v5.15.0/knowledge-base/why-does-the-opswat-icap-nginx-module-fail-to-install-or-load-on#resolution)

To load the OPSWAT dynamic module successfully on a custom-built NGINX installation, recompile NGINX with the same custom prefixes and include the `--with-compat` option.

1. **Rebuild NGINX with compatibility support enabled.**

./configure {all existing custom prefixes and options} --with-compat
make -j"$(nproc)"
sudo make install

2. **Download the OPSWAT NGINX module RPM** from the OPSWAT portal that matches your NGINX version and operating system.
3. **Extract the module shared object from the RPM.**

rpm2cpio nginx-module-ometascan-1.28.1+1.4.1-1.el8.ngx.x86_64.rpm | cpio -idmv

4. **Copy the module into the NGINX modules directory and set permissions.**

sudo cp usr/lib64/nginx/modules/ngx_http_ometascan_module.so /usr/nginx/modules/
sudo chmod 755 /usr/nginx/modules/ngx_http_ometascan_module.so

5. **Add the module directive to the NGINX configuration.**

# Dynamic modules
# load_module modules/ngx_http_geoip_module.so;
# load_module modules/ngx_http_headers_more_filter_module.so;
load_module modules/ngx_http_ometascan_module.so;
events {
worker_connections 1024;
}
http {
access_log /web_log/access.log;
error_log /web_log/error.log debug;
server {
listen 8080;
server_name localhost;
location / {
return 200 "NGINX custom build is running\n";
}
}
}

6. **Validate the configuration.**

sudo /usr/nginx/sbin/nginx -t

If the NGINX binary and the OPSWAT module are compatible, the configuration test should complete successfully.

Best Practice:

When using dynamic NGINX modules in a custom build, preserve the original configure arguments and add only `--with-compat` unless you intentionally need other changes. Unnecessary build differences can introduce additional compatibility problems.

- The module package version must match the installed NGINX version.
- If your custom NGINX build differs significantly from the expected vendor build, recompiling with `--with-compat` may still not be sufficient in every case.
- Installing the RPM directly is only expected to work when the required NGINX RPM dependency is present on the system.

Support

If Further Assistance is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
