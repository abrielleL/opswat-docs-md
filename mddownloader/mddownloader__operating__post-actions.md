<!-- source: https://www.opswat.com/docs/mddownloader/operating/post-actions -->

# Post Actions

This feature is only available since Update Downloader 2.5.0

We do not recommend to create post action and assign it to a product when:

- Update Downloader shares an export folder with any MetaDefender Core, and
- In Update Settings of that MetaDefender Core, the setting DELETE FILES AFTER IMPORT is enabled.

Reason: the packages in shared folder might be removed by MetaDefender Core first before the post action takes action on those packages.

Pre-defined post actions to be auto triggered whenever a downloaded engine, or its database, turns to ready state to deliver to your all associated offline MetaDefender product(s).

This feature setting can be found under **Inventory menu → Post Actions**

- Hit **ADD NEW POST ACTION** to add a new one

Info

- One post action could be assigned to one or multiple created product(s) - Check [4.2.2 Products](/docs/mddownloader/operating/inventory-management/products) to learn how to create a product on Update Downloader
- One created product can have one or multiple post action(s) assigned to run
### [Windows](/docs/mddownloader/operating/post-actions#windows)

Example action: `c:\Python3\python.exe c:\myscript\pa.py`

### [Linux](/docs/mddownloader/operating/post-actions#linux)

Example action: `/usr/bin/python2 /home/opswat/test.py

- Hit **ADD** button to finish.

## [Integration instruction](/docs/mddownloader/operating/post-actions#integration-instruction)

STD input for your integrated script to consume and process:

JsonCopy{
"content_type": "[string] <engine / database>",
"location": "[string] full folder path where .zip and .yml created",
"generated_end_time": "[string] EPOCH datetime when both .zip and .yml are built done 100%",
"package": {
"display_name": "[string] file name of .zip",
"file_size": "[integer] ORIGINAL file size of .zip",
"file_hash": "[string] ORIGINAL SHA256 hash of .zip"
},
"package_metadescriptor": {
"display_name": "[string] file name of associated .yml",
"file_size": "[integer] ACTUAL file size of associated .yml",
"file_hash": "[string] ACTUAL SHA256 hash of associated .yml",
"content": "[string] full content of .yml file which must be converted to JSON format"
}
}

ORIGINAL file size and hash of .zip file are defined in the master .yml file "\data\updates\metadescriptor".

For example:
