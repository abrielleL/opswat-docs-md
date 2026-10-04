<!-- source: https://www.opswat.com/docs/mddrive/v4.4.9/knowledge-base/failed-to-detect-or-interact-with-drives -->

# Toolkit Fails to Detect Some Drives

## [Issue](/docs/mddrive/v4.4.9/knowledge-base/failed-to-detect-or-interact-with-drives#issue)

MetaDefender Drive Toolkit cannot detect one or more of the inserted MetaDefender Drives. As a result, the MetaDefender Drive Toolkit can't perform actions such as install, activate, or update scanning engines for the undetected drives.

MetaDefender Drive Toolkit failing to detect two plugged-in MetaDefender Drives

## [Cause](/docs/mddrive/v4.4.9/knowledge-base/failed-to-detect-or-interact-with-drives#cause)

This issue often happens when another process competes for resources during I/O operations, leading to a potential "race condition," a condition that happens when two or more threads can access shared data and try to change it at the same time. A common cause of this conflict is antivirus software, a policy restricting USB device usage, or a competing network file system mounting service.

The following screenshot is an example of how a network mapping service can lead to such a conflict and a race condition. The disk partitions *E* and *F* are being used and assigned by an SSHFS mounting service, while they are still being seen as *E* and *F* by Windows' Disk Management:

Race condition example of MetaDefender Drives E and F

Another example is when the Disk Manager is opening and handling multiple MetaDefender Drives. This will prevent MetaDefender Drive Toolkit from gaining access to these MetaDefender Drives:

Windows Disk Manager using MetaDefender Drive partitions

## [Solution](/docs/mddrive/v4.4.9/knowledge-base/failed-to-detect-or-interact-with-drives#solution)

1. Find the processes that use the USB devices and prevent MetaDefender Drive Toolkit from reading the inserted MetaDefender Drives.
2. Terminate these processes.
3. Safely eject the unreadable MetaDefender Drives.
4. Re-insert the MetaDefender Drives back into the target machine and try again with MetaDefender Drive Toolkit.

Ending processes that prevent MetaDefender Drive Toolkit from accessing the inserted drives

If the issue persists after trying the previous solutions, please get in touch with OPSWAT's customer success specialists with a support packages or a log file. For instructions on generating support packages and extracting logs, please check the [Support Packages and Logs](https://www.opswat.com/docs/mddrive/troubleshooting/generate-supportpackage) page.
