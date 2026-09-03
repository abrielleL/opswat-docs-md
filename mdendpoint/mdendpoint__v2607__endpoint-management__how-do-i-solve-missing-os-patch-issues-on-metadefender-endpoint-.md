<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-do-i-solve-missing-os-patch-issues-on-metadefender-endpoint- -->

# How do I solve Missing OS Patch issues on MetaDefender Endpoint/MetaDefender IT-OT Access managed Linux devices?

> **Check Your Product:**
>
> This article applies to the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on Linux systems.

Users running MetaDefender Endpoint on one or more Linux devices may occasionally see MetaDefender IT-OT Access device compliance warnings/flags related to **Missing OS Patches**.

These warnings/flags are triggered by device issues and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Missing Patches**.

> **Pro Tips:**
>
> Malware is frequently designed to exploit the vulnerabilities in outdated applications and operating systems in order to gain entry to and infect a system.
>
> This is why keeping your operating system, OS security patches and all associated apps up-to-date is an essential element of risk reduction in cyber-security.

> **Pro Tips:**
>
> The following instructions are intended for *.deb* or *.rpm* based Linux systems, but steps may vary slightly depending on your distro and version.

To remediate Missing OS Patch related device compliance issues on your managed Linux devices, please follow the relevant instructions below.

## Debian

1. To synchronize your update package index with the latest available update index online, open a **Terminal** and type **sudo apt-get update**, then enter your admin password as prompted.

![](https://uploads.developerhub.io/prod/2x2P/gc616hp1c7ccbb16crgvdg1dxi9vb7o9ttpk2cclswmu8qfrmyo6f322a6apoe62.png)

2. Next, to install the latest versions of all packages currently installed on your system, type **sudo apt-get upgrade** then hit **Enter.**

![](https://uploads.developerhub.io/prod/2x2P/5mire344frso4bolkow776oh6lbri2k6t9n89ee71old9970rwxzyp0tugrzzl0l.png)

3. Alternatively, you can include the install of selected packages after the standard upgrades by typing **sudo apt-get install package-name** and then hitting **Enter**. For a list of available updates and package names, type **apt list –upgradable**

![](https://uploads.developerhub.io/prod/2x2P/254ls9wc280oxbakqix9p4ojcruvk7lh107sqfju2zjdj3bk489p98zmc0o7y0c5.png)

## RPM

For .rpm based Linux, open a **Terminal** and type **sudo yum update.**

![](https://uploads.developerhub.io/prod/2x2P/xzieolzfiox7xzvj14rnswq1qrly9ji0jdxski4zuew02mhfbmqxaxwwpse826qg.png)

> **Pro Tips:**
>
> To learn more about installing updates in Linux, [Read This](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-linux-101-updating-your-system). To learn more about installing updates in Linux via the command line, [Read This](https://www.cyberciti.biz/faq/how-do-i-update-ubuntu-linux-softwares/).

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint / MetaDefender IT-OT Access** **Managed Linux Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
