<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-do-i-check-if--noexec--flag-exists-on-a-linux-os- -->

# How do I check if "noexec" flag exists on a Linux OS?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Linux systems.

Pro Tip:

On Linux, MetaDefender Core deploys its engines and files in the **/var/lib** and **/usr/lib** folders. Depending on your file mount security policy, you may or may not have mounted **/var** or **/usr** with the flag **noexec**.

Essentially, the **noexec** flag will not allow any direct execution of binaries from the mounted filesystem/folder. In essence, if this flag exists, MetaDefender Core will not be able to launch its engine processes.

This will result in an engine with a **permanently_failed** module.

**To c heck if the ‘noexec’ flag exists on /var or /usr simply do the following:**

- Run Terminal and use one of the following commands:

  - **findmnt -l | grep noexec**

OR:

- **mount | grep noexec**

- Using the commands above will reveal whether there is a mount point with the **noexec** flag.
- If **/var** or **/usr** exist on the list, you must remove the **noexec** flag with the relevant following command:

  - **mount -o remount,rw,exec /var**
  - **mount -o remount,rw,exec /usr**

Support:

If you have followed all of the steps above but still have a **permanently_failed** module, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
