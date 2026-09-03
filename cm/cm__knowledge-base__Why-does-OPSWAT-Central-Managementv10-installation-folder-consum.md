<!-- source: https://www.opswat.com/docs/cm/knowledge-base/Why-does-OPSWAT-Central-Managementv10-installation-folder-consum -->

# Why does OPSWAT Central Management v10 installation folder consume a lot of disk space?

> **Check Your Version:**
>
> This article applies to all OPSWAT Central Management version 10.x.

## Issue

After a fresh installation of **OPSWAT Central Management (OCM) v10**, you may notice that the installation directory gradually increases in size.

## Possible Causes

1. **Engine updates**

If OCM10 is configured to download update modules from the internet, it periodically downloads engine update packages from OPSWAT’s update servers and stores them locally. When new engine updates are retrieved, the previous update files in the `fusion-updater` folder are retained for up to **5 days** before they are automatically deleted. As a result, the folder size may continue to grow during the initial days after installation. This behavior is expected.

Additionally, the total storage required depends on the number of **engines** included in your Core configuration — more engines will require more update packages and therefore more disk space. You can find more details about the storage requirement for OCM10 at [System Requirements - My OPSWAT Central Management](https://www.opswat.com/docs/cm/deployment/system-requirements#storage-usage-information)

2. **Log Growth**

By default, OPSWAT Central Managements logs are stored in the following directory:

`C:\ProgramData\OPSWAT\MOCM\Logs`

As OCM continues to operate, the accumulation of log files can cause gradual growth in storage usage.

3. **MetaDender Core’s reports**

MetaDefender Core’s reports are stored at the OCM10 installation folder (i.e C:\Program Files\OPSWAT\MOCM by default).

If MetaDefender Core scans a large number of files over time, these reports may increase the total size of the OCM installation folder.

## Solutions

1. **Engine update**

Monitor the `fusion-updater` folder for several days to confirm that the automatic cleanup process is functioning as expected. Folder size should stabilize once the update retention cycle completes.

2. **Log Growth**

Reduce disk usage from logs by adjusting the Trace log settings at **OCM10 Management Console** > **Settings** > **Servers** > **Trace Log.** Delete log files older than 14 days.

![](https://uploads.developerhub.io/prod/97qW/60ydryrynlzf7b5fvwizgkefgdrpiu9c8p0eh6ozxv108wj4udx430g31e91prpv.png)

You can also manually delete older log files if necessary.

3. **MetaDender Core’s reports**

If MetaDefender Core reports are consuming excessive space, you can consider decreasing the Data Retention length in OCM10 Global Settings.

In the Advanced settings, we also recommend enabling the option “Do not store detailed report data for allowed files” when it is not required. Detailed report data for allowed files typically does not contain any threat detection information and can consume significant disk space, as the majority of processed files are usually allowed files.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
