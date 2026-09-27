<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/peripheral-media-protection/enable-system-extensions-and-full-disk-access-on-macos -->

# Enable System Extensions and Full Disk Access on macOS

### 1. What the Feature Does

**Peripheral Media Protection** helps protect your Mac from threats introduced through removable and peripheral media devices, such as USB drives and other connected storage devices.

To use Peripheral Media Protection feature on macOS devices to enable protection against peripheral media threats, users must allow the required system extension and grant Full Disk Access beforehand.

### 2. Why Do I Need to Grant These Permissions?

macOS protects system resources and user data by restricting applications from accessing certain system-level functions and protected files.

For the protection to work correctly, macOS requires you to approve the system components that provide device-level protection and grant the application the necessary access to files and system resources.

The required permissions allow MetaDefender Endpoint to:

| Permission | Why it is required |
| ---- | ---- |
| **System Extension** | Enables device-level monitoring and control of connected peripheral media. |
| **Full Disk Access** | Enables the application to access protected files and locations required for security scanning and protection. |

> **NOTE**
>
> System Extension approval and Full Disk Access are separate macOS permissions. Both must be enabled for the protection features to work as intended.

**If either permission is missing**, some protection capabilities may not work correctly as **all peripheral devices will be disconnected/dismounted from the endpoint**.

![](https://uploads.developerhub.io/prod/2x2P/v247znglsf1qn8u4pbdy2vztbg4p6r08ggqz9ei3a8vted5flnfudqjhc3vwxiof.png)

User will also receive a pop-up notification if these permissions are missing

![](https://uploads.developerhub.io/prod/2x2P/672m3xy0e40vnta51ulp07ol3mm2fd9l9kfc6wvakcv89yok6z84c5xzw6ehe4mh.png)

### 3. How to Enable the Required Permissions

Follow these steps to approve the system extension and grant Full Disk Access.

There are 2 ways users can navigate to the setting

**Through operating system**

1. Open **Apple menu > Settings**.
2. Select **General > Login items & Extensions**

**Through the on-screen popup / user interface of MetaDefender Endpoint**

1. Click **Open System Settings**.
2. Toggle the button to enable the **PmpEndpoint **extension

![](https://uploads.developerhub.io/prod/2x2P/ad6xu2zk0qj37cyeg6yuihhiadqnwl7km5mzzljqqlpc3kbv7f2mg4hf1i9tweq6.png)

![](https://uploads.developerhub.io/prod/2x2P/6g6lhu3d0554y97do588l27selicuy1qebi0gi9byt3qs27gf8z0bsjvyebc6bso.png)

**Step 3: Grant Full Disk Access**

1. Go to **System Settings > Privacy & Security**
2. Select **Full Disk Access**
3. Locate the OPSWAT application in the list
4. Turn on **PmpEndpointSecurity**
5. Authenticate if prompted

**Troubleshooting**

If the protection feature is still unavailable after granting both permissions:

- Verify that the **system extension is approved**
- Verify that **Full Disk Access** is enabled for the correct OPSWAT application
- Restart the Mac if the system extension was recently approved
- Contact your administrator if the required settings are managed by your organization's Mobile Device Management or security policy

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
