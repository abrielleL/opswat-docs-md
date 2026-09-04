<!-- source: https://www.opswat.com/docs/mddrive/v4.4.8/knowledge-base/intel-rapid-storage-technology-intel-rst -->

# Warning: Intel RST Enabled

## [Issue](/docs/mddrive/v4.4.8/knowledge-base/intel-rapid-storage-technology-intel-rst#issue)

MetaDefender Drive boots the target device successfully but there is no disk found under **Disk Status and Remediation** page.

## [Cause](/docs/mddrive/v4.4.8/knowledge-base/intel-rapid-storage-technology-intel-rst#cause)

Some laptop and desktop devices come with Intel RST enabled by default. Intel RST prevents MetaDefender Drive from detecting and accessing storage partitions.

## [Solutions](/docs/mddrive/v4.4.8/knowledge-base/intel-rapid-storage-technology-intel-rst#solutions)

- Go to your device's BIOS menu and find the SATA configuration section.
- If you find the SATA Mode set to RAID or something like "RAID: ON" or "with RAID", switch it to AHCI.
- Plug MetaDefender Drive and try to boot it again.
- After using MetaDefender Drive and before booting Windows again, visit the BIOS menu again to revert the SATA configuration to its previous state.

Warning

OPSWAT MetaDefender Drive doesn't alter your data.

There is a chance that changing the storage configuration can corrupt your data and lead to an irrecoverable loss. If you break a RAID setup, your data may no longer be accessible. Likewise, if you change the controller type from RST to AHCI, Windows may no longer be able to boot.

Please carefully follow the instruction here for your system's safety: <https://discourse.ubuntu.com/t/ubuntu-installation-on-computers-with-intel-r-rst-enabled/15347>
