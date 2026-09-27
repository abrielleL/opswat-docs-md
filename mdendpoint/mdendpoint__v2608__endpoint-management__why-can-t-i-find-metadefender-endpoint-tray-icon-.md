<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/why-can-t-i-find-metadefender-endpoint-tray-icon- -->

# Why can't I find MetaDefender Endpoint tray icon?

> **Info**
>
> This article applies to all MetaDefender Endpoint releases, released after 9/10/16, deployed on Windows systems.

## Persistent MetaDefender Endpoint

Starting on 9 October, 2016, the Persistent MetaDefender Endpoint tray icon will not be pinned to the tray by default following installation.

Persistent MetaDefender Endpoint users who wish to pin the Client icon to the tray should enable this feature manually, by following one of the methods outlined below.

### **Option 1**

1. Open the **Start** menu.
2. Search for **MetaDefender Endpoint** or **MetaDefender IT-OT Access**, depending on which MetaDefender Endpoint version you run.
3. Click on **MetaDefender Endpoint** or **MetaDefender IT-OT Access** to start displaying the tray icon for this session.

### **Option 2**

1. Open File Explorer and type **%PROGRAMFILES(X86)%** into the path bar, then add **\OPSWAT** to the path to access the MetaDefender Endpoint installation directory.
2. Inside the directory, find and open the **Gears** folder.
3. Double click on **Gears.exe** to activate the tray icon.

> **Warning**
>
> If the MetaDefender Endpoint does not appear on your **Start** menu, it’s possible that your administrator has disabled the MetaDefender Endpoint tray icon on endpoints. You can confirm whether this is the case by trying **Option 2** above. If you see an error message stating that **Your administrator has disabled the** **MetaDefender Endpoint** **UI**, it means that either your administrator has disabled the client tray icon on endpoints, or your account does not include a token for this device. If this is the case, please contact your administrator for further details.

## On-Demand MetaDefender Endpoint

The On-Demand MetaDefender Endpoint always shows the tray icon, regardless of your account settings on the cloud.

> **Pro Tip:**
>
> If you do not see the tray icon when running the On-Demand MetaDefender Endpoint, it means that your account does not include a token for this device.
>
> In such cases, please contact your administrator for further details.

> **Support:**
>
> If You have followed the instructions above and still **Cannot Enable The** **MetaDefender Endpoint** **Tray Icon, And Are Sure That This Is Not Due To Administrator Settings Or Lack Of A Token For Your Device**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
