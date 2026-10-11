<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/utilities-engines/supported-engines-metadata-header -->

# Supported engines-metadata header

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Decode and encode children file names with Shift-JIS encoding](/docs/mdcore/v5.22.1/utilities-engines/supported-engines-metadata-header#decode-and-encode-children-file-names-with-shift-jis-encoding)

The archive engine uses UTF-8 as a default encoding to create the children file names, if an archive file uses Shift-JIS encoding, please specify this info in the engine-metadata to preserve file names

1. Use [MetaDefender Core API](https://docs.opswat.com/mdcore/metadefender-core/ref) to process a file
2. Send the **engines-metadata** header with this value

JsonCopy{
"extraction": { "charset": "SJIS" },
"compression": { "charset": "SJIS" }
}
