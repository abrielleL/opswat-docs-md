<!-- source: https://www.opswat.com/docs/mddrive/v4.4.8/release-notes/metadefender-drive-v3-10-0 -->

# MetaDefender Drive v3.10.0

| **MetaDefender Drive v3.10.0** Released on Sep 06, 2021 | This is a major release that adds new feature as well as improvement and stability |
| --- | --- |
| **New features** |  |
| Processing Workflows | Processing Workflows that will save your time and efforts from repeatedly selecting the same paths and modifying the same settings for every scan.  Instead, you will simply choose to create a workflow and save it at will after they finish a scan. On the next boots, from the same target system, you will be able to select and rerun a workflows from a list that have been created for that particular system.  Also, the Workflows dashboard will present a quick and critical view about the system being analyzed, in a time-line manner.  And like Scan Reports, Workflows can be reused and backup/restored for later uses. |
| Reports and Workflows auto naming | From now, Drive will suggest the name for Reports and Workflows with a smart combination of device’s exact hostname or brandname, the selected scan path and the date time of each scan. This provides the easiest and fastest way to organize scan reports, especially when you have to again and again scan multiple systems. |
| Include system identifiers in Scan Reports | For many purposes in many situations, device unique identifiers like hostname, serial number are required. In v3.10.0, they are available in the txt, pdf reports. |
| Enhance OPSWAT Central Management integration | - There is not the option to remove the local reports after they have been synced up with OPSWAT Central Management - Accept OCM self-signed certificates, all required certificates must exist in the NTFS partition of Drive, under the directory names “certificates” |
| **Improvements** |  |
| Modern Look-And-Feel | In v3.10.0 user interface and experience have been upgraded to a new level that is more intuitive and convenient to navigate around. The updated areas are:   - Navigation bar, main pages and pop-up modals are now made consistent with the same look and feel. - Settings Preference now appear in tiles so you don’t have to scroll up and down to view and modify the settings - New setting modals for OPSWAT Central Management and MetaDefender Vault - Show current version in the top view - Show version of available upgrade |
| New hardware drivers have been integrated | We keep improving our compatibility by updating with some popular wi-fi external cards. |
| **Bugs fixed** |  |
| Some potential issues have been identified and fixed in this release. | - In some specific conditions there will be issue connecting to OPSWAT Central Management using HTTPS - We also fixed some bugs about encryption and mounting encrypted disks |
