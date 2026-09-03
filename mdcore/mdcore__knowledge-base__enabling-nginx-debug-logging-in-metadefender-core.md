<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/enabling-nginx-debug-logging-in-metadefender-core -->

# Enabling NGINX Debug Logging in MetaDefender Core

This article applies to all MD Core versions.

MetaDefender Core uses an embedded NGINX instance as a reverse proxy in front of the application services. In most cases, troubleshooting should rely on MetaDefender Core application logs. However, NGINX debug logging can be helpful in specific scenarios where issues occur **before the request reaches the Core engine**.

You may need NGINX debug logs when troubleshooting:

- Missing or incorrect **HTTP headers**
- Requests that appear to be **rejected or not processed**
- Differences between **successful and failed API calls**
- **Authentication or proxy-related issues**
- Validation of the **exact request received** by MetaDefender Core (method, headers, timing)

Debug logs provide full visibility into:

- Incoming request headers
- Request processing stages
- Upstream communication
- Connection handling

> **Note**: Debug logging is very verbose and should be enabled only for temporary troubleshooting.

**1.** By default, the runtime NGINX configuration is generated under:

`C:\Windows\Temp\ometascan\nginx.conf`

This should not be modified directly.

However, it includes the following directive:

`include "C:/Program Files/OPSWAT/MetaDefender Core/nginx/*.conf";`

This allows additional configuration files to be loaded.

**2.** Create a debug configuration file:

`C:\Program Files\OPSWAT\MetaDefender Core\nginx\debug.conf`

Add:

`error_log "C:/Program Files/OPSWAT/MetaDefender Core/nginx/nginx-debug.log" debug;`

**3.** Restart MetaDefender Core service:

- Open Services (`services.msc`)
- Restart: `OPSWAT MetaDefender Core`

**4.** The debug log will be available at:

`C:\Program Files\OPSWAT\MetaDefender Core\nginx\nginx-debug.log`

**1.** By default, the runtime NGINX configuration is generated under:

`/var/run/ometascan/nginx.conf`

This should not be modified directly.

However, it includes the following directive:

`include /etc/ometascan/nginx.d/*.conf;`

This allows additional configuration files to be loaded.

**2.** Create a debug configuration file:

`sudo mkdir /etc/ometascan/nginx.d sudo vi /etc/ometascan/nginx.d/debug.conf`

Add:

`error_log /var/log/ometascan/nginx-debug.log debug;`

**3.** Restart MetaDefender Core service.

`sudo systemctl restart ometascan`

**4.** The debug log will be available at:

`/var/log/ometascan/nginx-debug.log`

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
