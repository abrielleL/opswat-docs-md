<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/client-certificates -->

# Client Certificates

While the browser cookie is a better user experience for the end-user and can be easier to integrate, it is not as reliable as the client certificate. Using them together can be very effective by first checking for the cookie and then falling back to the certificate if no cookie is present. This provides a better user experience when the cookie is present, but doesn’t fail if the cookie is not available for some reasons.

## How it works

When MetaDefender Endpoint is installed (persistent client) or run (on-demand client), a client certificate is silently installed in the personal certificate store of the current user* or keychain on the endpoint. This certificate is self-signed by OPSWAT.

- on Windows, you must use certmgr.msc to be able to verify it.

MetaDefender Endpoint uses the certificate Subject DN to provide the device identifier. The format of the Subject is:CN = [www.opswat.comO](http://www.opswat.comO) = OPSWATL = San FranciscoS = CAC = US0.9.2342.19200300.100.1.1 = {Device ID}

![](https://uploads.developerhub.io/prod/97qW/sdsg76sd1tkcfrkorrpagdkn0sileg1z0dm743od3j1hwgnqnk6gmbrb9g2uimyh.png)

The OID in dot notation above (0.9.2342.19200300.100.1.1) is also referenced as **device ID**.

When MetaDefender Endpoint is uninstalled (persistent client) or stopped (on-demand client) the persistent, it will remove the client certificate. Therefore the presence of the client certificate can be used to infer the presence of MetaDefender Endpoint and vice-e-versa.

Installing client certificates on endpoints is controlled in the My OPSWAT Central Management account settings.

![](https://uploads.developerhub.io/prod/97qW/4z83h9onw50y8qw5o45iiwujpswy9kl74i97bgq96fqi4mb5v9xo3ve93zixshj0.png)

The configuration needed to request and read the client certificate is different for every web server. There are typically options to make the certificate required or optional, as well as to enforce validation versus a CA (the OPSWAT CA in this case). If using Nginx for example, you would configure the server with the [ssl_verify_client](http://nginx.org/en/docs/http/ngx_http_ssl_module.html#ssl_verify_client) setting and a parameter of on, optional, or optional_no_ ca. The contents of the certificate would then be available to the server as variables $ssl_client_cert or $ssl_client_s_dn.

## Supported Browsers

As of November 10th, 2016, the client certificate is supported on both Windows and macOS.

| Browser | Windows | macOS |
| ---- | ---- | ---- |
| Chrome 34+ | Yes | Yes |
| Firefox* 28+ | Yes | Yes |
| Internet Explorer 8+ | Yes | No |
| Safari | No | Yes |

*: My OPSWAT Central Management agent couldn't insert client certificate to Firefox database if Firefox is running.
