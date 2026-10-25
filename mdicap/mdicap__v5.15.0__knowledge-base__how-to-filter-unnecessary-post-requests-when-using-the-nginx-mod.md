<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-to-filter-unnecessary-post-requests-when-using-the-nginx-mod -->

# How to Filter Unnecessary POST Requests When Using the NGINX Module?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Issue:** Unnecessary POST requests can be scanned when using the NGINX module, potentially impacting performance.

**Resolution:** Filter unnecessary POST requests by defining location matches in the NGINX configuration. This allows selective scanning while bypassing specific paths.

**Configuration Example:**

To scan all requests except `/o/oauth2/token` and `/c/portal/saml/acs`, use the following configuration in the nginx.conf file located in **/etc/nginx/nginx.conf**

HtmlCopyload_module /etc/nginx/modules/ngx_http_ometascan_module.so;
http {
client_max_body_size 1000M;
server {
listen 80;
server_name localhost;
location ~ ^\/(o\/oauth2\/token|c\/portal\/saml\/acs)$ {
proxy_pass <http://server_back_end_server.domain:8000;>
}
location / {
ometascan_pass <http://icap_server.domain:8043;>
ometascan_methods POST;
ometascan_read_timeout 1d;
proxy_pass <http://server_back_end_server.domain:8000;>
}
}
}

**Workarounds:** The following tool can be used to verify location configuration: <<https://nginx.viraptor.info/>>

**Related Articles:**

- [NGINX location directive](https://nginx.org/en/docs/http/ngx_http_core_module.html#location)
- [Using Regex in Nginx Location Block](https://stackoverflow.com/questions/59846238/guide-on-how-to-use-regex-in-nginx-location-block-section)

Also, the following tool can be used to verify location config: <https://nginx.viraptor.info/>

There are more details on the following links: [Module ngx_http_core_module](https://nginx.org/en/docs/http/ngx_http_core_module.html#location) and [Guide on how to use regex in Nginx location block section?](https://stackoverflow.com/questions/59846238/guide-on-how-to-use-regex-in-nginx-location-block-section)

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
