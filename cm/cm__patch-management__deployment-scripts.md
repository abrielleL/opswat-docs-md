<!-- source: https://www.opswat.com/docs/cm/patch-management/deployment-scripts -->

# Deployment Scripts

**Deployment Scripts** let you run your own PowerShell script on each device right before and right after a patch is installed. Use them to stop a service, back up data, or verify that an application is running again after the update.

Note Deployment scripts are available for On-Demand deployments for Windows Patches and Application Patches, on Windows devices only. Refer to [On-Demand Deployment](https://www.opswat.com/docs/cm/patch-management/on-demand-deployment) for detailed instructions.

- [Add Scripts to a Deployment](https://www.opswat.com/docs/cm/patch-management/deployment-scripts#add-scripts-to-a-deployment)
  - [Configure Scripts](https://www.opswat.com/docs/cm/patch-management/deployment-scripts#configure-scripts)
- [Write a Script](https://www.opswat.com/docs/cm/patch-management/deployment-scripts#write-a-script)
  - [Sample Scripts](https://www.opswat.com/docs/cm/patch-management/deployment-scripts#sample-scripts)
- [Monitor Script Results](https://www.opswat.com/docs/cm/patch-management/deployment-scripts#monitor-script-results)
- [What Happens When a Script Fails](https://www.opswat.com/docs/cm/patch-management/deployment-scripts#what-happens-when-a-script-fails)

## How It Works

The deployment executes sequentially in three phases: **Pre-script runs** ➔ **Patches install** ➔ **Post-script runs**

1. Pre-script runs on the device before any patch is installed. If the script fails and the job is configured to abort on failure, patch installation is skipped on that device.
2. Patches are installed on target devices.
3. Post-script runs after the patches finish. You can configure it to run immediately, or delay execution until the device reboots or the application relaunches.

> **Execution & Reporting Notes**
>
> - **One-time execution:** Each script runs **once per device** per deployment. Scripts are not retried, even if patch installation is retried.
> - **Status tracking**: Execution results are reported per device under the **Scripts tab **and summarized in the completion notification email.

Note  Each script runs **once** per device per deployment. Scripts are not retried, even though patches are.

## Add Scripts to a Deployment

![](https://uploads.developerhub.io/prod/97qW/o3zwq8da6gpt54s87dzb894pqaxsv5rizm58tu1lv7p18922inq5g1knidayjdg5.png)

1. In the left navigation, select **Patch Management > Jobs**
2. Select **Create On-Demand Deployment** and choose **Windows Patches** or **Application Patches**
3. Scroll to the **Automation Scripts** section. You can enable the pre-script, the post-script, or both

### Configure Scripts

| Configuration | Details |
| ---- | ---- |
| Enable the **Pre-script** ![](https://uploads.developerhub.io/prod/97qW/ze6qiz3r478dc11hatsfccvbx3cutd9se4sxewl4izeghx7r98yvr05w2ajrts4c.png) | - Select **Run the following script before update as** - Pick who the script runs as: **System**, **Administrator**, or **Current User** - See [Choose Who the Script Runs As](https://www.opswat.com/docs/cm/patch-management/deployment-scripts#choose-who-the-script-runs-as) for more details |
| Enable the** Post-script** ![](https://uploads.developerhub.io/prod/97qW/0q1gq134ufauvoco9a2q9v28fpxy5o4jjrf9o1y3r5yyttx1kz2r9x4kx5ex3v54.png) | Select **Run the following script after update as** and pick who the script runs as |
| Upload the script ![](https://uploads.developerhub.io/prod/97qW/4jt5gp6rzy0hd5urm2ogce862avs922s8d76czozjmq8cfbqi301fsu6l9dzvu6i.png) | Select **Choose File** and upload a .ps1 file or a .zip archive (max 3 MB) Once uploaded, the **File name**, **Last update**, and **Hash file [MD5]** are shown so you can confirm the right version is attached |
| Stop patching if the pre-script fails ![](https://uploads.developerhub.io/prod/97qW/7hzdniwuz0pylnv648iz984n4y4wxlhb35q7fb55yrez5ukii1o5xk4zr6e7w6eq.png) | Select **Abort the deployment on device(s) if the pre-script fails** Devices whose pre-script fails will not install any patch. Leave it unchecked (default) to record the failure and continue patching |
| Run the post-script in the final state ![](https://uploads.developerhub.io/prod/97qW/120thzfo1upry8srv3zhwnxbauhtqn7xh6u0kyjj8w151t60z5u9ysk2m0kmszp8.png) Note With **Run after the device reboots** enabled, the deployment stays open until the device actually restarts. With **Run after the application relaunches**, if the app is not relaunched before the deployment ends, the post-script is reported as Not executed. | Check **Run the post-script after the device reboots** (Windows Patches) or **Run the post-script after the application relaunches** (Application Patches) The post-script waits until the device has restarted or the app is running again. If no reboot is pending, it runs right away |

### Choose Who the Script Runs As

| Option | Use when |
| ---- | ---- |
| **System** (default) | The script needs full access to the machine, such as stopping services or writing to protected folders |
| **Administrator** | The script needs elevated rights in an administrator context |
| **Current User** | The script works with the signed-in user's files or settings, or shows a prompt. Nothing runs if no user is signed in |

## Write a Script

A script is a PowerShell file or a zip archive with main.ps1 at its root. Use a zip when the script needs helper files such as modules or configuration.

The script tells My OPSWAT Central Management how it went by printing an [output] block. The exit code is not used.

```plaintext
[output]
result = 1
msg = Stopped LOBApp and LOBSync successfully

```

- result must be 1 (success) or 0 (failure).
- msg is shown in the **Message** column of the Scripts tab. Make it useful, it is the first thing you will read when a script fails.

| Rule | Details |
| ---- | ---- |
| File type | .ps1 or .zip. A .zip must contain main.ps1 at its root and at most 1,000 files. |
| Size | Up to 3 MB. Empty files are rejected. |
| Time limit | 10 minutes. A script that runs longer is stopped and reported as **Timeout**. |
| Input | Scripts run non-interactively. A script that waits for input will fail. |

Tip Make scripts safe to run more than once, keep them short, and test them on a few devices before targeting the whole fleet.

### Sample Scripts

Use these samples as a starting point. Each one prints the [output] block described above.

| Purpose | Windows |
| ---- | ---- |
| Stop a service before the update | [Win-CheckExistingRegistryKeyScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckExistingRegistryKeyScript.ps1) |
| Start a service after the update | [Win-CheckRegistryKeyValueScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckRegistryKeyValueScript.ps1) |
| Check whether a specific process is running | [Win-CheckRunningProcessScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckRunningProcessScript.ps1) |
| Check whether a specific file exists on a specific path | [Win-CheckExistingFileScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckExistingFileScript.ps1) |
| Check whether a specific registry key exists | [Win-CheckExistingFileScript.ps1](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-CheckExistingFileScript.ps1) |
| Multiple script check (zip with main.ps1 and helper files) | [Win-multi-script.zip](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/CustomCheckSampleScripts/Windows/Win-multi-script.zip) |

## Monitor Script Results

1. In the left navigation, select **Patch Management > Jobs**
2. Open the deployment and select the **Scripts** tab. The tab appears only when the deployment has at least one script

![](https://uploads.developerhub.io/prod/97qW/78hr09l0ysbs59um3fikqj0rgfpm4khp0505o97veayyx10pqoslo4qdxjpkkwnv.png)

Each script has its own block showing:

1. **File name**, **Run as**, **Hash file [MD5]**, and any option you enabled
2. **Success / Failed / Not executed** counts across the devices shown
3. **Download** to get the exact script this deployment is running
4. A per-device table with **Status**, **Device Name**, **Reported At**, and **Message**. Use **Search by device name** to find one device, and click a row to open the device

![](https://uploads.developerhub.io/prod/97qW/oef0jjdape17ftm4pk1rz5sq43i97849qqryqaynhbfzp125jy4p5ocsd3axow0p.png)

### Script Statuses

The **Status** column shows how the script ended on each device. Hover over a status to see its raw result code. Codes 1 and 0 come from the script's own [output] block; negative codes are reported by the device when the script could not produce a result.

| Status | Result code | Meaning |
| ---- | ---- | ---- |
| **Success** | 1 | The script ran and reported result = 1 |
| **Failed** | 0 | The script ran and reported result = 0 |
| **Timeout** | -1 | The script ran past its time limit and was stopped |
| **Wrong format** | -2 | The script did not print an [output] block |
| **Invalid output** | -3 | The [output] block was malformed, for example a result other than 0 or 1 |
| **Could not run** | -4 | The device could not download, verify, unpack, or start the script |
| **Not executed** | -5 | The script was skipped, either because the pre-script aborted the deployment on that device, or because the awaited application relaunch never happened |

### Summary Counts

The three counters at the top of each script block group the per-device statuses into three buckets.

![](https://uploads.developerhub.io/prod/97qW/2e5uvzdawiwulwsj11lpn5g15wdrfp9d51c11d3uk31tk1ct3n0s1cr91hv8n8dl.png)

| Counter | Counts devices with status |
| ---- | ---- |
| **Success** | Success |
| **Failed** | Failed, Timeout, Wrong format, Invalid output, Could not run |
| **Not executed** | Not executed |

In other words, a device counts as **Failed** whenever the script did not finish with a success result, whether the script itself reported a failure or the device could not run it at all. **Not executed** is kept separate because the script was deliberately skipped, not broken.

Note The counters reflect the devices currently listed in the table below them, so they follow the page size and the device-name search. The completion email uses the same three buckets but counts every device in the deployment.

### Scripts Results in Completion Email

| Details |  | Completion Email |
| ---- | ---- | ---- |
| When a deployment with scripts finishes: -  The summary email includes an **Automation scripts** section with, for each script, the file name, who it ran as, the **Succeeded / Failed / Not executed** counts across all devices - Click View Details to navigate to the **Scripts** tab. Individual devices are not listed in the email. |  | ![](https://uploads.developerhub.io/prod/97qW/bhbwbomf8ol8moe2k83c4omqm2szmfo01ri4jo1avg2r9785ym5560l4w6tnbhm7.png) |

## What Happens When a Script Fails

| Script | Result |
| ---- | ---- |
| **Pre-script fails**, abort **unchecked** | The failure is recorded. Patches install and the post-script runs as normal |
| **Pre-script fails**, abort **checked** | That device installs nothing. Its patches are reported as failed with the reason *Deployment aborted because the pre-deployment script failed*, and the post-script is **Not executed**. Other devices continue normally |
| **Post-script fails** | Installed patches stay installed and their results are unchanged. The failure is shown in the deployment detail for visibility |

## Next Steps

- Track the rest of the deployment in [Monitor Deployment](https://www.opswat.com/docs/cm/patch-management/monitor-deployment)
- Set real-time alerts for key patch events under [Patch Notification](https://www.opswat.com/docs/cm/patch-management/patch-notification)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
