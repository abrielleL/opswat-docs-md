<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-to-use-a-ramdisk-for-the-tempdirectory- -->

# How to Use a RAMDISK for the tempdirectory?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender ICAP Server releases deployed on both Windows & Linux systems.

In order to improve the file scan speed, a custom tempdirectory can be set for the Metadefender ICAP Server.

#### [1. Instructions for Windows](/docs/mdicap/v5.15.0/knowledge-base/how-to-use-a-ramdisk-for-the-tempdirectory-#1-instructions-for-windows)

**Step 1:**

Create a RAMDISK on your system.

We recommend the following tool for this: [Tools and utilities for Windows](http://www.ltr-data.se/opencode.html/#ImDisk)

After installation, use the **ImDisk Virtual Disk Driver** application to create a new RAMDISK.

Mount a new virtual disk:

After disk creation, Windows will ask you to format the new disk.

**Step 2:**

Create, or edit the following registry entry:

HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\global\tempdirectory

where tempdirectory should be a string value with a desired location, for example: Z:\tempdir

**Step 3:**

The changes to take effect restart the mdicapsrv service.

After the service restart, your custom directory will be used for temporary file storage during file scan.

#### [2. Instructions for Linux:](/docs/mdicap/v5.15.0/knowledge-base/how-to-use-a-ramdisk-for-the-tempdirectory-#2-instructions-for-linux)

**Step 1:** Update the file fstab in the directory /etc/fstab

# Add this line at the end of the file
tmpfs /mnt/ramdisk tmpfs size=5G,uid=1000,gid=1000,mode=0755 0 0

**Step 2:** Mount this directory

sudo mount -a

**Step 3:** Validate the directory

sudo df -h /mnt/ramdisk

Please note that the mdicapsrv service can write to this directory.

**Step 4:** Update the config file /etc/mdicapsrv/mdicapsrc.conf

[global]
dbmode=1
icapaddress=0.0.0.0
icapport=1344
icaps_port=11344
restaddress=*
restport=8048
webhook_address=0.0.0.0
tempdirectory=/mnt/ramdisk
[logger]
logfile=/var/log/mdicapsrv/mdicapsrv.log
loglevel=info
nginx_logfile=/var/log/mdicapsrv/nginx-mdicapsrv.log

The changes to take effect restart the mdicapsrv service.

After the service restart, your custom directory will be used for temporary file storage during file scan.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
