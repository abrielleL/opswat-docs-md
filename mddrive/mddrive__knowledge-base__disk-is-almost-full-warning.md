<!-- source: https://www.opswat.com/docs/mddrive/knowledge-base/disk-is-almost-full-warning -->

# "Disk Is Almost Full. Used: 100%" on the 64GB Thumb Drive

## [Issue](/docs/mddrive/knowledge-base/disk-is-almost-full-warning#issue)

The notification bar shows the following message: *"Disk is almost full. Used: 100%"*

It has been reported that after showing this message, MetaDefender Drive takes longer than expected to perform a scan, and in some cases, it fails to boot.

## [Cause](/docs/mddrive/knowledge-base/disk-is-almost-full-warning#cause)

After using MetaDefender Drive for long scans or with large archive files, the temporary working space of the drive becomes full. MetaDefender Drive can't function properly if the *temp* data isn't flushed.

Error

This issue has been reported for the OPSWAT MetaDefender Drive USB version, which has a working space of around 21 GB.

## [Solution](/docs/mddrive/knowledge-base/disk-is-almost-full-warning#solution)

You need to fix your MetaDefender Drive using MetaDefender Drive Toolkit. This will flash your Drive with its current or latest software version and keep your previous scan reports.

Please follow the instructions to download and use the MetaDefender Drive Toolkit: <https://docs.opswat.com/mddrive/advanced-usages/drive-toolkit>.

## [**To prevent the issue from happening in the future:**](/docs/mddrive/knowledge-base/disk-is-almost-full-warning#to-prevent-the-issue-from-happening-in-the-future)

Since MetaDefender Drive USB has 21 GB available for the temporary working space, please plan your scans with less than 21GB of data per session.

You can also adjust the [**Archive Handling**](https://docs.opswat.com/mddrive/configuration/preferences---archive-handling) and [**Scan Settings**](https://docs.opswat.com/mddrive/configuration/preferences---scan-settings) from **Preferences** ***→*** **Settings** to achieve optimal performance and reduce the chances of this issue happening:

Adjust how MetaDefender Drive handles archive files

Adjust the settings for max file sizes and timeouts
