<!-- source: https://www.opswat.com/docs/mddownloader/v3.4.0/knowledge-base/how-can-i-set-proxy-server-for-the-product -->

# How can I set proxy server for the product?

## [Linux](/docs/mddownloader/v3.4.0/knowledge-base/how-can-i-set-proxy-server-for-the-product#linux)

Set variables https_proxy in file `/etc/default/ometadownloader`

## [Windows](/docs/mddownloader/v3.4.0/knowledge-base/how-can-i-set-proxy-server-for-the-product#windows)

Under Windows use the netsh tool to set the proxy, e.g.: `netsh winhttp set proxy <ADDRESS>`

In same cases setting the proxy with netsh is not sufficient. In that case set the proxy by starting Internet Explorer with SYSTEM rights and configure the proxy in the settings. To do this please follow this [article](http://social.technet.microsoft.com/wiki/contents/articles/13710.how-to-configure-proxy-settings-for-configuration-manager-primary-sites-that-manage-cloud-services.aspx).

Info

You might need to configure Windows proxy to bypass local addresses if you can't access Web Management Console from the host itself. Consult netsh documentation for additional configuration options.
