<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/troubleshooting/azure-proxy -->

# Azure Proxy

Summarize Page    Connect to Cursor Connect to VS Code
## ["Something Unexpected Happened" Error Message When Loggin In](/docs/mdmft/v3.11.4/troubleshooting/azure-proxy#something-unexpected-happened-error-message-when-loggin-in)

This error message only appears if the HTTP response is "502 Bad Gateway." It may occur when the "Translate URLs in headers" or the "Translate URLs in body" options are enabled in Azure APP Proxy.

#### [Resolution](/docs/mdmft/v3.11.4/troubleshooting/azure-proxy#resolution)

Disable the "Translate URLs in headers" and "Translate URLs in body" options in the Azure APP Proxy settings to prevent this error.

---
