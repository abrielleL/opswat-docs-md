<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-can-i-delete-a-device-from-my-metaaccess-console- -->

# How can I delete a device from my MetaDefender IT Access console?

This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

The **MetaDefender IT Access** **Console** facilitates two methods of guest MetaDefender Endpoint device removal:

- **Manual** removal of one or multiple devices
- **Automatic** removal of an individual device or a group of devices.

## [Option 1: Manual removal](/docs/macloud-sdp/kb/how-can-i-delete-a-device-from-my-metaaccess-console-#option-1-manual-removal)

Please Note:

For On-Demand MetaDefender Endpoint devices, please use Option 2, as Option 1 will only temporarily remove on-demand Client devices from the inventory.

1. Log into your **MetaDefender IT Access Console** and navigate to **Inventory>Devices**.
2. Select one or multiple devices from the device list by checking the selection boxes in the left-hand column, as illustrated below.
3. Once selected, expand the **Actions** drop-down menu in the upper right-hand corner of the device list, also illustrated below.

4. From the drop-down menu, select the option to **Delete**, then confirm your choice by clicking **Delete** in the prompt, as illustrated below.

Pro Tip:

|  |  |  |
| --- | --- | --- |
| Persistent MetaDefender Endpoint | Windows, macOS and Linux | Option 1 will trigger a remote uninstall the next time the device/s check in with the MetaDefender IT Access servers. |
|  | OS and Android | Option 1 will trigger a remote unregister action on the device/s, but the end-user/s will still need to uninstall/delete the OPSWAT app manually. |
| On-Demand MetaDefender Endpoint | All | Option 1 will not trigger any remote action and, if the Client is still running, it will reappear in the MetaDefender IT Access Console after a few minutes. |

## [Option 2: Automatic removal](/docs/macloud-sdp/kb/how-can-i-delete-a-device-from-my-metaaccess-console-#option-2-automatic-removal)

Pro Tip:

Automatic device removal is enabled via the MetaDefender IT Access Console’s Lost Device settings, which can be adjusted either for individual devices or for groups of devices, as follows:

- Individual devices: go to **MetaDefender IT Access Console>Settings>Global>Device Data>Lost Device** (see Screenshot A)

Groups of devices: go to **MetaDefender IT Access** **Console>Inventory>Device Groups>Relevant Group>Settings>Lost Device** (see Screenshot B)

**Screenshot A**

**Screenshot B**

1. Log into your **MetaDefender IT Access Console** and navigate to the relevant location detailed above.
2. Configure the options according to your preference.

Settings include:

- Automatically delete persistent devices unseen for *X* day/s consecutively
- Automatically delete on-demand devices unseen for *X* hour/s consecutively
- Automatically delete and uninstall the agent on devices if the devices have no access to cloud applications for *X* days consecutively (only available if Secure Access is enabled)
- Automatically delete unknown/ignored devices unseen for *X* days consecutively
- Automatically delete devices reporting as non-compliant for *X* days consecutively.

3. Finally, click **Save** to apply your settings.

Support:

If you have followed the instructions above but are having difficulty **Deleting A Device Via Your** **MetaDefender IT Access** **Console**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
