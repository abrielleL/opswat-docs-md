<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/where-can-i-find-faqs-about-metadefender-kiosk-s-antivirus-signa -->

# What is the frequency of MetaDefender Kiosk's antivirus signature/definition updates?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk V4 releases.

MetaDefender Kiosk relies on its underlying MetaDefender Core server to manage antivirus engine signature/definition updates.

The frequency of these updates is configured via the MetaDefender Core server to which the Kiosk is connected, and is also dependent on the frequency with which AV engine vendors release their updates.

So, the two parameters that determine the frequency of signature/definition updates are:

- The configuration setting on your MetaDefender Core installation which specifies the time interval between system checks and applying new updates. Go to your **MetaDefender Core Management Console>Settings>Module Update** to make changes, as highlighted in the image below.

- The frequency with which each antivirus vendor releases an update. Most vendors release definitions at least once per day, while many have multiple daily releases. Some vendors release updates over weekends, while others do not. Due to the high frequency of signature/definition updates, it is recommended that you allow for updates at least once per day.

Please Note:

If you use OPSWAT’s online update mechanism to auto-apply updates (i.e. via direct internet connection), you can configure the update interval to suit your needs.

The default setting for MetaDefender Core V4 and above is once every 4 hours.

If you are using the manual update option (i.e. not automated, offline updates), the frequency is controlled by how often you manually download and apply the offline update packages from [My OPSWAT](https://my.opswat.com/).

Support:

If you have any difficulty **Configuring and Applying MetaDefender Kiosk and Core’s Regular AV Engine Signature/Definition Updates**, please follow these instructions on [How To Create a Support Package](https://docs.opswat.com/mdkiosk/troubleshooting#creating-the-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
