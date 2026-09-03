<!-- source: https://www.opswat.com/docs/mddrive/v4.4.7/release-notes/metadefender-drive-v3-13-0 -->

# MetaDefender Drive v3.13.0

| [MetaDefender Drive v3.13.0](/docs/mddrive/v4.4.7/release-notes/metadefender-drive-v3-13-0#metadefender-drive-v3130) Released on Apr 08, 2022 | This is a major release that adds new feature as well as improvement and stability |
| --- | --- |
| **New features** |  |
| Scan BIOS/UEFI threats and notify on new Firmware updates availability | UEFI threats are gradually becoming a norm and hardware vendors are taking more precautions to mitigate attacks and to provide updates regularly. This version of MetaDefender Drive we are able to scan and report if system firmware is attacked and to notify if there is a new version of system firmware is available. |
| Scan Disk Boot Sector for virus | The boot sector virus resides in system hard drive boot sectors / partition tables waiting to be initiated when the computer turns on, to executes DOS commands and infects remaining storage devices attached to your computer. This new version of MetaDefender Drive can detect such threats early before the system fires up. |
| **Improvements** |  |
| The UX for Report area has been improved to be more consistent and focused |  |
| Some minor bugs have been fixed |  |
| Upgrade Drive's kernel to improve stability and prepare for new features |  |
| **Known Issues** |  |
| MetaDefender Drive will crash if running on some macOS devices which have disks encrypted by FileVault. | The new kernel is not very well supporting FileVault. We recommend macOS users not upgrade your Drive.  The fix for it will be available in 3.14.0, targeted in Jun 2022. |
