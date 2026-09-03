<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/resolved-os-patch-ubuntu-mde -->

# How do I solve Missing OS Patch issues on MetaDefender Endpoint/MetaDefender IT Access managed Ubuntu Linux devices?

This article applies to the current MetaDefender IT Access Console and API, and all MetaDefender Endpoint releases deployed on Ubuntu Linux systems.

MetaDefender IT Access provides variety compliance options tailored to different operating systems. Specifically for Ubuntu devices, we've implemented a dedicated rule aimed at compelling users to regularly update their operating systems. This involves monitoring the current patching status and detecting any available but uninstalled updates. This proactive approach ensures that the system remains current, benefiting from the latest enhancements and security patches, ultimately bolstering device stability and security.

Administrators have the flexibility to determine the frequency at which users are prompted to update their operating system. This can be configured by activating the '**Update(s) have been available**' condition under **Policy > Deep Compliance > Operating System > Linux**, allowing administrators to specify the desired update interval in days. A smaller number indicates a more frequent check for operating system updates.

To remediate OS update compliance issues on managed Ubuntu Linux devices, please follow the relevant instructions below.

Warning

These instructions are based on Ubuntu 20.04.05 LTS and will vary slightly depending on your Ubuntu version.

## [Through Software Updater](/docs/macloud-sdp/kb/resolved-os-patch-ubuntu-mde#through-software-updater)

1. Go to Applications, search for Software Updater, then click on the result.

The Software Updater will initially search for available updates and then display a list of them with checkboxes. You can uncheck any updates you do not want. To update everything, simply leave all the checkboxes checked.

2 . Click “Install now“ once you are satisfied with the selections.

Authentication, and the installation will begin.

This process may take some time, and you might be prompted to reboot your machine once it's finished.

## [Through Terminal](/docs/macloud-sdp/kb/resolved-os-patch-ubuntu-mde#through-terminal)

1. Open terminal and enter the following command to check for updates.

BashCopysudo apt update

2. Then, execute the flowing command to apply package updates and patches.

Type `Y` and press Enter to confirm.

## [Verify the update with MetaDefender Endpoint](/docs/macloud-sdp/kb/resolved-os-patch-ubuntu-mde#verify-the-update-with-metadefender-endpoint)

Once the installation is done, ensure that MetaDefender Endpoint is launched. Then, right-click on the MetaDefender Endpoint tray **Icon** and click **Recheck**.

Support:

If you have followed the relevant guidelines but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint/MetaDefender IT Access** **Managed Ubuntu Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
