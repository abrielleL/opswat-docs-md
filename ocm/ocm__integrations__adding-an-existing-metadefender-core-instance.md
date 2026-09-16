<!-- source: https://www.opswat.com/docs/ocm/integrations/adding-an-existing-metadefender-core-instance -->

# Adding an existing MetaDefender Core instance

The following guideline describes how to add an existing MetaDefender Core instance to OPSWAT Central Management.

1. Go to the **MetaDefender** **Core** management page under **Inventory** in the sidebar.

2. Click the **ADD CORE** button in the right top panel.

3. The dialog **Add Core** will be opened. Select the **Add an existing Core** button.

4. Fill the proper inputs. You can click the **TEST CONNECTION** button to check the connection status.

- **Name:** The name you want to assign to the new Core instance

- **API Key:** The API Key of the Core instance that should be used to authenticate the request

Warning

In order to access or modify the configuration or license settings of the instance, the chosen API Key should have the corresponding permission.

- **Server Address:** The address of the Core instance

5. The dialog will be closed and the Core page will be reloaded automatically if the result is successful.

Info

The status of the MetaDefender Core instance is **Connected** after the instance's version is fetched successfully.

Warning

While under management, MetaDefender Core instances will download module updates from OPSWAT Central Management by default. To ensure that this update process function properly, please verify that MetaDefender Core instances can properly connect to the OPSWAT Central Management server, such as any possible certificate issues that may require certificate import for the systems running the Core instances.

Please refer to [MetaDefender Core Module](/docs/ocm/integrations/metadefender-core-module) for more information.
