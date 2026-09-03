<!-- source: https://www.opswat.com/docs/filescan/3.1.1/installation/uninstall-guide -->

# Uninstall Guide

Please be aware that removing MetaDefender Sandbox will delete all configuration and data permanently! This cannot be undone!

Restart

Please be aware that after the uninstall process finished the system must be restarted. This is mandatory for the cleanup.

Please walk through the following steps to remove MetaDefender Sandbox from your system / VM.

**Step #1 - Navigate to the installation folder**

BashCopycd /home/sandbox/sandbox

**Step #2 -** **Ensure that the uninstall script is executable**

BashCopychmod +x uninstall.sh

**Step #3 - Run the uninstall script as root**

BashCopysudo ./uninstall.sh

**Step #4 - Manually confirm that you want to delete all Sandbox configuration and data**

Removing APT packages

The uninstall process will not remove APT packages. They can be removed manually if not needed anymore.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
