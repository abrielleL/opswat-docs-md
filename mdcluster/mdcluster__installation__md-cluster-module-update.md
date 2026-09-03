<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-module-update -->

# Module update

MetaDefender Cluster (MD Cluster) introduces three modes of Module Update. To switch between the modes, please sign in to MD Cluster **Control Center** console, navigate to `Settings` and select `Module Update` tab.

Info

Online update mode is enabled by default.

## [Online module update](/docs/mdcluster/installation/md-cluster-module-update#online-module-update)

In online update mode, MD Cluster **Control Center** will base its checks on the activated licenses to find and download the latest engine packages from OPSWAT online update infrastructure, repeating this process every four hours.

All downloaded engine packages are verified and stored in MD Cluster **File Storage** for licensed MetaDefender Core instances to pull, install, or upgrade on their end. Through this mechanism, the instances cease to independently pull the engine packages from the update infrastructure, conserving network bandwidth while enhancing their readiness.

## [Offline module update](/docs/mdcluster/installation/md-cluster-module-update#offline-module-update)

In offline update mode, administrators must download the licensed engine packages from **MetaDefender Update Downloader** and upload them manually to MD Cluster **Control Center**.

Info

Please reference [here](https://www.opswat.com/docs/mddownloader/operating/download-all-update-packages) for more details about downloading engine packages from MetaDefender Update Downloader.

1. Sign in to MD Cluster **Control Center** console.
2. Go to `Inventory` > `Modules`.
3. Press `Upload Package` at the top right corner.

Info

`Update All` is always disabled if Offline Update mode is selected in `Settings` > `Module Update`.

4. Choose your engine package files.

5. Click `Update` to submit the package files.

Info

Package files from various engines can be selected simultaneously.

6. Wait until engine packages are ready.
7. Engine update statuses on MetaDefender Core instances can be monitored in `Dashboard` > `System Health` > `Worker Health`.

## [Local folder update](/docs/mdcluster/installation/md-cluster-module-update#local-folder-update)

In local folder update, the administrator can specify the path to a folder in `Pick updates from` option. MD Cluster **Control Center** autonomously gathers packages that are added to the folder, then verifies the packages and stores them in MD Cluster **File Storage** for licensed MetaDefender Core instances to retrieve, install, or update on their end.

The administrator has the option to select `Delete files after import` so that MD Cluster **Control Center** wipes all packages upon success.

Info

Network-mapped drives and UNC paths are permitted.

- On Windows, ensure that MD Cluster Control Center has permission to access to the folder.
- On Linux, ensure that the folder has read and execute permissions set (e.g., `chmod 755`).
