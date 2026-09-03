<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management- -->

# How can I delete a device from My OPSWAT Central Management?

> **Check Your Product:**
>
> This article applies to all OPSWAT Central Management version 10.x.

The My OPSWAT Central Management **Console** facilitates two methods of guest MetaDefender Endpoint device removal:

- **Manual** removal of one or multiple devices
- **Automatic** removal of an individual device or a group of devices.

## Option 1: Manual removal

> **Please Note:**
>
> For On-Demand MetaDefender Endpoint devices, please use Option 2, as Option 1 will only temporarily remove on-demand Client devices from the inventory.

1. Log into your **Console** and navigate to **Inventory > Devices > Endpoint.**
2. Select one or multiple devices from the device list by checking the selection boxes in the left-hand column, as illustrated below.
3. Once selected, expand the **Actions** drop-down menu in the upper right-hand corner of the device list, also illustrated below.

![](https://uploads.developerhub.io/prod/97qW/d7htjqtyp4mm64mjqz4zoyx8ueegfg4utw6p5esfi958s4xo7gk9xxi9rpjus7af.png)

4. From the drop-down menu, select the option to **Delete.**

![](https://uploads.developerhub.io/prod/97qW/ujgvnqgohz0eqxlqvbt5bgvuy8rme6bpa69k4s3beh9ynaxw9wfeqsy8sas2dsvk.png)

5. Enter your PIN, then confirm your selection by clicking **Delete** in the prompt, as shown below.

![](https://uploads.developerhub.io/prod/97qW/halszi44a333ear1i7jexhyh3t5sk4sw0skj4d82eb87o4vd5lya7nyi2qfrprmz.png)

**Pro Tip:**

|  |  |  |
| ---- | ---- | ---- |
| Persistent MetaDefender Endpoint | Windows, macOS and Linux | Option 1 will trigger a remote uninstall the next time the device/s check in with the My OPSWAT Central Management servers. |
|  | OS and Android | Option 1 will trigger a remote unregister action on the device/s, but the end-user/s will still need to uninstall/delete the OPSWAT app manually. |
| On-Demand MetaDefender Endpoint | All | Option 1 will not trigger any remote action and, if the Client is still running, it will reappear in the My OPSWAT Central Management Console after a few minutes. |

## Option 2: Automatic removal

> **Pro Tip:**
>
> Automatic device removal is enabled via the Console’s Lost Device settings, which can be adjusted either for individual devices or for groups of devices, as follows:
>
> - Individual devices: go to **Console>Settings>Global>Endpoint Data>Unresponsive Device** (see Screenshot A)
> - Groups of devices: go to **Console>Inventory>Groups>Relevant Group>Settings>Lost Device**(see Screenshot B)

**Screenshot A**

![](https://uploads.developerhub.io/prod/97qW/igkblo4jgbkmko0b69ve48oc4p1asogyeng3f63kps2b8yy7ne53fb7n70fn5lng.png)

**Screenshot B**

![](https://uploads.developerhub.io/prod/97qW/axe7rfjzlu8558pn1m7q9fh5k4o769misetwy3fkpns03u27cq3fl2qmening9h0.png)

1. Log into your **Console** and navigate to the relevant location detailed above.
2. Configure the options according to your preference.

Settings include:

- Automatically delete persistent devices unseen for *X* day/s consecutively
- Automatically delete on-demand devices unseen for *X* hour/s consecutively
- Automatically delete and uninstall the agent on devices if the devices have no access to cloud applications for *X* days consecutively (only available if Secure Access is enabled)
- Automatically delete unknown/ignored devices unseen for *X* days consecutively
- Automatically delete devices reporting as non-compliant for *X* days consecutively.

3. Finally, click **Save** to apply your settings.

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Deleting A Device Via Your** **Console**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
