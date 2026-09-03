<!-- source: https://www.opswat.com/docs/myop/knowledge-base/what-external-links-does-my-opswat-on-premises-server-connect-to -->

# What external links does the My OPSWAT On-premises server connect to?

By default, aside from the server URLs that are configured inside My OPSWAT on-premises console, My OPSWAT On-premises also connects to OPSWAT hosting servers regularly to collect updates for certain features.

- <https://update.dl.opswat.com>

  - Features: [Product Updates](/docs/myop/configuration/updates#product-updates), [Module Updates](/docs/myop/configuration/updates#module-updates)
  - How to disable it: Uncheck the **Auto-update when a new version is available** checkbox.
- <https://activation.dl.opswat.com>

  - Features: [License Management](https://docs.opswat.com/product-management/configuration/license-management)
  - How to disable it: It cannot be disabled if you are using an online license.
- ntp.ubuntu.com via UDP port 123

  - The default NTP time server for Ubuntu used to sync the internal system clock.
  - How to disable it: It cannot be disabled.

These URLs may need to be exempted from either your firewall or proxy to make sure relevant features can work properly.
