<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-do-i-revert-metadefender-kiosk-to-a-previous-state-using-dee -->

# How do I revert MetaDefender Kiosk to a previous state using Deep Freeze software?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows or Linux systems.

Faronics Deep Freeze Enterprise software can be used to restore the MetaDefender Kiosk to its optimal original state after every scan session.

To configure your system to revert after each session, please follow the steps below:

- Ensure that Deep Freeze Enterprise edition is available.
- Install Deep Freeze Enterprise edition *without* enabling **Deep Freeze Local Policies.**
- Go to your **Kiosk Management Console>Configuration>Kiosk UI> Kiosk Interface**, then enable the Kiosk to **Reboot At End Of Session** as highlighted in the image below**.**

- Configure Kiosk to your preferences and then activate the product.
- Finally, take the system snapshot with your Faronics Deep Freeze software.

Pro Tip:

Faronics Deep Freeze ‘protects endpoints by Freezing a snapshot of a computer’s desired configuration and settings defined by the IT Admin. With an instant reboot, any unwelcome or unwanted changes are removed from the system, restoring it to its pristine Frozen state.’

Support:

If you have any difficulty **Reverting MetaDefender Kiosk to a Previous State Using Deep Freeze Software**, please follow these instructions on [How To Create a Support Package](https://docs.opswat.com/mdkiosk/troubleshooting#creating-the-package), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
