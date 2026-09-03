<!-- source: https://www.opswat.com/docs/mdcloud/operation/safe-url-redirect -->

# Safe URL Redirect

Safe URL Redirect is a service to protect users from malicious URLs, domains and IP addresses. The intent of this feature is to be integrated into other products that have links from unknown sources accessed by users. The safe URL will intercept the user request in the browser and prevent access to malicious websites.

It is a fast and unintrusive feature that makes browsing the web safer.

## [How to Use It](/docs/mdcloud/operation/safe-url-redirect#how-to-use-it)

Any address can be scanned before accessing by replacing the address with the following URL:

- [https://metadefender.opswat.com/safe-redirect/**<address](https://metadefender.opswat.com/safe-redirect/**%3Caddress)>**

The <address> field needs to be URL encoded and can be the any of the followings:

- Url
- Domain
- IP address

Example URL: <https://metadefender.opswat.com/safe-redirect/http%3A%2F%2Fwww.opswat.com>

## [How It Works](/docs/mdcloud/operation/safe-url-redirect#how-it-works)

When the user opens a URL using the safe URL redirect feature we scan the given address before the user reaches it. If the given address is clean then we redirect the user seamlessly without any interruptions. If the address is marked as infected by at least one of our engines, a warning page is displayed instead to notify the user about the potential danger and let them decide to stop or continue even if it's an infected site. The user can see the engines marking the address as malicious, and the complete scan result can be accessed by pressing the "View Details" button.

This feature uses the apikey of the logged in user from [https://metadefender.opswat.com](https://metadefender.opswat.com/). When the limit is exceeded, there will be a warning page instructing the user to upgrade account.
