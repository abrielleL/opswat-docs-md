<!-- source: https://www.opswat.com/docs/cm/configurations/product-updates -->

# Product Updates

## MetaDefender Endpoint

The Endpoint Components tab manages updates and installers for MetaDefender Endpoint.

![](https://uploads.developerhub.io/prod/97qW/ncblayfyx5at1g12ottiqwrcjz58m2xvthvga56fij95rkhtrh41l7wh0yzwhar2.png)

**Auto Update Settings**

Configure automatic update preferences for the system.

Settings:

- **Enable auto update**: Automatically checks and installs the latest updates from OPSWAT hosting servers.
- **Update frequency**: the frequency that My OPSWAT Central Management checks for an update.
  - **Active hours**: My OPSWAT Central Management won't check for updates during the specified times
    - Ex: Weekdays (Monday-Friday) from 8:00 to 17:00

## Module Updates

Administrators can configure how My OPSWAT Central Management updates modules for products such as MetaDefender Core, MetaDefender Kiosk Linux. A product instance checks if a new module version is available within My OPSWAT Central Management and updates itself if any.

Note [Staged Module Rollout](https://www.opswat.com/docs/cm/product-management/staged-module-rollout) is available for MetaDefender Core, see our detailed instructions.

![](https://uploads.developerhub.io/prod/97qW/sqn84bospo3c9m0jje565efkfq1o59ipbjldjiwn0fu5j3mqpqdhthl7fefk341d.png)

The following options are currently available:

**Internet**

My OPSWAT Central Management periodically reaches to OPSWAT update servers to fetch the latest update files. This requires [an outbound connection from My OPSWAT Central Management to OPSWAT update servers](https://www.opswat.com/docs/cm/deployment/system-requirements).

- *Recurrence Update: Daily/Weekly*
- *At: select a time in a day to check for updates.*

**Manual**

An administrator must manually upload the update files to My OPSWAT Central Management.

**Folder**

In Folder mode, OPSWAT Central Management continuously monitors the configured folder and automatically imports any available module updates from the specified location into the module update pool.

- **Delete files after import**: If selected, the files of the imported modules are deleted from the pickup folder after the import process finishes**.**

## Product Firmware Updates

Administrators can configure how My OPSWAT Central Management updates a firmware package for managed MetaDefender Kiosk Windows instances. A MetaDefender Kiosk Windows instance checks if a new version is available within My OPSWAT Central Management and updates itself if any.

![](https://uploads.developerhub.io/prod/97qW/pmz7bhyy1ik9ctft1iyuht6en1jb5jcmnvniivqp1y3310dm7essmvgbno0myv4c.png)

The following options are currently available:

**Internet**

My OPSWAT Central Management periodically reaches out to OPSWAT update servers to fetch the latest update files. This requires [an outbound connection from My OPSWAT Central Management to OPSWAT update servers](https://www.opswat.com/docs/cm/deployment/system-requirements).

- *Recurrence Update: Daily/Weekly*
- At: select a time in a day to check for updates.

**Manual**

An administrator must manually upload the update files to My OPSWAT Central Management.

> **Notes**
>
> - All times are displayed in the system's local timezone
> - Manual updates can be performed by selecting appropriate yml and zip files
> - System administrators can add additional rules for update management

## Applications Updates

Select OPSWAT Applications such as Kiosk, Core, and Industrial Firewall, can be updated from this section as detailed at [Update Application - My OPSWAT Central Management](https://www.opswat.com/docs/cm/product-management/update-application)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
