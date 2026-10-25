<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/release-notes/metadefender-drive-v3-9-2 -->

# MetaDefender Drive v3.9.2

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| **MetaDefender Drive v3.9.2** Released on Jul 09, 2021 | This is a major release that adds new feature as well as improvement and stability |
| --- | --- |
| **New features** |  |
| Drive Light Mode | From this release, when booting from systems that have only 4GB of memory or less, the user will be suggested two running modes:   - Light Mode:    - selecting this, the system will be running with only one AV engine   - BitDefender is recommended and pre-selected but the user is able to choose another AV engine at their wish   - all of the previous settings and integration (OPSWAT Central Management and MetaDefender Vault) are preserved and unchangeable - Normal Mode:    - choosing this mode, Drive will continue booting into normal working mode   - user should be aware of slow performance or even crash due to the lacking of resource |
| MetaDefender Vault Integration | MetaDefender Vault is one of the best ways to store and transfer valuable data crossing a critical infrastructure with safety. The integration between MetaDefender Drive and MetaDefender Vault in Drive 3.9.0 is to bring those benefits to your organization. |
| Preserve user settings during upgrade | Settings are saved when installing new version of Drive |
| Custom report naming | Reports now can be given with human memorable names |
| **Improvements** |  |
| Better User Experience | - Navigation bar has been made more intuitive - Device tab is updated with more information about the scan sessions - Allows restoring default settings - Notifcation messages have been generally improved - Eventlog is now updated more smoothly |
| Support nVIDIA Quadro Graphics | We keep extending our range of compatible hardware |
| Notice for Intel RST | On a laptop that has this technology integrated and enabled, some BIOS modification is required in order to help boot media to work. Drive will detect such cases and show an on-screen guidance. |
| Improved Performance and Power/Heat Management | Scan engines and utilities are optimized to reduce resource consumption while still increase throughput 15% |
| **Bugs fixed** |  |
| Better Japanese Translation | Previous editions had a less accurate Japanese translation. This has been corrected. |
| Some internal bugs fixed | Some bugs were fixed for files transferring and mounting destination disks |
