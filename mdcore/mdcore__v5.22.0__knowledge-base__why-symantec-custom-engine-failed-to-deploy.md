<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-symantec-custom-engine-failed-to-deploy -->

# Why has the Symantec custom engine failed to deploy?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows systems.

To install and deploy MetaDefender Core’s Symantec custom engine, certain **Registry Keys** need to be present in the registry.

If these keys do not exist, the Symantec engine installation process will time out.

**To install the Symantec custom engine in MetaDefender Core, you can manually add the missing registry keys by completing the following steps:**

Please Note:

Registry key names and values are case-sensitive.

1. Open the Windows registry (**regedit.exe**)
2. Navigate to **HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters**
3. Create a new **Value Name** with the type **Multi-String Value** and the name: **NullSessionPipes**
4. **Save** the changes
5. Remove the Symantec engine from your MetaDefender Core system
6. **Uninstall** the Symantec Protection Engine manually from Windows
7. Navigate to the location where the Symantec engine is located (**Program Files\Symantec**) and **Delete** this folder manually
8. Click **Update all** in the **Modules** page to reinstall the engine.

Support:

If you have followed the instructions above but are still experiencing a Symantec installation **timeout**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
