<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-is-metadefender-core-failing-to-connect-via-proxy- -->

# Why is MetaDefender Core Failing to Connect via Proxy?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

#### [Issue:](/docs/mdcore/v5.22.0/knowledge-base/why-is-metadefender-core-failing-to-connect-via-proxy-#issue)

MetaDefender Core requires a correctly configured proxy to establish internet connectivity for:

- Downloading engine packages
- Licensing the product
- Other

If the proxy configuration is incorrect, MetaDefender Core may fail to connect to the internet, even if a proxy server has been added.

MetaDefender Core uses its own proxy settings and does not rely on the operating system configuration.

The proxy entry must be defined using only IP or domain name and port.

Proxy URLs with prefixes (e.g., http:// or https://) are not supported.

When the proxy is incorrectly configured, you may see warnings in the log file:

- Log file location:`<Core installation folder>\data\logs\Core.log`
- Example warning message: `[WARNING] date / time (common.communication) Error while downloading file, url=‘’, http_status='0', error='ProxyNotFoundError', errorDetails='Unknown error' [msgid: 485]`

#### [Resolution:](/docs/mdcore/v5.22.0/knowledge-base/why-is-metadefender-core-failing-to-connect-via-proxy-#resolution)

Open MetaDefender Core UI → Settings → Network.

Review the Proxy Server configuration.

✅ Correct format:

- `proxy.company.com port 8080`
- `10.10.10.10 port 8080`

❌ Incorrect format:

- [http://proxy.company.com](http://proxy.company.com/) `port 8080`
- [https://10.10.10.10](https://10.10.10.10/) `port 8080`

If your proxy entry includes`http://`or `https://`, remove the prefix.

Save the settings and retry the proxy connection.

#### [Prevention:](/docs/mdcore/v5.22.0/knowledge-base/why-is-metadefender-core-failing-to-connect-via-proxy-#prevention)

If MetaDefender Core cannot reach the internet via proxy:

- Ensure the proxy server is entered as IP or domain + port only.
- Avoid using http:// or https:// prefixes.
- Check the MetaDefender Core.log for related warnings (ProxyNotFoundError).

Correcting the format should resolve proxy connectivity issues.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
