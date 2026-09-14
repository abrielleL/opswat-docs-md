<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/installation/on-premise-deployments-overview -->

# On-Premise Installation Overview

## [Before installation](/docs/mdicap/v5.14.1/installation/on-premise-deployments-overview#before-installation)

Before you begin the installation, ensure that your On-premise environment meet the [General System Requirements](/docs/mdicap/v5.14.1/getting-started/general-system-requirements). If you are installing MetaDefender ICAP Server on the same server as MetaDefender Core, the server must meet the cumulative system requirements of all the products.

## [Installation General Steps](/docs/mdicap/v5.14.1/installation/on-premise-deployments-overview#installation-general-steps)

1. Download the package of your choice from the [My OPSWAT](https://my.opswat.com/)
2. Check the [Production Considerations](/docs/mdicap/v5.14.1/installation/production-considerations)
3. Install the package on your computer based on your OS - [Installation Methods](/docs/mdicap/v5.14.1/installation/installation-methods)
4. Open a web browser and point to http://<server name or IP> (by default, port 8048 is used)

## [Installation notes](/docs/mdicap/v5.14.1/installation/on-premise-deployments-overview#installation-notes)

Warning

Starting with MetaDefender ICAP Server 5.2.0, the centralized/shared database deployment model is supported (all MetaDefender ICAP Server instances share the same database), along with traditional standalone database mode (every MetaDefender ICAP Server instance has its own database to manage)

Please check [PostgreSQL Database Deployment Options](/docs/mdicap/v5.14.1/installation/installation-postgresql-options) before install

- **Internet Connectivity:** The installation requires internet access to download libraries and activate the instance.

## [Offline Installation](/docs/mdicap/v5.14.1/installation/on-premise-deployments-overview#offline-installation)

If you need to perform an offline installation, please contact sales for detailed instructions on how to install MetaDefender ICAP Server without an active internet connection.
