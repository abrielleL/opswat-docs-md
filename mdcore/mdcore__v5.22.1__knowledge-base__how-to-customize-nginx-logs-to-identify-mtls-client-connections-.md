<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-customize-nginx-logs-to-identify-mtls-client-connections- -->

# How to customize Nginx logs to identify mTLS client connections?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core v5 releases deployed on Windows and Linux systems.

Currently, **MetaDefender Core does not support editing the existing log format.** However, it supports creating a new custom log format where Nginx can write the needed details.

Follow the steps below to generate a new log file that lets you differentiate between mTLS and regular requests:

1. **Create the configuration files:**

   - Windows:

     - C:\Program Files\OPSWAT\MetaDefender Core\nginx**newlog.conf** (to configure the new log format)
     - C:\Program Files\OPSWAT\MetaDefender Core\nginx**built-in/mtls.conf** (to configure where nginx will write the log to)
   - Linux:

     - /etc/ometascan/nginx.d/**newlog.conf** (to configure the new log format)
     - /etc/ometascan/nginx.d/**built-in/​​​​​​​mtls.conf** (to configure where nginx will write the log to)
2. **Add the following data to the config files:**

**newlog.conf**:

HtmlCopylog_format mtls '$remote_addr - $ssl_client_s_dn [$time_local] "$request" '
'$status $body_bytes_sent "$http_referer" '
'"$http_user_agent" ssl_client_verify "$ssl_client_verify" ssl_client_s_dn "$ssl_client_s_dn" ssl_client_i_dn "$ssl_client_i_dn" ssl_client_serial "$ssl_client_serial"';
log_format message_log_file_batch_mtls '$remote_addr - $remote_user [$time_local] ' '"$request" $status $body_bytes_sent ' '"$batch_id" ' '"$http_referer" "$http_user_agent" ' '$request_time' 'ssl_client_verify "$ssl_client_verify" ssl_client_s_dn "$ssl_client_s_dn" ssl_client_i_dn "$ssl_client_i_dn" ssl_client_serial "$ssl_client_serial"';
log_format message_log_file_mtls '$remote_addr - $remote_user [$time_local] ' '"$request" $status $body_bytes_sent ' '"batch_id:$http_batch" ' '"$data_id" ' '"$http_referer" "$http_user_agent" ' '$request_time' 'ssl_client_verify "$ssl_client_verify" ssl_client_s_dn "$ssl_client_s_dn" ssl_client_i_dn "$ssl_client_i_dn" ssl_client_serial "$ssl_client_serial"';

**mtls.conf**

HtmlCopyssl_client_certificate "path_to_ca_cert/ca.crt";
ssl_verify_client optional;
access_log "path_to_nginx_folder\\mtls.log" mtls;
location ~ "^/file/sync$" {
access_log "path_to_nginx_folder\\mtls.log" message_log_file_mtls;
set $data_id "";
header_filter_by_lua_block {
if ngx.header["data-id"] then
ngx.var.data_id = "data_id" .. ":" .. ngx.header["data-id"];
end
}
if ( $request_method !~ ^(POST)$ ) {
return 404;
}
more_set_headers 'Cache-Control: no-cache';
content_by_lua_file resource/resourcehandler.raw;
}
location ~ "^/file/batch$" {
access_log "path_to_nginx_folder\\mtls.log" message_log_file_batch_mtls;
set $batch_id "";
body_filter_by_lua_block {
ngx.ctx.buffered = (ngx.ctx.buffered or "") .. ngx.arg[1]
if ngx.arg[2] then
ngx.ctx.buffered = string.sub(ngx.ctx.buffered, 1, 5000)
end
local brief_batch_id = string.gsub(ngx.ctx.buffered, "%\x22", "")
local resp_batch_id = brief_batch_id:match('^{batch_id:([a-f0-9]+)')
if resp_batch_id then
ngx.var.batch_id = "batch_id" .. ":" .. resp_batch_id
end
}
if ( $request_method !~ ^(POST)$ ) {
return 404;
}
more_set_headers 'Cache-Control: no-cache';
content_by_lua_file resource/resourcehandler.raw;
}
location ~ "^/(file|process)$" {
access_log "path_to_nginx_folder\\mtls.log" message_log_file_mtls;
set $data_id "";
body_filter_by_lua_block {
ngx.ctx.buffered = (ngx.ctx.buffered or "") .. ngx.arg[1]
if ngx.arg[2] then
ngx.ctx.buffered = string.sub(ngx.ctx.buffered, 1, 5000)
end
local brief_data_id = string.gsub(ngx.ctx.buffered, "%\x22", "")
local resp_data_id = brief_data_id:match('^{data_id:([a-f0-9]+)')
if resp_data_id then
ngx.var.data_id = "data_id" .. ":" .. resp_data_id
end
}
if ( $request_method !~ ^(POST)$ ) {
return 404;
}
more_set_headers 'Cache-Control: no-cache';
content_by_lua_file resource/resourcehandler.raw;
}

3. **Restart the MetaDefender Core service**
4. **Verify the new configuration by sending requests**

   - Perform a scan request **with mTLS** and **without mTLS**.
   - The result will be as follows:

With mTLS:

HtmlCopy10.40.50.228 - CN=client\x5C0A [29/Jul/2025:13:20:21 +0700] "POST /file/async HTTP/1.1" 404 948 "-" "curl/7.81.0" ssl_client_verify "SUCCESS" ssl_client_s_dn "CN=client\x5C0A" ssl_client_i_dn "CN=my_ca" ssl_client_serial "2553AE8B5C0360FA6A015EF3F53B4A2EF59A664E"

Without mTLS:

HtmlCopy::1 - - [29/Jul/2025:13:19:30 +0700] "POST /file HTTP/1.1" 200 57 "batch_id:-" "data_id:a00d24282a7d4e8098bab2fd042ccfcd" "https://localhost:8008/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/138.0.0.0 Safari/537.36" 0.093ssl_client_verify "NONE" ssl_client_s_dn "-" ssl_client_i_dn "-" ssl_client_serial "-"Notes

- The logging for the endpoints `/file/sync`, `/file/batch`, `^/(file|process)` will **no longer output to the official** `nginx.log` in MetaDefender Core. Instead, logs will be written to the new log file.
- It is advised to place the new log file (**nginx_mtls.log**) in the same folder as `nginx.log`.

  - This ensures it will be included in the **support package**.
  - The log filename **must start with** `nginx` (e.g., `nginx_mtls.log`).
Limitations

- This is a **workaround, not an official solution**. OPSWAT does not provide product support for this customization.
- You will need to maintain the settings manually after upgrades.
- Log rotation is **not supported** for the new log file.

  - The file will continuously grow in size.
  - You must implement your own rotation/cleanup process if needed.
Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).
