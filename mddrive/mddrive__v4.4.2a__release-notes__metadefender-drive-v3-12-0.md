<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/release-notes/metadefender-drive-v3-12-0 -->

# MetaDefender Drive v3.12.0

| [MetaDefender Drive v3.12.0](/docs/mddrive/v4.4.2a/release-notes/metadefender-drive-v3-12-0#metadefender-drive-v3120) Released on Dec 24, 2021 | This is a major release that adds new feature as well as improvement and stability |
| --- | --- |
| **New features** |  |
| Data Integrity Verification | When a baseline is set for a scan workflows, after the analysis, a report will be provided with all the changes that have been found on the selected file path. |
| **Improvements** |  |
| Upgraded to new kernel to support new hardware | - Support Intel® Iris® Xe Graphics. - Support Dell Wireless 1490 (802.11a/g). - Support nVIDIA Quadro hi-end graphic cards. |
| Languages | - French version has been improved. |
| Some defects have been reported and fixed | - "Version of OCM is not compatible" for OCM v7.19.0 .1150. - “Settings preservation” restoration had some critical issues. We fixed it and settings of Drive will be restored to default states when upgrading from previous version to 3.12.0; but moving forward it will work as expected. |
| **Known Issues** |  |
| MetaDefender Drive will crash if running on some macOS devices which have disks encrypted by FileVault. | The new kernel is not very well supporting FileVault. We recommend macOS users not upgrade your Drive.  The fix for it will be available in 3.12.1, targeted in Januarry 2022. |
