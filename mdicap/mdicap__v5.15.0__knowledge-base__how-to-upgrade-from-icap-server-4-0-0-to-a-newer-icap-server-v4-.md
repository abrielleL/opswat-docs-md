<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/how-to-upgrade-from-icap-server-4-0-0-to-a-newer-icap-server-v4- -->

# How to upgrade from ICAP Server 4.0.0 to a newer ICAP Server release?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender ICAP Server v4.0.0 release contains an issue that can cause configuration data loss during the upgrade.

Note

This issue applies to Windows deployments only.

On Linux, the upgrade can be performed on the traditional way, with no data loss.

To upgrade from v4.0.0, please perform the followings:

1. Stop the ICAP Server service using the following command:

net stop mdicapsrv

2. Check the data folder under MetaDefender ICAP Server installation folder (*<INSTALLATION DIRECTORY>\data*, usually C:\Program Files\OPSWAT\MetaDefender ICAP Server\data). If there is any *.war or *.shm files that exist in this folder, it means that the services are still running. Please be sure to stop the services correctly (no mdicapsrv.exe process is running)
3. **Copy** the content of your *<*INSTALLATION* DIRECTORY>\data* folder from the installation folder to a safe place.
4. Uninstall MetaDefender ICAP Server v4.0.0.
5. Remove content of *<*INSTALLATION* DIRECTORY>\data* folder.
6. Install the latest version of the MetaDefender ICAP Server.
7. Stop the ICAP Server service again using the following command:

net stop mdicapsrv

8. **Replace** the data folder with the files from **Step 3** to *<*INSTALLATION* DIRECTORY>\data* (keeping your data backup untouched).
9. Run the following command: *<INSTALLATION DIRECTORY>\mdicapsrv-upgrade-db.exe.*
10. Restart the ICAP Server service using the following command:

net start mdicapsrv

11. Login to the web management interface and check if your configuration and scan history is untouched.

Support:

If you need any further help to upgrade from this version, we encourage you to contact [OPSWAT support](https://my.opswat.com/portal/support) for assistance.
