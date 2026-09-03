<!-- source: https://www.opswat.com/docs/mdcore/proactive-dlp/supported-engines-metadata-json -->

# Supported engines-metadata JSON

## [Overwrite file encoding detection](/docs/mdcore/proactive-dlp/supported-engines-metadata-json#overwrite-file-encoding-detection)

The Proactive DLP engine has the capability to detect file encoding and process the content with that encoding. However, by nature, it is not 100% accuracy with file encoding detection. In several cases, the clients determine exactly the encoding of the file, so they can send this information to the engine to have a better detection. To utilize this feature, please see the bellow steps:

1. Use [MetaDefender Core API](https://docs.opswat.com/mdcore/metadefender-core/ref#fileanalysispost) to send a file
2. Use the **engines-metadata** to send the encoding

JSONCopy{
"proactive_dlp": {
"charset": "ISO-2022-JP"
}
}

The engine uses UTF-8 as default encoding if the header is not set
