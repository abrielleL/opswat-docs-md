<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-control-what-happens-to-log-files-when-devices-are-del -->

# How can I control what happens to log files when devices are deleted in MetaDefender Endpoint?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

Adding and removing devices is a normal, but often hectic, part of managing a network. Which is why OPSWAT strives to facilitate streamlined onboarding and offboarding for My OPSWAT Central Management users, thereby minimizing the burden on IT administrators.

- In terms of **Onboarding**, all account associations are embedded in the installer.
- In terms of **Offboarding**, when a user uninstalls the MetaDefender Endpoint, My OPSWAT Central Management will automatically detect the event and remove that device from the associated account.

Large networks, with frequent device onboarding and offboarding, can introduce noise into the log management landscape, leading to frustration, wasted time and effort. To combat this, My OPSWAT Central Management administrators have the option to adjust the default behavior for log retention.

> **Pro Tip:**
>
> My OPSWAT Central Management’s default behavior is to **Archive** the logs for any deleted device for the duration of the data retention period. This period is 30 days for standard accounts, but customers are welcome to [Contact The OPSWAT Sales Team](https://www.opswat.com/contact) for details on how to upgrade their account and extend their data retention period.

The alternative to archiving data for deleted devices is to enable **Purge** mode, whereby a device deletion event will trigger the immediate deletion of all associated My OPSWAT Central Management log files.

## How to enable Purge mode

1. Log into the **My OPSWAT Central Management Console** and navigate to **Settings>Global>Device Data>Endpoint Data.**
2. Next to **Data retention behavior**, check the **Purge** option, as illustrated in the screenshot below.
3. Finally, to enable your settings, click **Save**.

![](https://uploads.developerhub.io/prod/97qW/7lqizhyquhds765q7jedzzvxjrhtrjxea8t49e4gvs251iee7dgya0jlp6fgew1n.png)

> **Support:**
>
> If you have any queries, concerns or issues around **Managing The Log Files For Deleted Client Devices**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
