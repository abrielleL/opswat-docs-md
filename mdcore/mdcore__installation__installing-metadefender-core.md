<!-- source: https://www.opswat.com/docs/mdcore/installation/installing-metadefender-core -->

# Installation

Starting with MetaDefender Core 4.20.0, the centralized/shared database deployment model is supported (all MetaDefender Core instances share the same database), along with traditional standalone database mode (every MetaDefender Core instance has its own database to manage).

- [Standalone mode](/docs/mdcore/installation/standalone-mode)
- [Shared Database Mode](/docs/mdcore/installation/shared-database-mode)

## [Installation](/docs/mdcore/installation/installing-metadefender-core#installation)

1. Download the package of your choice from [My OPSWAT](https://my.opswat.com/home/metadefender-core)
2. Install the package on your computer via the Command Line or via the Wizard
3. Open a web browser and point to http://<server name or IP>:<port>

   - The default port is **8008**
   - In case of problem check [Inaccessible Management Console](/docs/mdcore/troubleshooting/inaccessible-management-console) page
4. Complete the required steps of the [basic configuration wizard](/docs/mdcore/installation/initial-setup-using-configuration-wizard)
5. You must [activate](/docs/mdcore/installation/metadefender-core-licensing) this deployment to use its features

## [Installation notes](/docs/mdcore/installation/installing-metadefender-core#installation-notes)

- If the MetaDefender Core package **dependencies are not installed** on your system you may need to have a working Internet connection or you may have to provide the Installation media during the installation. Consult your Operating System documentation on how to use Installation media as a package repository.
- During installation the databases might need to be upgraded. This could take noticeable time depending on database size (eg.: length of scan history).
