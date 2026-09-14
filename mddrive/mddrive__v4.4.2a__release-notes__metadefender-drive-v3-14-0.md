<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/release-notes/metadefender-drive-v3-14-0 -->

# MetaDefender Drive v3.14.0

| [MetaDefender Drive v3.14.0](/docs/mddrive/v4.4.2a/release-notes/metadefender-drive-v3-14-0#metadefender-drive-v3140) Released on Jun 30, 2022 | This is a major release that adds new feature as well as improvement and stability |
| --- | --- |
| **New features** |  |
| QuickScan | When time is sensitive, you can quickly select a preconfigured end-to-end analyst on the most critical Windows directories with the most trusted AV engine. We are focusing Windows first, and the most important directories in a Windows system are:   - Users data & documents - Installed Programs - System Directories |
| Allow transferring to multiple USB after scanning | Drive now can transfer user's clean data to more than one external USB storages within a scan session |
| Apply MetaDefender Vault Guest workflow for post-scan | In MetaDefender Vault, a "guest" is a temporary account which has limited access and life time. By using guest wofklow, we can secure the data being transfered through airgap. |
| Modify engine update priority: Local storage → intranet → internet | We are prioritizing the engine installation basing on geological order.   - If there are updates available in Drive's storage, they will be installed and initialized first, automatically - If there are no local updates available, user will be notified and will need to click "Online Update" to get update from an OCM (if there is one connected) or from the internet (if the connected OCM is not serving update services) |
| **Improvements** |  |
|  |  |
| **Known Issues** |  |
| Scanning uncompleted in some special situations |  |
