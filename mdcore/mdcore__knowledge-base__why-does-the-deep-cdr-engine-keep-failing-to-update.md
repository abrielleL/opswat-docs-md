<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-the-deep-cdr-engine-keep-failing-to-update -->

# Why does the Deep CDR engine keep failing to update?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Please Note:

Please ensure that **Microsoft Visual C++ 2017 Redistributable Package** is installed.

If this third-party requirement is not met, it could result in Deep CDR’s failure to activate, update and execute.

**Linux dependencies**:

CentOS: libgomp, ncurses-compat-libs

RedHat 7.x: libgomp, ncurses

RedHat 8.x: libgomp, ncurses-compat-libs, libnsl

Ubuntu/Debian: libgomp1, libncurses5

libgdiplus 6.0.5 or above (only need if you have file type conversion from documents to images such as DOCX to JPG, ...)

Another factor that could result in Deep CDR’s failure (and other AV engines) to update is **inadequate network bandwidth**.

In an online environment where MetaDefender Core is configured to download engine update packages directly from an OPSWAT update server source, using a gigabit network speed (125MB/sec) is highly recommended to avoid potential network related issues during file downloads.

At the very least, the requirement is a network speed of 100Mbps (12.5MB/sec).

Support:

If you have followed the instructions above but **Your Deep CDR Engine Still Keeps Failing To Update**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
