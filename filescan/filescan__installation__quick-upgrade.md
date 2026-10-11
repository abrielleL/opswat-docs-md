<!-- source: https://www.opswat.com/docs/filescan/installation/quick-upgrade -->

# Upgrade

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check System Requirements

Before starting the installation, please make sure that your target system meets the [Technical Requirements](/docs/filescan/installation/technical-requirements) and the installation is **performed by a person with basic Linux skills**.

If your target system is currently running **Ubuntu 20.04**, then please upgrade to **Ubuntu 22.04 LTS** following the [Operating System Upgrade](/docs/filescan/installation/operating-system-upgrade) guide.

Warning

This page only refers to product installation with a **stable Internet connection**!

For **offline installations**, please follow the [Offline Installation](/docs/filescan/installation/offline-installation) guide instead!

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

More details available in [Installation Options](/docs/filescan/installation/installation-options).

Warning

If you configured **a custom user name and installation path** during your original installation, please configure the **same values**, otherwise the installer cannot find the existing installation!

**Step #5 - Run the install shell script**

Warning

The **first start after the upgrade** updates the database. On a **large database** (100,000 reports or more) this can take from a few minutes up to an **hour or more**.

While the update runs, the web interface may show errors, and file uploads may not work. This stops by itself when the update is finished. **No data is lost.**

Until the update is finished, please **do not restart** the Sandbox service or the server, and do not run the upgrade again. A restart starts the database update again from the beginning.

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
