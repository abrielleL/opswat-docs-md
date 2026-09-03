<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/eset-engine-failed-to-initialize-on-the-hardened- -->

# Why have the ESET scan engine failed to initialize on the hardened Linux OS?

This article applies to all MetaDefender Core V5 and V4 releases deployed on hardened Linux systems.

Pro Tip:

For customers using a hardened Linux OS, such as Hardened Amazon Linux 2, the ESET engine will fail to initialize unless certain changes are made.

The ESET scan engine require execution permission on a temp folder. However, while on the hardened system, such permissions are restricted on: **/var/tmp**, resulting in the engine’s failure to initialize.

Browse [MetaDefender Configuration](/docs/mdcore/configuration/metadefender-configuration) for instructions on how to change the default temp folder (**tempdirectory**) to a folder that has execution permission.

Support:

If you have followed all of the steps above but your **ESET** engine are still failing to initialize, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
