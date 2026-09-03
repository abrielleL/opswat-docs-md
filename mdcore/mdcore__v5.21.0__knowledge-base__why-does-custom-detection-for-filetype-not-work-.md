<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-does-custom-detection-for-filetype-not-work- -->

# Why does custom detection for FileType not work?

 **Check Your Version:** This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

The custom detection is only supported from File Type version 7.4 and later

### [**Issue**](/docs/mdcore/v5.21.0/knowledge-base/why-does-custom-detection-for-filetype-not-work-#issue)

Custom detection for a filetype is enabled, but the file is still detected as Unknown (Data).

### [**Possible causes and solutions**](/docs/mdcore/v5.21.0/knowledge-base/why-does-custom-detection-for-filetype-not-work-#possible-causes-and-solutions)

1. **Incorrect path to the custom XML rule file**
   Verify that the path to your custom rule is correct at **Inventory > Modules > Utilities > FileType**, section **Enable custom detection**
2. **Settings not saved**
   After enabling custom detection and adding rule(s), ensure you click **Save** in the MetaDefender Core UI.
3. **Filetype engine not restarted**
   Restart the FileType engine for changes to take effect. You can do this by disabling and then re-enabling the FileType engine in the UI.
4. **Invalid or incorrect custom rule**
   Review your XML rule file to confirm that the syntax and matching criteria are correct. Check these documents for more details.

   1. [Custom detection - MetaDefender Core](https://www.opswat.com/docs/mdcore/utilities-engines/custom-detection)
   2. [How to add custom detection for a file type? - MetaDefender Core](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-add-custom-detection-for-a-file-type)
5. **Built-in rule taking priority**

   - A file may match both a custom rule and a built-in FileType rule
   - To ensure the custom rule is used, assign it a high confidence score. Please see more details at [Custom detection - MetaDefender Core](https://www.opswat.com/docs/mdcore/utilities-engines/custom-detection#custom-rules)

     - The “detection score” can be found in the JSON scan result: `filetype_info.file_info.likely_type_ids.score`

**Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
