<!-- source: https://www.opswat.com/docs/mddrive/knowledge-base/how-do-i-deploy-the-clean-metadefender-drive -->

# How do I deploy the clean MetaDefender Drive?

This article applies to the MetaDefender Drive Toolkit and the Windows environment

When reflashing the MD Drive with the MD Drive Toolkit, the old data will be backed up and restored automatically to the new deployment. But in some cases, a clean deployment is required. You can follow the instructions below to have a clean-up of MD Drive.

Warning:

After following these steps, the old data will be erased, including settings, scan result, license, and engine package.

## 1. Using Rufus (<https://rufus.ie/en/>)

You can download Rufus software and follow the setup below to clean up the MD Drive storage

## [2. Using Windows Disk Management](/docs/mddrive/knowledge-base/how-do-i-deploy-the-clean-metadefender-drive#2-using-windows-disk-management)

Using Windows Disk Management can help you manually delete all of the existing partitions of the MD Drive. This action requires administrator permission.

When plugging the MD Drive into the computer, open Windows Disk Management and locate the Disk with the label “MetaDefender Drive”

Right-click on all of the partitions of that disk and choose “Delete Volume.”

After deleting, you can only see 1 Unallocated space.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
