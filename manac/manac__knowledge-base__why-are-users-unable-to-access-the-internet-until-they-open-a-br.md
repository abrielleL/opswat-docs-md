<!-- source: https://www.opswat.com/docs/manac/knowledge-base/why-are-users-unable-to-access-the-internet-until-they-open-a-br -->

# Why are users unable to access the internet until they open a browser to a site outside the local network

## [DHCP](/docs/manac/knowledge-base/why-are-users-unable-to-access-the-internet-until-they-open-a-br#dhcp)

- If possible, ensure that the Captive Portal API option, 114 is configured for the DHCP scope in question.
- Detailed instructions can be found here: [How to configure DHCP option 114 on Windows DHCP server](/docs/manac/knowledge-base/how-to-configure-dhcp-option-114-on-dhcp-server)
- **Caveats:**

  - In a Windows shop, your DHCP server must be running at least Server 2019.
  - It’s possible this option will be finicky to get working with iOS devices and unsupported on Linux, depending on your distro.

## [Layer 2 Integration](/docs/manac/knowledge-base/why-are-users-unable-to-access-the-internet-until-they-open-a-br#layer-2-integration)

If the DHCP option doesn’t work for large portions of users, or just gives an inconsistent user experience, there are other options.

If enforcement in your NAC environment is currently happening via ACL updates on a Layer 3 switch, this could also be contributing to a suboptimal captive portal experience. This is due to the fact that ACL updates take time, and your endpoints' captive portal detection systems may already thinl they are on the Internet before the device can be redirected.

If this sounds familiar, it’s useful to explore the cost/benefit proposition of moving to Layer 2 enforcement, which happens right at the switch port or wireless controller/access point.

In this architecture, enforcement happens as part of the RADIUS Authorization process. Hence the endpoint is blocked if needed, before it can even pull an IP address. This eliminates any window for captive portal detection to report a false positive.

There are many other upsides to Layer 2 enforcement, which the NAC team and you Account Manager will be happy to explore with you in detail.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
