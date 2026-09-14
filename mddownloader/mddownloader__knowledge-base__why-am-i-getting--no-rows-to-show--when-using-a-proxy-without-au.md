<!-- source: https://www.opswat.com/docs/mddownloader/knowledge-base/why-am-i-getting--no-rows-to-show--when-using-a-proxy-without-au -->

# Why Am I Getting "No Rows to Show" When Using a Proxy Without Authentication in Browser Settings?

**Problem**

When you set the proxy without authentication in Edge or Chrome, it typically applies to the system proxy settings. However, the MetaDefender Update Downloader relies on WinHTTP instead of WinINet, meaning it does not inherit the browser's proxy settings.

As a result, you may encounter the error: "No rows to show."

**Solution**

Since the MetaDefender Update Downloader currently does not provide a UI option to configure proxy settings, you need to set the WinHTTP proxy manually using the `netsh` command:

1. Open Command Prompt as Administrator:

   - Press `Win + R`, type `cmd`, and press `Ctrl + Shift + Enter`.
2. Set the WinHTTP Proxy:

   - Run the following command, replacing `<proxy_ip>:<port>` with your actual proxy details:

HtmlCopynetsh winhttp set proxy <proxy_ip>:<port>

Example:

HtmlCopynetsh winhttp set proxy 192.168.1.100:8080

3. Refresh the Update Downloader web console and click "Update All."

4. Check if the page now displays correctly.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support)
