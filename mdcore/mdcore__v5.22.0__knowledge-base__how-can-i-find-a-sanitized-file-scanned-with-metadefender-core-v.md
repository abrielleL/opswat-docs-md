<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-can-i-find-a-sanitized-file-scanned-with-metadefender-core-v -->

# How can I find a sanitized file scanned with MetaDefender Core v5?

This article applies to all MetaDefender Core V5 releases deployed on Windows and Linux systems.

Once a file is scanned by MetaDefender Core and then sanitized, it can be downloaded from the following link:

URLCopyhttp://<MetaDefender>:8008/file/converted/<dataid>?apikey=<apikeyset>

- <MetaDefender> needs to be set to your MetaDefender I.P. location or name
- <dataid> needs to be inserted as per data-id of the file
- <apikey> Only required if REST API keys have been defined

Support:

If **Further Assistance** is required then please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
