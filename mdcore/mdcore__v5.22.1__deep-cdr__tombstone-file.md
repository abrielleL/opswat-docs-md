<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/deep-cdr/tombstone-file -->

# Tombstone file

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Since MetaDefender Core 4.19.1, whenever any child file in original archive file are not sanitized successfully, the product supports to append **tombstone file** into sanitized archive file to indicate which original child file(s) are removed from sanitized archive output file with details.

Each tombstone file will be auto created and placed at the same location as removed original child file(s) with following file name and content format:

File name format: `<original child file name>.tombstone.txt`

JsonCopy{
"data_id":"<data id of original child file scan result processed by MetaDefender Core>",
"file_info": {
"sha256": "<SHA256 hash of original child file>"
},
"process_info": {
"blocked_reason": "<blocked reason to indicate why original child file was not sanitized successfully>"
}
}Info

Please note that the tombstone functionality for the PST file type is supported starting from Core version 5.13.0, in combination with Archive Compression engine version 7.3.0.

A setting called “ADD TOMBSTONE FILE DURING ARCHIVE SANITIZATION” is required to be enabled (disabled by default) under each desired workflow rule to make this feature triggered:

For example:

Original archive file content:

Downloading archived sanitization file and check its content:

whereas a tombstone file called `infected.txt.tombstone.txt`

JsonCopy{
"data_id": 66aab3e361e04df7a78206e6ae5ceb15,
"file_info": {
"sha256" : 275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f
},
"process_info": {
"blocked_reason" : Infected
}
}
