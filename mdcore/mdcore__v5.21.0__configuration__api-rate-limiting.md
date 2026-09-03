<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/api-rate-limiting -->

# API Rate Limiting

If both are used, the settings from the UI will be applied instead of those in the `ini` file.

By default MetaDefender Core does not have any hard limit on the number of API requests coming to Nginx web server. However, in order to secure more your MetaDefender Core server, users are supported to limit the number of API requests to better control their server load and prevent potential DOS (Deny of service) attack (this feature has been introduced since MetaDefender Core version 4.15.0).

This configuration support is applicable to two REST requests on MetaDefender Core:

- [POST Login](/docs/mdcore/v5.21.0/metadefender-core#userlogin)
- [POST File Analysis](/docs/mdcore/v5.21.0/metadefender-core#fileanalysispost)

## [On Linux](/docs/mdcore/v5.21.0/configuration/api-rate-limiting#on-linux)

1. Create file `nginx_rate_limit.ini`in the directory `/usr/lib/ometascan/`

Note

The configuration files should be readable for the user that runs MetaDefender Core service (On linux: metascan, on Windows: service user).

2. Enter the following settings into the file:

nginx_rate_limit.iniCopymax_scan_request=X;
max_login_request=Y;

Whereas X, Y > 0 (If X or Y is not valid then MetaDefener Core will ignore and remain unlimited as default behavior).

When these configurations are set, MetaDefender Core will allow users to send maximum X "/login" REST request per minute, and maximum Y "/file" REST request per minute.

3. Restart MetaDefender Core service (ometascan).

## [On Windows](/docs/mdcore/v5.21.0/configuration/api-rate-limiting#on-windows)

1. Create file `nginx_rate_limit.ini` in the directory `<Installation Directory>\nginx`

Note

The configuration files should be readable for the user that runs MetaDefender Core service (On linux: metascan, on Windows: service user).

2. Enter the following settings into the file:

nginx_rate_limit.iniCopymax_scan_request=X;
max_login_request=Y;

Whereas X, Y > 0 (If X or Y is not valid then MetaDefener Core will ignore and remain unlimited as default behavior).

When these configurations are set, MetaDefender Core will allow users to send maximum X "/login" REST request per minute, and maximum Y "/file" REST request per minute.

3. Restart MetaDefender Core service (ometascan).

## [How this feature works:](/docs/mdcore/v5.21.0/configuration/api-rate-limiting#how-this-feature-works)

This feature fundamentally respects Nginx web server's rate limiting, learn more here: <https://www.nginx.com/blog/rate-limiting-nginx/>

For instance, users can set a limit for [POST File Analysis](/docs/mdcore/v5.21.0/metadefender-core#fileanalysispost) by setting "max_scan_request" = 600, that means MetaDefender Core only allows serving maximum 600 file process requests per minute. However due to the fact that NGINX mechanism tracks request at millisecond granularity, this limit means 1 request per 100 milliseconds, and thus users should not be able to send all 600 process requests at once (In this particular circumstance, every request coming after the allowed one will be rejected, and result in HTTP 503 response error code)
