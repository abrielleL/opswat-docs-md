<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/check-cached-objects-properties -->

# Check cached objects properties

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This article describes how to check if an object is cached by Symantec Blue Coat ProxySG and its current properties.

## [Prerequisites](/docs/mdicap/v5.14.1/integrations/check-cached-objects-properties#prerequisites)

1. ICAP is setup with Blue Coat.
2. Blue Coat caching is enabled (default).

   - See: [4.4.2.5 Disable Symantec Blue Coat ProxySG caching](/docs/mdicap/v5.14.1/integrations/disable-symantec-blue-coat-proxysg-caching)

## [Step-by-step guide](/docs/mdicap/v5.14.1/integrations/check-cached-objects-properties#step-by-step-guide)

Use the following syntax to check if an object is in cache:

https://<proxyip>:8082/CE/Info/<protocol name,

e.g. http>/<url without the protocol specification, e.g. without http://>

Example: The check if the following object is in the cache: <http://www.bluecoat.com/sites/default/themes/bc_pandemonium/css/docviewer.css>

Enter the following in the browser: <https://1.2.3.4:8082/CE/Info/http/www.bluecoat.com/sites/default/themes/bc_pandemonium/css/docviewer.css>

If the object is in the cache, you will obtain a table providing details on the cached object such as:

## [Related Information](/docs/mdicap/v5.14.1/integrations/check-cached-objects-properties#related-information)

Error rendering macro 'contentbylabel' : parameters should not be empty
