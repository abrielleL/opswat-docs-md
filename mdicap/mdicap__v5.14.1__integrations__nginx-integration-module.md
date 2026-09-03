<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/nginx-integration-module -->

# NGINX Integration Module

MetaDefender ICAP Server integrates with NGINX via the upstream module (reverse proxy) and related configuration directives.

The integration is enabled via a certified [NGINX Dynamic Module](https://www.f5.com/go/product/nginx-modules/opswat).

## Prerequisites

- You are running NGINX version 1.20.2 or above. The module supports both NGINX Community and NGINX Plus.
- MetaDefender ICAP Server version 5.1.0 or above is installed and licensed, and relevant NGINX integration settings are enabled.

  - To enable integration with NGINX module, refer to [NGINX Integration Configurations](/configuration/enable-integration-with-nginx)
- The integration uses a bridge module (called "Ometascan NGINX module") between your NGINX web server and MetaDefender ICAP Server.

  - The module installer can be downloaded on [My OPSWAT](https://my.opswat.com)Portal - **Product Downloads > MetaDefender ICAP Server > Modules and Utilities** section.

Warning

on RHEL or CentOS, httpd_can_network_connect must be enabled by command:

`setsebool -P httpd_can_network_connect 1`

More details about httpd_can_network_connect, please refer to <https://www.nginx.com/blog/using-nginx-plus-with-selinux/#Issue-1:-Proxy-Connection-is-Forbidden>

## Flow Diagrams

## Directives

### Forward

#### ometascan_pass

| Syntax | **ometascan_pass** **URL;** |
| --- | --- |
| Default | — |
| Context | location |

Info

Sets the protocol, address and optional URI of the proxied MD ICAP server. “`http`” or “`https`” protocols can be specified. The address can be specified as a domain name or IP address, and an optional port:

> ometascan_pass [http://icap_server:8080;](http://icap_server:8080;/)

Info

If an error occurs when sending a sub-request to the MD ICAP Server (timeout, network issue, etc) an error will be sent back to the ICAP client, and the request will be blocked.

Warning

When using `ometascan_pass,` the `proxy_request_buffering` of the Nginx proxy module will be disabled.

Info

When the sub-request to MD ICAP Server error (Timeout, Network, etc). The error will respond to the client, and the request blocked.

Info

When allowed with sanitized the `filename` parameter of `Content-Disposition` header will be renamed corresponding Metadender Core's CDR setting

#### ometascan_methods

| Syntax | ometascan_methods <list methods>; |
| --- | --- |
| Default | ometascan_methods GET HEAD POST PUT PATCH DELETE; |
| Context | location |

Info

This directive specifies HTTP request methods that are considered by `ometascan_pass`. HTTP request methods not listed will be ignored. The following HTTP methods are allowed: `GET`, `HEAD`, `POST`, `PUT`, `PATCH`, and `DELETE`

#### ometascan_send_timeout

| Syntax | ometascan_send_timeout time; |
| --- | --- |
| Default | ometascan_send_timeout 60s; |
| Context | location |

Info

Sets a timeout for transmitting a request to the proxied server. The timeout is set only between two successive write operations, not for the transmission of the whole request. If the proxied server does not receive anything within this time, the connection is closed.

Time intervals can be specified in milliseconds, seconds, minutes, hours, days and so on. Refer [here](http://nginx.org/en/docs/syntax.html) for more information.

Info

Time intervals can be specified in milliseconds, seconds, minutes, hours, days and so on, using the following suffixes:

ms milliseconds

s seconds

m minutes

h hours

d days

w weeks

M months, 30 days

y years, 365 days

Ref: [Configuration file measurement units (nginx.org)](http://nginx.org/en/docs/syntax.html)

#### ometascan_connect_timeout

| Syntax | ometascan_connect_timeout time; |
| --- | --- |
| Default | ometascan_connect _timeout 60s; |
| Context | location |

Info

Defines a timeout for establishing a connection with a proxied server. Note that this timeout should not exceed 75 seconds.

#### ometascan_read_timeout

| Syntax | ometascan_read_timeout time; |
| --- | --- |
| Default | ometascan_read__timeout 60s; |
| Context | location |

Info

Defines a timeout for reading a response from the proxied server. The timeout is set only between two successive read operations, not for the transmission of the whole response. If the proxied server does not transmit anything within this time, the connection is closed.

#### ometascan_x_forwarded_for

Info

Supported since version 1.1.0

| Syntax | ometascan_x_forwarded_for on/off; |
| --- | --- |
| Default | ometascan_x_ forwarded_for off; |
| Context | location |

#### ometascan_intercept_errors

| Syntax | ometascan_intercept_errors on/off; |
| --- | --- |
| Default | ometascan_intercept_ errors off; |
| Context | location |

Determines whether ometascan blocked responses should be passed to a client or intercepted and redirected to nginx for processing with the [error_page](https://nginx.org/en/docs/http/ngx_http_core_module.html#error_page) directive.

#### ometascan_allow_bad_request_traffic

Warning

- This will allow bad request traffic go to the protected system
- Only enable this directive for testing purpose

| Syntax | ometascan_allow_bad_request_traffic on/off; |
| --- | --- |
| Default | ometascan_allow_ bad_request_traffic off; |
| Context | location |

The ICAP Server will respond to the 400 Bad Request when receives an invalid HTTP RFC request from the ometascan module. By default, the module will respond to 400 Bad requests from the client. Enabling this option the module will allow requests whose bad requests without scanning

Info

- Supported since Ometascan NGINX module v1.2.0
- Must use MD ICAP Server v5.4.0 or newer
- The ometascan_allow_bad_request_traffic on required the **ometascan_pre_cache on**
#### ometascan_set_header

| Syntax | ometascan_set_header field value; |
| --- | --- |
| Default |  |
| Context | location |

Allows redefining or appending fields to the request header passed to the proxied server. The value can contain text, variables, and their combinations. These directives are inherited from the previous configuration level if and only if there are no ometascan_set_header directives defined on the current level. By default, no field is redefined.

If the value of a header field is an empty string then this field will not be passed to a proxied server:

`ometascan_set_header`Accept-Encoding "";``

### Caching

#### ometascan_pre_cache

| Syntax | ometascan_pre_cache on/off; |
| --- | --- |
| Default | ometascan_pre__cache off; |
| Context | location |

Warning

This configuration will not work when AppProtect is used and put on same scope

Info

Turn on/off pre-caching request when sending to MD ICAP Server.

When the cache is **enabled** the module will make a copy of the request on the NGINX server. And send it to the back-end when received allowed message from MD ICAP Server

#### ometascan_pre_cache_size

Warning

ometascan_pre_cache_size is deprecated since Ometascan NGINX module v1.2.0

| Syntax | ometascan_pre_cache_size size; |
| --- | --- |
| Default | ometascan_pre_cache_size 9223372036854775807; |
| Context | location |

Info

Config maximum caching size per request. Sizes can be specified in bytes, kilobytes (suffixes `k` and `K`) or megabytes (suffixes `m` and `M`), for example, “`1024`”, “`8k`”, “`1m`”.

### SSL/TLS

#### ometascan_ssl_trusted_certificate

| Syntax | ometascan_ssl_trusted_certificate file; |
| --- | --- |
| Default | _ |
| Context | location |

Info

Specifies a file with trusted CA certificates in the PEM format used to verify the certificate of the proxied HTTPS server.

#### ometascan_ssl_verify

| Syntax | ometascan_ssl_verify on | off; |
| --- | --- |
| Default | ometascan_ssl_ verify off; |
| Context | location |

Info

Enables or disables verification of the proxied HTTPS server certificate.

#### ometascan_ssl_verify_depth

| Syntax | ometascan_ssl_verify_depth number; |
| --- | --- |
| Default | ometascan_ssl_ verify_depth 1; |
| Context | location |

Info

Sets the verification depth in the proxied HTTPS server certificates chain.

#### ometascan_ssl_protocols

| Syntax | ometascan_ssl_protocols [SSLv3] [TLSv1] [TLSv1.1] [TLSv1.2] [TLSv1.3]; |
| --- | --- |
| Default | ometascan_ssl_ protocols TLSv1.1 TLSv1.2 TLSv1.3; |
| Context | location |

Info

Enables the specified protocols for requests to a proxied HTTPS server.

#### ometascan_ssl_ciphers

| Syntax | ometascan_ssl_ciphers ciphers; |
| --- | --- |
| Default | ometascan_ssl_ ciphers DEFAULT; |
| Context | `location` |

Info

Specifies the enabled ciphers for requests to a proxied HTTPS server. The ciphers are specified in the format understood by the OpenSSL library.

The full list can be viewed using the “`openssl ciphers`” command.

#### ometascan_ssl_session_reuse

| Syntax | ometascan_ssl_session_reuse on | off; |
| --- | --- |
| Default | ometascan_ssl_ session_reuse on; |
| Context | `location` |

Info

Determines whether SSL sessions can be reused when working with the proxied server. If the errors “`SSL3_GET_FINISHED:digest check failed`” appear in the logs, try disabling session reuse.

**Required**:

- The header contains a key `Connection` with the value `keepalive`.
- Enabled persistence connection of the MD ICAP Server ([Global settings](/configuration/other-settings#global-settings))

E.g: proxy_set_header `Connection` '`keepalive`';

#### ometascan_ssl_name

| Syntax | ometascan_ssl_name name; |
| --- | --- |
| Default | ometascan_ssl_ name <ometascan_pass_host>; |
| Context | `location` |

Info

Allows overriding the server name used to verify the certificate of the proxied HTTPS server and to be passed through SNI when establishing a connection with the proxied HTTPS server.

By default, the host part of the ometascan_pass URL is used.

#### ometascan_ssl_server_name

| Syntax | ometascan_ssl_server_name on | off; |
| --- | --- |
| Default | ometascan_ssl_ server_name off; |
| Context | `location` |

Info

Enables or disables passing of the server name through TLS Server Name Indication extension (SNI, RFC 6066) when establishing a connection with the proxied HTTPS server.

### Health Check

#### ometascan_health_check

| Syntax | ometascan_health_check interval=<msec> [passes=<count>] [fails=<count>] [timeout=<msec>] [jitter=<msec>] [mandatory [persistent]] |
| --- | --- |
| Default | disabled |
| Context | location |

Enables health checking for the upstream servers configured via ometascan_pass in the same location. The health check targets the same servers as the ometascan_pass directive. The first health check will start immediately after the process startup, and then it follows the time interval

**Parameters:**

| Parameter | Description | Default |
| --- | --- | --- |
| interval | The interval between health checks in milliseconds | 5000 (5s) |
| passes | Number of consecutive successful checks required to mark a server as UP | 1 |
| fails | Number of consecutive failed checks required to mark a server as DOWN | 1 |
| timeout | Timeout for each health check in milliseconds | 1000 (1s) |
| jitter | Sets the time within which each health check will be randomly delayed  Without it, if many peers share the same interval, they’ll synchronize and create a burst of simultaneous checks (“thundering herd”), which spikes CPU, network, and backend load. The jitter adds a small random delay (bounded by jitter and the interval) to decorrelate those timers and smooth the traffic. | 0 |
| mandatory [persistent] | Start servers in a "checking" state until the first check completes; client requests are not sent to "checking" servers  The persistent parameter sets the initial “up” state for a server after reload if the server was considered healthy before reload. | disabled |

**Example:**

upstream ometascan_backend {
zone ometascan_zone 64k;
server 192.168.1.10:8043;
server 192.168.1.11:8043;
}
server {
location / {
ometascan_pass http://ometascan_backend;
ometascan_health_check interval=5000 passes=2 fails=3 timeout=2000;
proxy_pass http://backend;
}
}Info

It creates a **shared memory zone** named: ometascan_zone with 64 kilobytes

#### ometascan_health_check_status

| Syntax | ometascan_health_check_status; |
| --- | --- |
| Default | disabled |
| Context | location |

Response the health check status

Warning

It should only be used to test if the feature is working. It should not be used in a production environment.

**Example:**

uupstream ometascan_backend {
zone ometascan_zone 64k;
server 192.168.1.10:8043;
server 192.168.1.11:8043;
}
server {
location / {
ometascan_pass http://ometascan_backend;
ometascan_health_check interval=5000 passes=2 fails=3 timeout=2000;
proxy_pass http://backend;
}
location /health_status {
ometascan_health_check_status;
}
}

When call GET /health_status the response will be

{
"servers": [
{
"name": "192.168.1.10:8043",
"status": "down",
"passes": 0,
"fails": 5
},
{
"name": "192.168.1.11:8043",
"status": "up",
"passes": 9,
"fails": 0
}
]
}
### Example Config

load_module modules/ngx_http_ometascan_module.so;
events {
worker_connections 4096;
}
http {
client_max_body_size 1000M;
server {
listen 80;
server_name localhost;
location ^~ / {
ometascan_pass http://icap_server.domain:8043;
ometascan_methods POST PUT;
ometascan_read_timeout 1d;
proxy_pass http://back_end_server.domain:8000;
}
}
}Info

- `client_max_body_size` Sets the maximum allowed size of the client request body. If the size in a request exceeds the configured value, the 413 (Request Entity Too Large) error is returned to the client. Please be aware that browsers cannot correctly display this error. Setting size to 0 disables checking of client request body size.
- `ometascan_pass` Set URL of the MD ICAP Server
- `ometascan_methods POST PUT;` Only scan POST and PUT methods
## Integration Steps

### Get installation file of ometascan nginx module

Download from [My OPSWAT Portal](https://my.opswat.com/portal/products) - **Downloadable Utilities > NGINX Module Library** section

### Command Line Install

#### CentOS

BashCopysudo rpm -i nginx-module-ometascan-1.20.2+1.0.0-1.el7.ngx.x86_64.rpm
#### Debian

BashCopysudo dpkg -i nginx-module-ometascan_1.20.2+1.0.0-1_buster_amd64.deb
### Custom NGINX Configuration Directives

This is to load the new NGINX integration module and configure all relevant settings in the NGINX configuration file (e.g. **/etc/nginx/nginx.conf**).

**Example 1:**

load_module modules/ngx_http_ometascan_module.so;
events {
worker_connections 4096;
}
http {
client_max_body_size 1000M;
server {
listen 80;
server_name localhost;
location ^~ / {
ometascan_pass http://icap_server.domain:8043;
ometascan_methods POST PUT;
ometascan_read_timeout 1d;
proxy_pass http://back_end_server.domain:8000;
}
}
}Info

- `client_max_body_size` Sets the maximum allowed size of the client request body. If the size in a request exceeds the configured value, a 413 error (Request Entity Too Large) is returned to the client. Please be aware that browsers cannot correctly display this error. Setting size to 0 disables checking of client request body size.
- `ometascan_pass` Set URL of the MD ICAP Server
- `ometascan_methods POST PUT;` (only enables scans for POST and PUT methods)

**Example 2 (Load Balancing):**

load_module /etc/nginx/modules/ngx_http_ometascan_module.so;
http {
client_max_body_size 1000M;
upstream icap {
server icap_server.first.domain:8043;
server icap_server.second.domain:8043;
}
server {
listen 80;
server_name localhost;
location ^~ / {
ometascan_pass http://icap;
ometascan_methods POST PUT;
ometascan_read_timeout 1d;
proxy_pass http://back_end_server.domain:8000;
}
}
}
## Configure HTTPS

**Generate the certificate**

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout certs.key -out certs.pem

**HTTPS Example Config**

BashCopyload_module /etc/nginx/modules/ngx_http_ometascan_module.so;
http {
client_max_body_size 1000M;
upstream icap {
server icap_server.first.domain:8043;
server icap_server.second.domain:8043;
}
server {
listen 443 ssl;
server_name localhost;
ssl_certificate /path/to/certs.pem;
ssl_certificate_key /path/to/certs.key;
location ^~ / {
ometascan_pass http://icap;
ometascan_methods POST PUT;
ometascan_read_timeout 1d;
proxy_pass http://back_end_server.domain:8000;
}
}
}Info

Add `ssl`, `ssl_certificate` and `ssl_certificate_key` variables. Refer [here](http://nginx.org/en/docs/http/configuring_https_servers.html) for more information regarding nginx HTTPS configuration.

## Performance Testing Results

Info

Performance test results are performed in a controlled environment and serve only as a reference. The results demonstrate the raw throughput capacity for the MD ICAP Server, outside of any scanning activity performed by MetaDefender Core. Overall solution performance will depend on several factors including available system resources, file content (dataset) and network performance.

### Test Environment

| Component | Value |
| --- | --- |
| CPU cores | 8 |
| RAM | 8 GB |
| Storage | 50 GB |
| CPU limit | 4000MHz |
| Squid caching | No caching |
| files in dataset | 542 (500KB-1MB) |
| Dataset size (run 10x) | 378MB |
| Simultaneous users (threads) | 100 |
| Total requests | 542000 |

### Results

| Metric | **Client - Backend** | **Client - Squid - Backend** | **Client - Squid - MD ICAP - Backend ** | **Client - Nginx - MD ICAP - Backend** |
| --- | --- | --- | --- | --- |
| Request throughput (req/s) | 105.9 | 91.8 | 17.8 | **65.6** |
| Data throughput (kB/s) | 75629 | 65549 | 13000 | **46861** |
| Total time (sec) | 5118 | 5905 | 29774 | **8260** |
