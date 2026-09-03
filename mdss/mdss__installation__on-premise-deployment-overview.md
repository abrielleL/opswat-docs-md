<!-- source: https://www.opswat.com/docs/mdss/installation/on-premise-deployment-overview -->

# On-Premise Deployment Overview

## [Before installation](/docs/mdss/installation/on-premise-deployment-overview#before-installation)

Before you begin the installation, ensure that your On-premise environment meet the [system requirements](/docs/mdss/getting-started/general-system-requirements). If you are installing MetaDefender Storage Security on the same server as MetaDefender Core, the server must meet the cumulative system requirements of all the products.

## [Installation General Steps](/docs/mdss/installation/on-premise-deployment-overview#installation-general-steps)

1. Download the package of your choice from the [My OPSWAT](https://my.opswat.com/)
2. Check the [Production Considerations](/docs/mdss/installation/production-considerations)
3. Install the package on your computer based on [Installation Methods](/docs/mdss/installation/installation-methods)
4. Open a web browser and point to http://<server name or IP> (by default, port 80 is used)
5. Complete the installation and proceed with the [onboarding](/docs/mdss/operations/onboarding)

## [Installation notes](/docs/mdss/installation/on-premise-deployment-overview#installation-notes)

- **Internet Connectivity:** The installation requires internet access to download packages from the container registry
- **.NET Framework:** On Windows, the installer will download and apply .NET Framework 4.8 if it is not already installed
- **Support:** If you encounter issues, open a support case and include the “Metadefender*” files located in `C:\Users\<user>\AppData\Local\Temp`

## [Offline Installation](/docs/mdss/installation/on-premise-deployment-overview#offline-installation)

If you need to perform an offline installation, please refer to the [Linux Offline Installation](/docs/mdss/installation/linux-offline-installation) for detailed instructions on how to install MetaDefender Storage Security without an active internet connection. This guide includes steps for preparing necessary dependencies.
