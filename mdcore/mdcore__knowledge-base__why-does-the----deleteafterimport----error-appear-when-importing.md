<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-the----deleteafterimport----error-appear-when-importing -->

# Why does the “deleteafterimport” error appear when importing an MD Core configuration from standalone mode to shared database mode?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

**Issue:** An error message, **“deleteafterimport”**, appears when a user imports an MD Core configuration from a standalone database mode instance to an MD Core instance using shared database mode.

**Note:** Officially, importing configurations between standalone and shared database modes is **not supported** due to potential differences in configuration settings. Some configurations may exist only in standalone mode but not in shared DB mode, and vice versa. Additionally, the use cases for these modes differ, making configuration discrepancies expected.

**Cause:**

The `deleteafterimport` configuration is not valid for **Shared Database Mode**. This option specifies that once **MD Core** completes updating the package from the configured folder, it will automatically delete the files in that folder. However, this behavior is not supported in **Shared Database Mode** due to its centralized data management structure.

But in shared db mode → we can have multiple MD Core point to the same location (shared folder/network) → this option is always disabled in shareddb, because if not → it will delete all files → other MD Core cannot have the files → failed to updates.

**Temporary solution:**

- Open the **settings_export.json** file located in the exported ZIP file.
- Modify the specified field “**deleteafterimport**” from **true** to **false**.
- Recompress the files into a ZIP archive.
- Import the updated ZIP file to MD Core.

- Ensure that the configuration is imported successfully.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
