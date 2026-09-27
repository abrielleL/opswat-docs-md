<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/troubleshooting/cannot-access-protected-apps-from-okta -->

# Cannot access protected apps due to CORS error

## 1. Issue Summary

User currently can not access to Microsoft Apps (Word, Excel, …) from Okta, due to a callback error that originates from MetaDefender Endpoint with api returns cors error.

## 2. Root Cause

Chromium 142 introduces a new [Local Network Access security policy](https://chromestatus.com/feature/5152728072060928) requirement. Requests from web pages to loopback addresses such as `localhost` / `127.0.0.1` are blocked unless the user (or an admin policy) explicitly grants access.

Because **gears-beta.opswat.com** communicates with a local server to verify compliance before access, these restrictions can disrupt normal operation.

> **Info**
>
> Starting in **Chromium-based browsers v142+** (released Oct 28, 2025)—including Chrome, Edge, Brave, and Opera—access to protected apps from Okta may fail due to new local-network security rules.

## 3. Resolution

**Step 1: Enable the “Local network access” flag in the browser to log in to Okta**

- Open Settings → Privacy and security
- Locate the site to enable this flag

![](https://uploads.developerhub.io/prod/2x2P/p85cxcyja7yiltvcce41dkhqinfe0p5vjr2h0ncf7pskcsfagiiukoxnfop262wy.png)

- Expand and Locate the “Local network access” flag, and select “Allow”

![](https://uploads.developerhub.io/prod/2x2P/wzn0q49ohqmucp0judufzglpq8pf0tllhklvz55r994qf88nb2qeg6eecuzaevlf.png)

**Step 2: Apply This Setting Across an Enterprise**

Enterprise administrators can deploy a Chrome and/or Edge policy to set the “Local Network Access” setting to “Allow” for your website.

Please refer to:

- [Chrome Enterprise Policy List & Management Documentation](https://chromeenterprise.google/policies/#LocalNetworkAccessAllowedForUrls)
- [Microsoft Edge Browser Policy Documentation](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/localnetworkaccessallowedforurls)
- [Managing the Chrome v142Local Network Access Prompt](https://support.beyondidentity.com/hc/en-us/articles/34457691192215-Managing-the-Chrome-v142Local-Network-Access-Prompt#:~:text=Enter%20chrome://flags%20in,the%20launch%20of%20Chrome%20M141).)

## 4. Next Actions

To improve UX when checking the “Local network access” permission, you can optionally query this permission at runtime. Although not required, this check allows you to notify users proactively and provide clearer guidance if the permission is missing.

## 5. References

- [Error message - Permission was denied for this request to access the unknown address space](https://www.dynamsoft.com/web-twain/docs/faq/chromium-142-local-network-access-issue.html)
- [New permission prompt for Local Network Access  |  Blog  |  Chrome for Developers](https://developer.chrome.com/blog/local-network-access#:~:text=Local%20Network%20Access%20restricts%20the,is%20restricted%20to%20secure%20contexts.)

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
