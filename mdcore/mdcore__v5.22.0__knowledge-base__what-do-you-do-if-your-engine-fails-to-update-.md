<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/what-do-you-do-if-your-engine-fails-to-update- -->

# What do you do if your engine fails to update?

This article applies to all MetaDefender Core V4 and V5releases deployed on Windows and Linux systems.

If the engine in your OPSWAT MetaDefender Core fails to update and you are unsure of the product version, you can follow these steps:

1. **Check Update Configuration**:

   - Ensure that the update configuration is set correctly. Updates can be configured to **Internet** (Automatic), **Local** (Automatic), or **Manual**. For more details, refer to the [Engines Update Configuration](/docs/mdcore/v5.22.0/configuration/engines-update-configuration).
2. **Use Update Downloader**:

   - If your MetaDefender Core server is deployed offline, you will need to use the **MetaDefender Update Downloader** utility to download the engine updates definition updates.
   - Navigate to [**Product Downloads**](https://my.opswat.com/product-downloads) in My OPSWAT > select MetaDefender Core > locate the **Modules & Utilities** section > download the **Update Downloader**.
   - After downloading, configure the update downloader to fetch updates and apply them to the offline MetaDefender Core system. For more information, follow the instructions in the [Update Downloader server configuration file](https://www.opswat.com/docs/mddownloader/configuration/update-downloader-server-configuration-file).
3. **Apply Updates Manually**:

   - Upload the update packages through the MetaDefender Core **Management Console**, follow the instructions in the [Engines Update Configuration](/docs/mdcore/v5.22.0/configuration/engines-update-configuration).
4. **Verify Internet Connectivity**:

   - if not using MD Core in air-gap or offline mode, ensure that the server has proper internet connectivity to access the update servers. Allow access to `https://update.dl.opswat.com` for fetching engine/database updates.
5. **Upgrade to the Latest Version**:

   - If the issue persists, consider upgrading to the latest version of MetaDefender Core. Visit [**My OPSWAT**](https://my.opswat.com/home) to download the latest version. Upgrading ensures you benefit from the latest features and bug fixes.

These steps should help resolve the issue with engine updates in MetaDefender Core.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
