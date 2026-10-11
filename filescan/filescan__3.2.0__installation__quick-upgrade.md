<!-- source: https://www.opswat.com/docs/filescan/3.2.0/installation/quick-upgrade -->

# Upgrade

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check System Requirements

Before starting the installation, please make sure that your target system meets the [Technical Requirements](/docs/filescan/3.2.0/installation/technical-requirements) and the installation is **performed by a person with basic Linux skills**.

If your target system is currently running **Ubuntu 20.04**, then please upgrade to **Ubuntu 22.04 LTS** following the [Operating System Upgrade](/docs/filescan/3.2.0/installation/operating-system-upgrade) guide.

Warning

This page only refers to product installation with a **stable Internet connection**!

For **offline installations**, please follow the [Offline Installation](/docs/filescan/3.2.0/installation/offline-installation) guide instead!

Please walk through the following steps:

**Step #1 -** **Download and copy the release archive**

Download the release archive from <https://my.opswat.com/portal/products>

Copy the release archive to a folder on the Sandbox server, e.g. your home folder

**Step #2 - Unpack the release archive:**

Info

Please use the **password** that you received from your OPSWAT Sales Representative!

Please adjust the x.y.z **version numbers** to match the downloaded filename.

BashCopy7za x -aoa -p"PASSWORD" MetaDefender_Sandbox_vx.y.z-Standalone.zip

**Step #3 - Move to the installation folder:**

BashCopycd sandbox-installer

**Step #4 - (Optional) Configure** `install.cfg` **to specify a custom user name and installation path**

There is no need to modify `install.cfg` if you used the default options during the original installation.

More details available in [Installation Options](/docs/filescan/3.2.0/installation/installation-options).

Warning

If you configured **a custom user name and installation path** during your original installation, please configure the **same values**, otherwise the installer cannot find the existing installation!

Info

If you use the default options, the existing **filescanio** user will be automatically renamed to **sandbox**.

If you have an existing installation at the default directory: **/home/filescanio/FileScanIO** then this directory will be moved & renamed to **/home/sandbox/sandbox**.

**Step #5 - Run the install shell script**

Note that this operation can take up to 20-30 minutes (depending on available network bandwidth).

BashCopysudo ./install.sh

All components should restart automatically after the upgrade is completed.

**Step #6 - (Optional) Troubleshooting if the Sandbox service failed to** **restart**

Verify the status of the `sandbox` service and if the running docker container are healthy:

BashCopysudo service sandbox status
sudo docker ps

The `sblog` bash command can be used to check the application logs for different system components.

This command is available to all users (but might require sudo privileges):

BashCopy# Show logs from the transform component
sblog
# Show logs from the broker component
sblog -b

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
