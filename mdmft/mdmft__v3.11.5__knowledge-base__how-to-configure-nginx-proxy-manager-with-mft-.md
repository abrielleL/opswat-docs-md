<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-to-configure-nginx-proxy-manager-with-mft- -->

# How to configure NGINX Proxy Manager with MFT?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Requirement:

You will need Docker to setup NGINX Proxy Manager. Full instruction guide can be found here:

[Full Setup Instructions | Nginx Proxy Manager](https://nginxproxymanager.com/setup/)

Default login password is admin@example.com/changeme

## [Adding Self-signed Certificate to NPM](/docs/mdmft/v3.11.5/knowledge-base/how-to-configure-nginx-proxy-manager-with-mft-#adding-self-signed-certificate-to-npm)

On the main page, choose SSL Certificates > Add SSL Certificate > Custom

Give the certificate a name, then choose the files accordingly on your computer. After finishing adding the certs, click save.

## [Adding a Proxy Host](/docs/mdmft/v3.11.5/knowledge-base/how-to-configure-nginx-proxy-manager-with-mft-#adding-a-proxy-host)

Go to Hosts > Proxy Hosts > Add Proxy Hosts

Fill in the required information.

**Domain Names**: The domain name that clients will access to your MFT server.

**Scheme**: https or http. This is the scheme that NPM use to talk with your MFT server.

**Forward Hostname / IP**: IP of your MFT server.

**Forward Port**: Port of your MFT server.

Adding the SSL by go to SSL tab, choose your already added SSL Certificate, turn on **Force SSL** option.

## [Troubleshooting](/docs/mdmft/v3.11.5/knowledge-base/how-to-configure-nginx-proxy-manager-with-mft-#troubleshooting)

When the MFT server is accessed through the NGINX Proxy, user might encounter this error

When we look into the headers of the *transfer_file* file request, we can see that there are some custom headers like *File_name*, *File_size*, *Group_id* and *Transfer_method* that MFT uses but by default, NGINX Proxy will ignore this header because it is not a standardize header like the others.

To fix this, we will go to NPM Dashboard, go to Advanced Setting of the Proxy Host, then add **either one of this 2 directive**:

Proxy HostCopyunderscores_in_headers on;
ignore_invalid_headers off;

**underscores_in_headers on;** will tell NGINX to **allow headers that have underscores in it**, which is what MFT use.

**ignore_invalid_headers off;** will tell NGINX to includes all the headers that is not valid (Valid names are composed of English letters, digits, hyphens, and possibly underscores), instead of discarding it in the request.

These directives are available on NGINX document: [Module ngx_http_core_module](https://nginx.org/en/docs/http/ngx_http_core_module.html#ignore_invalid_headers)

Support:

If you have followed the instructions above but are still unable to configure NGINX Proxy Manager with MFT, please follow these instructions on [How To Create a Support Package](https://www.opswat.com/docs/mdmft/troubleshooting/how-to-create-support-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support-services).
