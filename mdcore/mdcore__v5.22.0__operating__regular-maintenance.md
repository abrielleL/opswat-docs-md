<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/operating/regular-maintenance -->

# Regular Maintenance

## [Checking for Upgrades](/docs/mdcore/v5.22.0/operating/regular-maintenance#checking-for-upgrades)

Metadefender Core checks for available database updates and scan engine updates for the installed anti-malware engines on a regular basis. To manually update a scan engine or its database, click on the update now button or the upload package link on the **Inventory > Engines** page.

## [Checking Engines / Databases Health](/docs/mdcore/v5.22.0/operating/regular-maintenance#checking-engines--databases-health)

Metadefender Core regularly checks for available database updates and scan engine updates for the installed anti-malware engines. Both database and engine upgrades are based on a mechanism that checks for authenticity of the origin of the upgrade package. If the authenticity is confirmed, the upgrade package is downloaded. As an extra stability measure each downloaded upgrade package is tested locally to ensure that it is functioning properly. Only after successful testing will the upgrade package be distributed among MetaDefender Core nodes.
