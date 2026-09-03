<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/what-do-i-do-if-my-modules-disappear-from-the-core-ui- -->

# What do I do if my modules disappear from the Core UI?

If you are noticing that module(s) are missing from the Core UI there are a few different things that you can check prior to submitting a support ticket:

1. **MetaDefender Core Cannot Reach the Update Server:** The update server for MetaDefender Core is [https://update.dl.opswat.com](https://update.dl.opswat.com/), which is used for fetching engine and database updates. To ensure that MetaDefender Core can reach the Update Server, please review the following troubleshooting steps below:

   1. **Check Internet Connection**: Verify that the MetaDefender Core server has a stable internet connection. This is necessary for connecting to the update server.
   2. **Allowlist Required URLs**: Make sure the following URLs are accessible from your environment:

      - [**https://activation.dl.opswat.com**](https://activation.dl.opswat.com/) (for license activation)
      - [**https://update.dl.opswat.com**](https://update.dl.opswat.com/) (for engine and database updates)
   3. **Firewall Configuration**: Verify that the firewall is not blocking the required URLs or ports. If the server is in a restricted environment, configure the proxy settings in MetaDefender Core to allow access to the update and activation servers.
   4. **Offline Updates**: If the server is offline, you can use the **MetaDefender Update Downloader** utility to download updates on a system with internet access and then transfer them to the offline server. The utility can be downloaded from [**My OPSWAT Portal**](https://my.opswat.com/product-downloads) under Produt Downloads > click on **MetaDefender Core** > under **Modules & Utilities** click on **Update Downloader for Offline Environment**
   5. **Check System Notifications**: Verify if there are any notifications in the MetaDefender Core interface indicating issues such as disk space or memory availability, as these can also affect updates.
2. **Restart the Services:** Sometimes, restarting the MetaDefender Core services can resolve issues with missing modules. Restart the services through operating system’s services manager or by using the command line.
3. **Clear Browser Cache**: If you are accessing the MetaDefender Core user interface through a web browser, clear your browser cache and refresh the page. Cached data can sometimes cause display issues.
4. **Reinstall MetaDefender Core**: If the above steps do not resolve the issue, consider reinstalling MetaDefender Core. Ensure you have back up of your configuration and data before proceeding with a reinstallation.

   1. Have a backup version (snapshot, recovery point,…)
   2. Import/Export your configuration settings.
   3. Export processing history as needed.

**Contact OPSWAT Support:**

If the problem persists, reach out to OPSWAT support for further assistance. In the ticket please provide the following details:

- Details about your environment
- The version of MetaDefender Core you are running
- Details about any specific errors you are receiving and relevant screenshots
- Support Package. This will allow us to check logs and check for any specific errors. Please review our documentations on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.21.0/troubleshooting/how-to-create-support-package-)
- License key. This will allow us to confirm and verfiy which modules should be available to you based on the purchased package.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
