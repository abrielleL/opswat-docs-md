<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/utilities-engines/file-info-details -->

# Block files based on file info details

#### [Configure to return file info details](/docs/mdcore/v5.21.0/utilities-engines/file-info-details#configure-to-return-file-info-details)

Beside the basic file info such as true file type format, the file type also provides advance file details, to enable this feature, follow these steps:

- At **Inventory > Modules > Utilities > FileType**, Tick **Enable Exif module**

- At **Workflow Management > Workflows > [Workflow name] > File Type > General**, Enable **Include file details > Metadata**

JSON output:

JsonCopy"filetype_info": {
...
"file_metadata": {
"BitDepth": "8",
"ColorType": "RGB with Alpha",
"Compression": "Deflate/Inflate",
"FileAccessDate": "2023:01:10 10:58:17-08:00",
"FileCreateDate": "2023:01:10 10:58:17-08:00",
"FileModifyDate": "2023:01:10 10:58:17-08:00",
"FilePermissions": "-rw-rw-rw-",
"Filter": "Adaptive",
"Gamma": "2.2000000000000002",
"ImageHeight": "598",
"ImageSize": "1405x598",
"ImageWidth": "1405",
"Interlace": "Noninterlaced",
"Megapixels": "0.83999999999999997",
"PixelUnits": "meters",
"PixelsPerUnitX": "5669",
"PixelsPerUnitY": "5669",
"SRGBRendering": "Perceptual"
},
..
}

The feature is in BETA, please use the data for information only. The JSON structure and attribute names can be changed without notice.

#### [Configure to block files based on file details](/docs/mdcore/v5.21.0/utilities-engines/file-info-details#configure-to-block-files-based-on-file-details)

The file type engine allows you to block a file based on its file info details.

`JSON Path`: Specifies the path to the attribute in the JSON. See the "filetype_info" section in the exported JSON, currently supports the paths under "file_info_details" and "file_metadata".

*Example:* `$.file_metadata.producer`

`Value pattern`: Defines the pattern to match against the attribute value. Supports regular expressions.

*Example:* `GemBox.*?`
