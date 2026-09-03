<!-- source: https://www.opswat.com/docs/filescan/3.1.1/installation/notes-for-air-gapped-environments -->

# Air-gapped Systems

## [Important notes for air-gapped/offline systems](/docs/filescan/3.1.1/installation/notes-for-air-gapped-environments#important-notes-for-air-gappedoffline-systems)

- The normal installation process **requires an Internet connection** (moving the system into a DMZ is recommended)
- The offline installation process **does not require** any network connectivity: [Offline Installation](/docs/filescan/3.1.1/installation/offline-installation)
- Air-gapped systems will only receive updated features (like YARA) when installed and upgraded with an active Internet connection. We recommend moving the system into a DMZ during these windows.
- All third-party integrations (e.g. Reputation API, geolocation/WHOIS lookup) require an Internet connection.
- The "File download" feature is not available in air-gapped environments.

To run the sandbox in an offline environment without any errors, the following setting must be applied (after completing the installation process in an online environment).

Info

The "offlineMode=true" setting is automatically added when an [Offline Installation](/docs/filescan/3.1.1/installation/offline-installation) is performed.

There is no need to apply any futher changes!

Please open `/home/sandbox/sandbox/transform.cfg` using a text editor and add the following line:

transform.cfgCopyofflineMode=true

Please remember to **save the configuration file** and restart the `sandbox` service:

BashCopysudo service sandbox restart

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
