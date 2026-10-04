<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-do-a-custom-check-on-endpoints- -->

# How can I do a custom check on endpoints?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases subsequent to:
>
> - For custom script checks (detailed below):
>   - **V7.6.136.0 (Windows Client)**
>   - **V10.4.162.0 (macOS Client)**
>   - **V15.6.19.0 (Redhat-based Linux Client)**
>   - **V15.4.22.0 (Debian-based LinuxClient)**
> - For multiple script checks (detailed below):
>   - **V7.6.366 (Windows Client)**
>   - **V10.4.300.0 (macOS Client)**
>   - **V15.6.2209.85 (Redhat-based LinuxClient)** (only supported via playbook)
>   - **V15.4.2209.89 (Debian-based Linux Client)** (only supported via playbook)

> **Please Note:**
>
> As of 9 January 2018 (for Windows and macOS systems) and 22 December 2020 (for Linux systems), My OPSWAT Central Management offers administrators the option to perform custom remote checks of managed endpoints.
>
> This includes checks that are not offered in OPSWAT’s granular policy, such as whether a specific registry key or file exists, or whether a specific process is running on an endpoint device.

## How it works

Administrators have the option to write a custom script (to perform a specialized check on an endpoint device) and then apply it to a **Policy** via their My OPSWAT Central Management **Console**.

Once a custom check is enabled via policy, My OPSWAT Central Management will push the script to all endpoints associated with that policy.

My OPSWAT Central Management will then invoke the script on those endpoints at the pre-configured (admin-defined) privilege level and frequency.

## How to enable it

1. Log into your **Console** and navigate to **Policy Management>Policies>Relevant Policy>Laptops/Desktops>Deep Compliance**.
2. Toggle the **Custom Check** switch to its enabled state, as illustrated in the screenshot below.
3. Select the operating system (for which you’d like to run a custom check) by clicking the appropriate tab, also illustrated below.

![](https://uploads.developerhub.io/prod/97qW/rfxp3xfid5botfaxdxjn1bev3nzo8w8zbryt9ayymot73yibvmkkwvtcvariwwh4.png)

4. Next, check the box for **Script returns**, then select the **False** option from the drop-down menu.
5. Check the **Run the powershell/shell script as** selection box and then, from the drop-down menu, select the privilege level at which MetaDefender Endpoint should run the script, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/o7etj22et0gw384vkcdaqbex65y3dgk46upv5knvqpp51iraisheug9mvn6d1m0g.png)

> **Please Note:**
>
> - **Persistent MetaDefender Endpoint:** supported versions prior to V7.6.324/10.4.284 (or all supported versions for Linux) will run the script with system/root privilege.
> - **On-Demand MetaDefender Endpoint:** supported versions prior to 7.3.503.0/10.5.213.0 (or all supported versions for Linux) will run the script with current user privilege.

6. Finally, to apply your settings, click **Save**, then enter your **PIN** as prompted.

Next, you must configure the frequency with which you would like the OPSWAT Client to run the script.

To do so, please follow the instructions below.

7. In your **Console**, navigate to **Settings>Global>Device Agents>Compliance Report.**
8. Adjust the number in the **Agents will run script every** ***X*** **minutes** option, as illustrated below.
9. Finally, click **Save** to apply your settings, also illustrated below.

![](https://uploads.developerhub.io/prod/97qW/9lzu3fjcmvh1v8kdu7kxp8vir6on3robzc8po946dbtry7psg9icblot0bp9vwi8.png)

> **Pro Tip:**
>
> Whenever an endpoint Client executes the script, it will report the script result to the cloud, along with the compliance check report.
>
> Should the script fail to run, or should it time out, the cloud will register the device custom check as PASSED. Administrators can then view the script result via **Console>Inventory>Devices>Relevant Device>Device Details View>Custom Check**, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/o0zqrw1tx1r0j7dwp3kp9i7nv4yotntc6kvq62p7dkdt1dysjwakj4rpozkc92se.png)

> **Pro Tip:**
>
> Administrators can also filter the device list to display only the devices that the script returns as FALSE, by following the instructions below:
>
> 1. Go to your **Console>Inventory>Devices.**
> 2. Use the checkboxes to select the appropriate devices, then click the **Filters** button in the top right-hand corner of the device list (see Screenshot A).
> 3. In the pop-up menu, expand the **Other Categories** section, then check the **Custom Check** selection box (see Screenshot B).
>
> Scroll down to the bottom of the pop-up menu, then click **Update** to apply your filters (see Screenshot C).

**Screenshot A**

