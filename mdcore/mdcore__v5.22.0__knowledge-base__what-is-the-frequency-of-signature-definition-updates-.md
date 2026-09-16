<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/what-is-the-frequency-of-signature-definition-updates- -->

# What is the frequency of signature/definition updates on MetaDefender Core?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

There are two parameters that determine the frequency of signature/definition updates:

- The frequency with which each antivirus vendor releases updates

  - [Windows](https://my.opswat.com/anti-malware-engine-status/windows)
  - [Linux](https://my.opswat.com/anti-malware-engine-status/linux)
- The configuration setting on your MetaDefender Core or MetaDefender Kiosk installation that specifies the time interval between system checks and applying new updates.

Please Note:

Most antivirus vendors release definitions at least once per day. Many have multiple daily releases. Some vendors release updates on weekends while others do not.

If you have configured OPSWAT's **Online Update** feature to auto-apply updates (i.e. via direct internet connection), you can then also configure the update interval to suit your preference.

When configured for **Automatic Updates**, MetaDefender Core will check for available scan engine (and signature/definition database) updates on a regular basis. To learn more about engine and database update checks, visit [Regular Maintenance](/docs/mdcore/v5.22.0/operating/regular-maintenance).

Please Note:

The default interval setting for a new installation of MetaDefender Core or MetaDefender Kiosk is every 4 hours (once per day).

If you have toggled settings to **Manual Update** (aka **Offline Updates**) the frequency is controlled by how often you download and apply the offline update package from OPSWAT.

Pro Tip:

Most of MetaDefender Core’s included scan engines (and their signature/definition databases) can be configured to either **Internet** (**Automatic**), **Local** (**Automatic**) or **Manual** updates:

● To learn about configuring updates for MetaDefender Core V5, visit [Engines Update Configuration](/docs/mdcore/v5.22.0/configuration/engines-update-configuration).

For engines where update settings cannot be toggled, updates will be incorporated into new MetaDefender Core version releases.

Support:

For further guidance regarding **Scan Engine Signature/Definition Updates**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
