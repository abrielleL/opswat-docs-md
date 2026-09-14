<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-is-core-receiving-http-403-or-timeout-errors-when-downloadin -->

# Why Is Core Receiving HTTP 403 or Timeout Errors when downloading engine updates from OCM?

#### [Issue](/docs/mdcore/knowledge-base/why-is-core-receiving-http-403-or-timeout-errors-when-downloadin#issue)

You may see log messages similar to the following in your Core system:

HtmlCopy[WARNING] 2025.04.10 18:23:40.925: (common.communication) Error while downloading file, url='QUrl("http://XXXXX:9000/console/core/metadescriptor?version=5.13.3&deployment=XXXXX&serial=0")', http_status='0', error='UnknownNetworkError', errorDetails='Connection timed out' [msgid: 485]
[ERROR ] 2025.04.10 18:23:40.925: (common.update) Error parsing metadescriptor, message='Could not download metadescriptor' [msgid: 282]
[WARNING] 2025.04.10 18:23:51.796: (common.communication) Error while downloading file, url='QUrl("http://XXXXX:9000/console/core/metadescriptor?version=5.13.3&deployment=XXXXX&serial=0")', http_status='403', error='ContentAccessDenied', errorDetails='Error transferring http://XXXXX:9000/console/core/metadescriptor?... - server replied: Forbidden' [msgid: 485]
#### [**Cause**](/docs/mdcore/knowledge-base/why-is-core-receiving-http-403-or-timeout-errors-when-downloadin#cause)

These messages usually mean that Core is having trouble connecting to OCM (OPSWAT Central Management). It may be caused by:

- Network timeout or proxy issues
- Port 9000/tcp being blocked
- Restrictions in your firewall or proxy

#### [Solution](/docs/mdcore/knowledge-base/why-is-core-receiving-http-403-or-timeout-errors-when-downloadin#solution)

Please check the following:

1. **Proxy or Network Settings** Make sure your network allows Core to connect to the OCM server. If you're using a proxy, verify that it allows traffic to the OCM address on port **9000/tcp**.
2. **Firewall Rules** Ensure port **9000/tcp** is open between Core and OCM. This is required for downloading updates and descriptors.
3. **More Info on Ports** For a full list of ports used by OCM, see the documentation here: [Recommended System Requirements - OPSWAT Central Management v7 - Legacy](https://www.opswat.com/docs/ocm/installation/recommended-system-requirements#ports-used).

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
