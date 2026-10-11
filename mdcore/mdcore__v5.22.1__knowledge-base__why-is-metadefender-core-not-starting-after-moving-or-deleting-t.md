<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-is-metadefender-core-not-starting-after-moving-or-deleting-t -->

# Why is MetaDefender Core not starting after moving or deleting the certificates from the initial location?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

MetaDefender Core relies on nginx for its web interface. On startup, nginx will check the configured location for the SSL certificate, will attempt to load it into C:\Windows\Temp\ometascan and then will start and be ready to accept connections.

If at any time the certificate is deleted or removed, nginx will no longer be able to start and this will cause Core to completely fail. The SSL configuration is not easily accessible to find the previously configured certificate and paths, making recovering this information not practical.

To resolve this, the best option will be to reset the SSL configuration and, once the Core service is successfully restarted using HTTP, the certificate can be imported back into the MetaDefender Core certificate inventory and the HTTPS configuration can be reenabled.

To do this, simply follow the steps outlined here: [HTTPS Configuration Removal Tool](/docs/mdcore/v5.22.1/troubleshooting/https-disablement-tool)

Please Note:

The SSL configuration reset tool will normally not affect any other part of the MD Core configuration, but best practices are to perform a configuration export before running this tool.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
