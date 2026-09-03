<!-- source: https://www.opswat.com/docs/mdcore/configuration/what-happens-when-you-change-data-directory- -->

# What happens when you change data_directory?

- If you update the `data_directory` registry value to a new location and restart MD Core, the application will create a **new, fresh data folder** at the specified path.
- **A new database and empty folders** for Quarantine and Sanitize, etc will be created in the new location. The UI will show the Welcome screen, and you must go through the initial setup process as if it’s a fresh installation.
- **Existing data (credentials, processing history, configuration, etc.) from the old data folder will not be available** in the new location unless you manually migrate the data.

In case, you want to completely move all the installation folder and files to another location (drive), please check this documentation: [How to relocate installation folder in MetaDefender Core on Windows?](/docs/mdcore/knowledge-base/how-to-relocate-installation-folder-in-metadefender-core-on-wind)
