<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/what-are-the-engine-clean-up-instructions -->

# What are the engine clean-up instructions?

This tool only works on MetaDefender Core **4.18.0 and older**.
For Metadefender Core **4.19.0+**, please use the instructions found here: [Engine Clean-up Tool](/docs/mdcore/v5.22.0/troubleshooting/engine-clean-up-tool)

For MetaDefender Core 4.19.2 or newer, all engines could be removed directly on the MetaDefender Core management console UI under Modules page or you can consult this article : [How to Remove Engines from MetaDefender Core using command line?](/docs/mdcore/v5.22.0/knowledge-base/how-to-remove-engines-from-metadefender-core-using-command-line-)

Sometimes, during the engines downloading/deployment process, some of them may remain in **"failed"** or **"permanently failed"** status. In this case, you can perform an engine clean-up by downloading the [engine_sweeper tool](https://kb-hosting-cs.s3.amazonaws.com/KB/Core4/engine_sweeper.zip) and following the next steps:

1. Extract the engine_sweeper.zip package to a temporary location on the server where MetaDefender Core is installed
2. Open a Command Prompt window **as Administrator** and navigate to the temporary folder where you have extracted the archive
3. Run the command **ometascan-engine-sweeper.exe -l** to display a list of all installed engines

4. Run the command **ometascan-engine-sweeper.exe -e <engine name from above> -c** to clean the engine having the issues

**Note**: During the cleanup process, the MetaDefender Core and Node services will be **restarted**, and the Updates Settings Source will be set to "**Manual**"

5. Check the engine in Inventory > Modules as it should now be grey. (e.g. Deep CDR in the following screenshot)

6. Revert your Updates Settings Source from "Manual" to your previous setting and trigger an update, for the engine to re-deploy successfully
7. More parameters that can be used with this tool can be found in the next screenshot

Support:

If you have followed all of these steps and your engines are still unusable, please see [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), then please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
