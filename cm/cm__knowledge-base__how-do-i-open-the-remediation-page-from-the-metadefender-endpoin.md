<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-open-the-remediation-page-from-the-metadefender-endpoin -->

# How do I open the remediation page from the MetaDefender Endpoint on Arch Linux?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Arch Linux systems.If you want to open the remediation page from MetaDefender Endpoint, you need to run command line as: ***opswat-client -r***

> **Pro Tip:**
>
> The MetaDefender Endpoint device issue **Remediation Page** is usually accessible via the **My OPSWAT Central Management Console>Inventory>Devices** tab, under the *device details* view for each device, as illustrated in the screenshots below.

![](https://uploads.developerhub.io/prod/1yda/jrrjqk7ibs3ewgvenmegk3uyjjlbmwr4ypui4g6ke3ph61lfgo0sy695vopdqea4.png)

![](https://uploads.developerhub.io/prod/1yda/5n7erngewlvn9yjxahnag0ar3y4n4idxok7vj2rqkswsurf7bgwklrt4dbso3nc9.png)

To open the MetaDefender Endpoint remediation page via the Arch Linux distribution, the Linux system will need to have **xdg-utils** installed, so that MetaDefender Endpoint can open a compatible browser.

To do this, please follow the instructions below.

1. Download the **xdg-utils** package via [This Link](https://www.freedesktop.org/wiki/Software/xdg-utils/).
2. Install the package by running the command: **pacman -S xdg-utils**

The MetaDefender Endpoint should now open the remediation page without issue.

> **Support:**
>
> If you have followed the instructions above but are still **Unable To Open The Device Issue Remediation Page Via Your Arch Linux System**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
