<!-- source: https://www.opswat.com/docs/filescan/installation/quick-installation -->

# Online Installation

Before starting the installation, please make sure that your target system meets the [Technical Requirements](/docs/filescan/installation/technical-requirements) and the installation is **performed by a person with basic Linux skills**.

Warning

This page only refers to product installation with a **stable Internet connection**!

For **offline installations**, please follow the [Offline Installation](/docs/filescan/installation/offline-installation) guide instead!

Warning

If you have an active **AV engine or EDR agent** on the target system, please read this page before starting the installation: [Which paths should be excluded from AV engine/EDR agent scans on the sandbox server?](/docs/filescan/faq/which-paths-should-be-excluded-from-av-engine-edr-agent-scans-on)

Pro Tip

Before installing, please check out our [Proxy Usage](/docs/filescan/installation/installation-with-proxy) or [Air-gapped Systems](/docs/filescan/installation/notes-for-air-gapped-environments) pages if these requirements apply to you!

Please walk through the following steps. If you encounter any issues during installation, refer to our [Troubleshooting Guide.](https://docs.opswat.com/filescan/troubleshooting)

## [Preparation](/docs/filescan/installation/quick-installation#preparation)

### [Ubuntu 22.04 or Ubuntu 24.04](/docs/filescan/installation/quick-installation#ubuntu-2204-or-ubuntu-2404)

**Step #1 - (Optional) Create a new user that will own all the installed files and run the Sandbox services**

BashCopysudo adduser --disabled-password --gecos "" sandbox

**Step #2 - Install 7-Zip:**

BashCopysudo apt-get update
sudo apt-get install p7zip-full -y
### [Red Hat 9.x or Rocky Linux 9.x](/docs/filescan/installation/quick-installation#red-hat-9x-or-rocky-linux-9x)

EPEL repositories

Some packages require the EPEL repositories. Ensure they are available in your package manager.

**Step #1 - Install EPEL repositories**

BashCopysudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm -y

**Step #2 - (Optional) Create a new user that will own all the installed files and run the Sandbox services**

BashCopysudo useradd --create-home sandbox
sudo passwd -l sandbox

**Step #3 - Install 7-Zip:**

BashCopysudo dnf update -y
sudo dnf install p7zip -y
## [Installation](/docs/filescan/installation/quick-installation#installation)

**Step #1 - Download and unpack the product installer:**

Download the release archive from <https://my.opswat.com/portal/products> and save it to a convenient location, e.g. your home folder.

The release archive is password protected and needs to be unpacked using 7-Zip:

Info

Please use the **password** that you received from OPSWAT support!

Please adjust the x.y.z **version numbers** to match the downloaded filename.

BashCopy7za x -aoa -p"PASSWORD" MetaDefender_Sandbox_vx.y.z-Standalone.zip

**Step #2 - Move to the installation folder:**

BashCopycd sandbox-installer

**Step #3 - (Optional) Edit install.cfg to specify a custom user name and installation path**

*Note: The default settings work fine for standard deploys and all features can be configured post installation.*

More details are available in [Installation Options](/docs/filescan/installation/installation-options).

**Step #4 - Run the install shell script**

Note that this operation can take up to 20-30 minutes (depending on available network bandwidth).

BashCopysudo ./install.sh

The first step of the installation process is accepting the product EULA, you need to **press Y** to start the installation.

**Step #5 - Access the Sandbox web server (**[**https://localhost:443**](https://localhost:443)**) and setup the initial Admin user**

**Step #6- Add your Activation Key**

The system will not be able to generate scan reports yet, as a **valid Activation Key is required.**

Please use the Activation Key that you received from your OPSWAT Sales Representative, and follow the instructions on the [License Activation](/docs/filescan/installation/license-activation) page.

Simple steps for Online activation:

Navigate to the *Admin panel > Settings > Integrations > License Management* tab, then click on *Activate All,* then **enter your license key**!

**Step #7 - Scan your preferred test file to check if the Sandbox system functions properly**

**Step #8 - (Optional) Troubleshooting if the Sandbox service failed to** **initialize**

Verify the status of the `sandbox` service and if the running docker container are healthy:

BashCopysudo service sandbox status
sudo docker ps

The `sblog` bash command can be used to check the application logs for different system components.

This command is available to all users (but might require sudo privileges):

BashCopy# Show logs from the transform component
sblog
# Show logs from the broker component
sblog -bBest practices

For a more comprehensive report, it is considered a best practice to enable the use of the MD Cloud Reputation API. For further details on this: [MetaDefender Cloud Reputation Service](/docs/filescan/integrations/reputation-api-integration)

The sandbox API is documented here: [**MD Sandbox API**](https://docs.opswat.com/filescan/metadefender-sandbox-api-reference-v1)

## [Important notes for air-gapped systems](/docs/filescan/installation/quick-installation#important-notes-for-air-gapped-systems)

Please see the [Air-gapped Systems](/docs/filescan/installation/notes-for-air-gapped-environments) subpage.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
