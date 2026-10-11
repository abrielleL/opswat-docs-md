<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-seeing--unable-to-find-mft-server--error-on-the-kiosk- -->

# Why am I seeing "Unable to find MFT server" error on the Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info:

- This article applies to all Kiosk versions

Customers may encounter an error on the Kiosk stating:

HtmlCopyUnable to find MFT server

Even though network paths and firewall rules appear correctly configured. Network monitoring may still show partial communication between the Kiosk and the MFT server.

## [**Observed Behavior in Logs (e.g for URL is opswat.com)**](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-seeing--unable-to-find-mft-server--error-on-the-kiosk-#observed-behavior-in-logs-eg-for-url-is-opswatcom)

HtmlCopyRestServer.cpp#9930 RestServer::CheckWebSessionSurvey(): {No session} Couldn't resolve host name(6)
HTTPMessenger.cpp#63 CurlWrapper::LogMessage(): Error calling GET "https://opswat.com/vault_rest/version" : 28. Failed to connect to opswat.com port 443 after 21076 ms: Couldn't connect to server. Called in func HTTPMessenger::GenericGET() at line 226
HTTPMessenger.cpp#63 CurlWrapper::LogMessage(): Error calling GET "https://opswat.com/vault_rest/version" : 6. Could not resolve host: opswat.com. Called in func HTTPMessenger::GenericGET() at line 226
Trace calls:
Error calling GET "http://opswat.com/vault_rest/version" : 28. Failed to connect to opswat.com port 80 after 21056 ms: Couldn't connect to server. Called in func HTTPMessenger::GenericGET() at line 226
Trace calls:
SocketServer.hpp#204 SocketServer::OnOpen(): Open connection 127.0.0.1:52988

Analysis of the Kiosk and MFT logs revealed the following:

- Attempts to reach `opswat.com` failed with errors such as:

  - `Could not resolve host`
  - `Failed to connect to server after timeout`
- Local Service Status

  - Successful local socket connections (e.g., `127.0.0.1:52988`) indicate the Kiosk service itself is running correctly.

## [**Cause**](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-seeing--unable-to-find-mft-server--error-on-the-kiosk-#cause)

The errors suggest DNS resolution issues and/or network connectivity problems between the client Kiosk and the Vault server. Despite proper firewall and service configuration, the client is unable to reach the target servers using the hostnames.

## [**Recommended Troubleshooting Steps**](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-seeing--unable-to-find-mft-server--error-on-the-kiosk-#recommended-troubleshooting-steps)

- **Verify Server Hostnames and Reachability**

  - Confirm that `opswat.com` is correct.
  - Attempt to reach the servers using their IP addresses to bypass DNS issues.
- **Test DNS Resolution**

HtmlCopynslookup opswat.com

- **Test Network Connectivity**

HtmlCopyping opswat.com
curl -v https://opswat.com/vault_rest/version

- **Check Firewall, Proxy, and Routing Rules**

  - Ensure outbound connections on ports 80 and 443 are allowed.
  - Verify that there is no proxy or routing configuration blocking access.
- **Review Local Hosts File (Optional)**

  - If DNS cannot be resolved correctly, consider adding entries to the local hosts file as a temporary workaround.

## [**Conclusion**](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-seeing--unable-to-find-mft-server--error-on-the-kiosk-#conclusion)

The “Unable to find MFT server” error is generally caused by network/DNS issues rather than Kiosk or MFT service failures. Confirming hostname resolution and connectivity from the client machine usually resolves the problem.

Workarounds: Review Local Hosts File (Optional)

If DNS cannot be resolved correctly, consider adding entries to the local hosts file as a temporary workaround.

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
