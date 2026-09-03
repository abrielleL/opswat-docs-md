<!-- source: https://www.opswat.com/docs/mdss/where-to-get-help/permission-denied-while-uninstalling-on-linux -->

# Permission denied while uninstalling on Linux

On some Linux distributions that have **SELinux (Security-Enhanced Linux)** enabled by default you may encounter a "Permission denied" message when uninstalling MDSS. The uninstall still completes successfully and only some docker containers might still be left running if `mdss -u clean` was not executed before the uninstall. This is due to SELinux policies and can be avoided by disabling SELinux temporarily before uninstalling by running:

BashCopysudo setenforce 0
