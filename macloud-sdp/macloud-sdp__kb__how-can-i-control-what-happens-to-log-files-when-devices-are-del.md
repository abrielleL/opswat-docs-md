<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-can-i-control-what-happens-to-log-files-when-devices-are-del -->

# How can I control what happens to log files when devices are deleted?

This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

Adding and removing devices is a normal, but often hectic, part of managing a network. Which is why OPSWAT strives to facilitate streamlined onboarding and offboarding for MetaDefender IT Access users, thereby minimizing the burden on IT administrators.

- In terms of **Onboarding**, all account associations are embedded in the installer.
- In terms of **Offboarding**, when a user uninstalls the MetaDefender Endpoint, MetaDefender IT Access will automatically detect the event and remove that device from the associated account.

Large networks, with frequent device onboarding and offboarding, can introduce noise into the log management landscape, leading to frustration, wasted time and effort. To combat this, MetaDefender IT Access administrators have the option to adjust the default behavior for log retention.

Pro Tip:

MetaDefender IT Access’s default behavior is to **Archive** the logs for any deleted device for the duration of the data retention period. This period is 30 days for standard accounts, but customers are welcome to [Contact The OPSWAT Sales Team](https://www.opswat.com/contact) for details on how to upgrade their account and extend their data retention period.

The alternative to archiving data for deleted devices is to enable **Purge** mode, whereby a device deletion event will trigger the immediate deletion of all associated MetaDefender IT Access log files.

## [How to enable Purge mode](/docs/macloud-sdp/kb/how-can-i-control-what-happens-to-log-files-when-devices-are-del#how-to-enable-purge-mode)

1. Log into the **MetaDefender IT Access Console** and navigate to **Settings>Global>Device Data.**
2. Next to **Data retention behavior**, check the **Purge** option, as illustrated in the screenshot below.
3. Finally, to enable your settings, click **Save**.

Support:

If you have any queries, concerns or issues around **Managing The Log Files For Deleted Client Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
