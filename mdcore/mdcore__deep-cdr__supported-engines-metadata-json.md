<!-- source: https://www.opswat.com/docs/mdcore/deep-cdr/supported-engines-metadata-json -->

# Supported engines-metadata JSON

## [Overwrite file encoding for TXT and HTML](/docs/mdcore/deep-cdr/supported-engines-metadata-json#overwrite-file-encoding-for-txt-and-html)

The Deep CDR engine processes the TXT and HTML file as UTF-8 encoding by default. In several cases, the clients determine exactly the encoding of the file, so they can send this information to the engine to have a better detection. To utilize this feature, please see the bellow steps:

1. Use [MetaDefender Core API](https://docs.opswat.com/mdcore/metadefender-core/ref#fileanalysispost) to send a file
2. Use the **engines-metadata** to send the encoding

JsonCopy{
"deep_cdr": {
"charset": "ISO-2022-JP"
}
}
## [Select schema file to validate for XML](/docs/mdcore/deep-cdr/supported-engines-metadata-json#select-schema-file-to-validate-for-xml)

See the details [here](https://www.opswat.com/docs/mdcore/deep-cdr/validate-xml-files-against-an-xsd-schema).

JsonCopy{
"deep_cdr": {
"xml2xml.validate_against_schema.schema_name": "person.xsd"
}
}
