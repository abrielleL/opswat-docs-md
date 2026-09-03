<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/low-disk-space -->

# Low disk space

Disk space might be an issue on a sandbox server after a long period of heavy load, especially if the retention settings are not configured correctly (see [Retention Policy Configuration](/docs/filescan/3.1.1/configuration/retention-policy-configuration)) or some old files cannot be removed from the system for an unexpected reason.

In this case, it is crucial to understand which processes use up more disk space than expected.

Warning

Before doing a deeper investigation or cleaning up any files on the system, it is strongly recommended to **reboot the sandbox server and check if the disk usage improves**.

A reboot allows the system to purge obsolete files.

After a reboot, the first step would be checking the available disk space across all partitions:

BashCopydf -h
Example output:
Filesystem Size Used Avail Use% Mounted on
/dev/root 97G 32G 66G 33% /
tmpfs 16G 0 16G 0% /dev/shm
tmpfs 6.2G 2.5M 6.2G 1% /run
tmpfs 5.0M 0 5.0M 0% /run/lock
/dev/nvme0n1p15 105M 6.1M 99M 6% /boot/efi
tmpfs 3.1G 4.0K 3.1G 1% /run/user/1000

A total disk usage of 30-50 GB is typical on a sandbox server with continuous medium load. If your total disk usage is substantially more, then further investigation is necessary to determine which system folders use that extra space.

If you have multiple system partitions, then please pay special attention to the available space on the `/home`, `/var` and `/data` partitions, because the sandbox service actively uses those partitions.

Recommended minimum sizes for the most important partitions:

| Partition | Minimum size |
| --- | --- |
| /var | 50 GB |
| /home | 20 GB |
| /data | 20 GB |
| /usr | 10 GB |

It is also recommended to check the disk usage of top-level system folders:

BashCopysudo du --max-depth=1 -hx / 2>/dev/null | sort -hr
Example output:
32G /
23G /var
4.9G /usr
3.4G /home
711M /data
263M /root
140M /boot
7.5M /etc
200K /tmp
36K /snap
16K /opt
16K /lost+found
4.0K /srv
4.0K /mnt
4.0K /media

If a top-level folder looks larger than expected, it is possible to drill down to the necessary level, e.g.:

BashCopysudo du --max-depth=1 -hx /var 2>/dev/null | sort -hr
sudo du --max-depth=1 -hx /var/lib/docker 2>/dev/null | sort -hr
sudo du --max-depth=1 -hx /home 2>/dev/null | sort -hr
sudo du --max-depth=1 -hx /home/sandbox 2>/dev/null | sort -hr
sudo du --max-depth=1 -hx /home/sandbox/sandbox 2>/dev/null | sort -hr
sudo du --max-depth=1 -hx /usr 2>/dev/null | sort -hr

When the largest folders are found on the system, it is usually obvious which process is responsible for writing to those folders.

### [Docker disk usage](/docs/filescan/3.1.1/troubleshooting/low-disk-space#docker-disk-usage)

The Sandbox service uses several Docker containers, and it is also recommended to check the total disk usage of Docker:

BashCopysudo docker system df
Example output:
TYPE TOTAL ACTIVE SIZE RECLAIMABLE
Images 17 9 16.85GB 3.35GB (19%)
Containers 18 18 2.021GB 0B (0%)
Local Volumes 25 5 2.849MB 86.97kB (3%)
Build Cache 131 0 0B 0B

Note that the total disk usage of Docker usually corresponds to the size of the `/var` top-level folder (or partition).

### [Optional tools](/docs/filescan/3.1.1/troubleshooting/low-disk-space#optional-tools)

Using these commands is usually enough to discover the largest folders and sub-folders. If it is possible to install additional packages, then the `ncdu` utility provides an interactive summary of disk usage:

BashCopysudo apt install ncdu
sudo ncdu /

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