![](https://uploads.developerhub.io/prod/97qW/zbzsy2cb0pgt35k2bqwan0fbzl2kbepxjftur1lnilpw7q3zyx8rvw3ixf3g5t8i.png)

**Screenshot B**

![](https://uploads.developerhub.io/prod/97qW/u0ls539idfqmq18rlpapvcl57dmzeda0b0fuerk3osddy1lg8ezz8128vl3kc6dg.png)

**Screenshot C**

![](https://uploads.developerhub.io/prod/97qW/54wzny1wepjr07zcgp9334r32xv4twinyfc4l5pf66kmua58em9ekw7z1l425lvg.png)

## Permission requirements

My OPSWAT Central Management supports the running of custom scripts at the following privilege levels for Windows and macOS:

| **Run as** | **Windows** | **macOS** | **Linux** |
| ---- | ---- | ---- | ---- |
| System | SUPPORTED | SUPPORTED | SUPPORTED (Root) |
| Administrator | SUPPORTED | NOT SUPPORTED | NOT SUPPORTED |
| Current User | SUPPORTED | SUPPORTED | SUPPORTED |

> **Please Note:**
>
> The above privilege settings only apply to the Persistent MetaDefender Endpoint.
>
> The On-Demand MetaDefender Endpoint runs the custom script at the current on-demand process’s permission level, so:
>
> - If you run the **On-Demand MetaDefender Endpoint** (which requires administrator privilege), the script will be run at administrator level privilege.
> - If you run the **limited** **On-Demand MetaDefender Endpoint** (which does not require elevated privilege), the script will be run at current user level privilege.

## Script requirements and support

1. MetaDefender Endpoint supports the following script formats:

- **Powershell** for Windows
- **Shell** for macOS and Linux.

> **Please Note:**
>
> MetaDefender Endpoint does not support administrator inputs while executing a script.

2. Script files must have the following extensions:

- ***.ps1***  for Windows
- ***.sh*** for macOS and Linux .

3. Multi-script files must be packaged in a ***.zip*** file, with the main ***.ps1***/***.sh*** file located in the root folder, while sub-scripts can be located in either root folders or subfolders.

> **Please Note:**
>
> For Linux devices, multi-script is only supported via **Playbook**, not via standard **Custom Check** settings. For more information on running custom checks via playbook, please refer to [Playbooks](https://www.opswat.com/docs/cm/endpoint-security-solution/playbooks) guidelines.

4. Scripts must return an output with the following format:

> **Info**
>
> `[output]`
>
> `result = 0`
>
> `msg = this is a script log`
>
> - *Where* ***result*** *only accepts 0/1 (meaning False/True).*
> - *Where* ***msg*** *is limited to 2048 bytes.*

![](https://uploads.developerhub.io/prod/97qW/ttlv9ryphp2yucpl8znj3mkgjlyc751w8ihcvbpyeh7g9lrfxc3ejilqbjn3is9v.png)

![](https://uploads.developerhub.io/prod/97qW/ax0swjdkpnh051snlsa00xg9tdvyaez4sut0o9clabhf455x40vfv0t3msckko67.png)

> **Please Note:**
>
> If the script returns with the wrong format, or an invalid value for the **result** or **msg** parameter, the MetaDefender Endpoint will treat it as **Failed to execute**, and the **My OPSWAT Central Management** will then register the device check status as **Passed**.

## Sample scripts

|  | Windows | macOS |
| ---- | ---- | ---- |
| Whether a specific registry key exists | [Win-CheckExistingRegistryKeyScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckExistingRegistryKeyScript.ps1) |  |
| Whether a specific registry key value contains certain regex string | [Win-CheckRegistryKeyValueScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckRegistryKeyValueScript.ps1) |  |
| Whether a specific process is running on the system | [Win-CheckRunningProcessScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckRunningProcessScript.ps1) | [MacOS-CheckRunningProcessScript.sh](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/MacOS/MacOS-CheckRunningProcessScript.sh) |
| Whether a specific service is running on the system | [Win-CheckRunningServiceScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckRunningServiceScript.ps1) | [MacOS-CheckRunningServiceScript.sh](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/MacOS/MacOS-CheckRunningServiceScript.sh) |
| Whether a specific file exists on a specific path in the system | [Win-CheckExistingFileScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckExistingFileScript.ps1) | [MacOS-CheckExistingFileScript.sh](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/MacOS/MacOS-CheckExistingFileScript.sh) |
| Multiple script check* | [Win-multi-script.zip](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-multi-script.zip) | [MacOS-multi-script.zip](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/MacOS/MacOS-multi-script.zip) |

> **Please Note:**
>
> Custom scripts are only available for MetaDefender Endpoint releases subsequent to:
>
> - For custom scripts checks:
>   - **V7.6.136.0 (Windows Client)**
>   - **V10.4.162.0 (macOS Client)**
>   - **V15.6.19.0 (Redhat-based Linux)**
>   - **V15.4.22.0 (Debian-based Linux)**
> - For multiple script checks*:
>   - **V7.6.366 (Windows Client)**
>   - **V10.4.300.0 (macOS Client)**
>   - **V15.6.2209.85 (Redhat-based Linux)** (only supported via playbook)
>   - **V15.4.2209.89 (Debian-based Linux)** (only supported via playbook)
>
> For more information on playbook-facilitated custom and multi-script checks for Linux systems, please refer to [Playbooks](https://www.opswat.com/docs/cm/endpoint-security-solution/playbooks)[** guidelines.**](https://www.opswat.com/docs/cm/endpoint-security-solution/playbooks)

> **Support:**
>
> If you have followed the instructions above, but are having difficulty **Running A Custom Check or Multi-Script Check**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
