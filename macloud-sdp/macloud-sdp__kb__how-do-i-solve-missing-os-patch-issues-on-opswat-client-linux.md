<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-solve-missing-os-patch-issues-on-opswat-client-linux -->

# How do I solve Missing OS Patch issues on MetaDefender Endpoint/MetaDefender IT Access managed Linux devices?

This article applies to the current MetaDefender IT Access Console and API, and all MetaDefender Endpoint releases deployed on Linux systems.

Users running MetaDefender Endpoint on one or more Linux devices may occasionally see MetaDefender IT Access device compliance warnings/flags related to **Missing OS Patches**.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Missing Patches**.

Pro Tip:

Malware is frequently designed to exploit the vulnerabilities in outdated applications and operating systems in order to gain entry to and infect a system.

This is why keeping your operating system, OS security patches and all associated apps up-to-date is an essential element of risk reduction in cyber-security.

Pro Tip:

The following instructions are intended for *.deb* or *.rpm* based Linux systems, but steps may vary slightly depending on your distro and version.

To remediate Missing OS Patch related device compliance issues on your managed Linux devices, please follow the relevant instructions below.

## [Debian](/docs/macloud-sdp/kb/how-do-i-solve-missing-os-patch-issues-on-opswat-client-linux#debian)

1. To synchronize your update package index with the latest available update index online, open a **Terminal** and type **sudo apt-get update**, then enter your admin password as prompted.

2. Next, to install the latest versions of all packages currently installed on your system, type **sudo apt-get upgrade** then hit **Enter.**

3. Alternatively, you can include the install of selected packages after the standard upgrades by typing **sudo apt-get install package-name** and then hitting **Enter**. For a list of available updates and package names, type **apt list –upgradable**

## [RPM](/docs/macloud-sdp/kb/how-do-i-solve-missing-os-patch-issues-on-opswat-client-linux#rpm)

For .rpm based Linux, open a **Terminal** and type **sudo yum update**

**To enable automatic updates functionality in Zypper on openSUSE, follow these steps:**

Pro Tip:

To learn more about installing updates in Linux, [Read This](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-linux-101-updating-your-system). To learn more about installing updates in Linux via the command line, [Read This](https://www.cyberciti.biz/faq/how-do-i-update-ubuntu-linux-softwares/).

Support:

If you have followed the instructions above but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint / MetaDefender IT Access** **Managed Linux Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
