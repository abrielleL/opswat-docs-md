<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/troubleshooting/too-many-sockets-or-files-open -->

# Too Many Sockets or Files Open

Only on Linux systems: if too many sockets or files are open by the process this can cause problems.

## [How to detect](/docs/mdcore/v5.21.0/troubleshooting/too-many-sockets-or-files-open#how-to-detect)

Check the **file descriptor** limit:

ulimit -n

Check the used file descriptor count on a running process:

watch -n 1 "ls /proc/\`ps -eo comm,pid | awk '\$1 == \"ometascan\" { print \$2 }'\`/fd | wc -l"

If the count is close to the limit this will cause problems.

Rule of thumb: 1 scan workflow requires 2-3 file descriptors.

## [Solution](/docs/mdcore/v5.21.0/troubleshooting/too-many-sockets-or-files-open#solution)

Increasing the number of file descriptors

The command **ulimit -n** displays the current set number of maximum file descriptors. In order to increase this number follow the next steps:

Append this line to **/etc/sysctl.conf**

fs.file-max = 65535

Add the following lines to **/etc/security/limits.conf**

* soft proc 65535
* hard nproc 65535
* soft nofile 65535
* hard nofile 65535

Restart the system to apply the new configuration. After restart you can check the changed limit by issuing **ulimit -n**

> ulimit -n
> 65535
