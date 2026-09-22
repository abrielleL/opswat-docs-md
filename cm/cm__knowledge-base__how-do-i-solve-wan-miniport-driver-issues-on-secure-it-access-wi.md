<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-wan-miniport-driver-issues-on-secure-it-access-wi -->

# How do I solve WAN Miniport Driver issues on Secure IT Access Windows device?

> **Check your product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows 10 or 11 systems.

> **Info:**
>
> If you encounter a Secure IT Access connectivity issue accompanied by the error message below, this troubleshooting guide is designed to assist you in resolving the problem as much as possible.
>
> *1. Unable to complete the connection setup on your machine. Please try again or follow the* ***Troubleshooting Guide*** *to solve your issues. If the problem persists, contact the OPSWAT Support.*

Users running MetaDefender Endpoint on Windows may occasionally see that **Secure IT Access** cannot connect successfully due to **WAN Miniport driver** issues.

**WAN Miniport drivers** are responsible for many functionalities, including wireless and alternative connections. However, **WAN Miniport driver** issues can block or disturb your Secure IT Access connectivity.

To remediate WAN Miniport issues on your Windows devices, please follow the relevant instructions below.

1. Open **Windows Device Manager**
2. Navigate to **Network adapters**
3. Uninstall all of the **WAN Miniport (XXXX)** devices

![](https://uploads.developerhub.io/prod/1yda/uu2vvbr2w6pdtsgio406slu2lenaoxmu5y9e2kz8ekqkxji9c3k0ii1f6ulpud66.png)

4. Right-click on any item and choose **Scan for hardware change.**

![](https://uploads.developerhub.io/prod/1yda/3bn1fb75vo7dxt59czxwadguzrglmlb37ag4ezjwnt96rgatzwxn28mggj3e43d6.png)

5. The WAN Miniport adapters should have re-installed themselves.
6. Try to connect Secure IT Access again.

> **Please note:**
>
> Make sure all **WAN Miniport drivers** are enabled.

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience WAN Miniport driver issues**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
