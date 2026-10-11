<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/knowledge-base/how-can-i-set-proxy-server-for-the-product -->

# How to Integrate a Proxy Server with MetaDefender Update Downloader

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Linux](/docs/mddownloader/v3.5.0/knowledge-base/how-can-i-set-proxy-server-for-the-product#linux)

**For Linux installations of MetaDefender Update Downloader**
To configure MetaDefender Update Downloader to use a proxy server:

1. Change to the following directory: **/etc/default**
2. Open the **ometadownloader** file using a text editor.
3. Locate the following line: `https_proxy=http://host:port`
4. Update the proxy address and port to match your environment. For example: `https_proxy=http://10.10.1.0:8080`
5. Save the file after making the changes.

## [Windows](/docs/mddownloader/v3.5.0/knowledge-base/how-can-i-set-proxy-server-for-the-product#windows)

### [**For Windows installations of MetaDefender Update Downloader**](/docs/mddownloader/v3.5.0/knowledge-base/how-can-i-set-proxy-server-for-the-product#for-windows-installations-of-metadefender-update-downloader)

MetaDefender Update Downloader can use the proxy settings configured at the Windows operating system level.

The `netsh winhttp` command configures the Windows WinHTTP proxy settings.

#### [**Configure the proxy server**](/docs/mddownloader/v3.5.0/knowledge-base/how-can-i-set-proxy-server-for-the-product#configure-the-proxy-server)

1. Open **Command Prompt as Administrator**.
2. Run the following command:

   `netsh winhttp set proxy <proxy_server>:<port>`

   For example:

   `netsh winhttp set proxy 10.1.0.10:8080`
3. After the command is completed, Windows will display the current WinHTTP proxy configuration.

   Example:

   `Current WinHTTP proxy settings:`

   `Proxy Server(s) : 10.1.0.10:8080`

   `Bypass List : (none)`

#### [**Verify the proxy configuration**](/docs/mddownloader/v3.5.0/knowledge-base/how-can-i-set-proxy-server-for-the-product#verify-the-proxy-configuration)

To confirm that the proxy server is configured correctly:

1. Open **Command Prompt**.
2. Run the following command:

   `netsh winhttp show proxy`
3. The current WinHTTP proxy settings will be displayed.

   Example:

   `Current WinHTTP proxy settings:`

   `Proxy Server(s) : 10.1.0.10:8080`

   `Bypass List : (none)`

In some cases, setting the proxy with `netsh winhttp set proxy` is not sufficient. Windows services running under the Local System account read proxy settings from their own profile, not from the netsh setting. In that case, you may need to set the proxy by starting Edge with SYSTEM rights and configuring the proxy in Internet Options.

**Applies to**

Windows services (such as OPSWAT products) that cannot reach the internet after the proxy was set with netsh.

**Set the proxy through Internet Options as SYSTEM**

1. Download PsTools from [Microsoft](https://download.sysinternals.com/files/PSTools.zip) and extract `PsExec.exe`.
2. Open Command Prompt as Administrator.
3. Run:

 `psexec -i -s control.exe inetcpl.cpl`

This opens the Internet Options window as the SYSTEM account.

4. Go to the **Connections** tab and click **LAN settings**.
5. Select **Use a proxy server**, enter the proxy address and port, and click **OK**.
6. Restart the affected service.

Note: On older systems you can also run `psexec -i -s "C:\Program Files\Internet Explorer\iexplore.exe"` and open Internet Options from the IE menu. On Windows 11, use the `control.exe inetcpl.cpl` command above instead.

Info

You might need to configure Windows proxy to bypass local addresses if you can't access Web Management Console from the host itself. Consult netsh documentation for additional configuration options.
