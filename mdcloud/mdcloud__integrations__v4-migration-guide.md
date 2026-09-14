<!-- source: https://www.opswat.com/docs/mdcloud/integrations/v4-migration-guide -->

# V4 Migration Guide

The following table shows the difference in headers between the API versions for the file upload:

| Header | Used for | V3 | V4 |
| --- | --- | --- | --- |
| Authentication header (see [API Authentication Mechanisms](/docs/mdcloud/integrations/api-authentication-mechanisms) for details) | General | Authorization | apikey |
| Filename header | File upload | x-filename | filename |
| Scan workflow selection | File upload | x-rule | rule |
| Archive password | File upload | x-archive-password | archivepwd |
| Private scanning | File upload | x-sample-sharing | samplesharing |
| Scan URL | File upload | x-download-form | downloadform |
| Bulk hash scan details | Bulk hash lookup | x-include-scan-details | includescandetails |
| Include additional hash details | Hash lookup | x-file-metadata |  |

### [Hash Lookup Changes](/docs/mdcloud/integrations/v4-migration-guide#hash-lookup-changes)

The hash lookup endpoint would return additional information like PEInfo and EXIF when the "file_metadata" header was passed. In V4 this header was deprecated in favor of the "additional_ info" key in the JSON body response which specifies exactly what additional info the file API can return. To see more information about this header go to [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Retrieving scan reports using a data hash).

### [File Scan Changes](/docs/mdcloud/integrations/v4-migration-guide#file-scan-changes)

The rule header (see [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Analyze file) for more details) used to be a fixed string which specifies what operation to perform on the file. Now the rule header can accept multiple values, separated by commas:

| Header | Operation Performed |
| --- | --- |
| multiscan | Multiscanning (default, always performed) |
| sanitize | Perform data sanitization |
| cdr | Sanitization **without** multiscanning |
| unarchive | Multiscanning and unarchiving of the file |

The headers can be sent in any combination separated by commas. This allows for future operations to be added in a seamless way, and for clients to easily control operations performed on the file.

Also, the file upload will now return an error if the content type is not one of the supported formats. See [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Analyze file) for details.

### [Sanitization Change](/docs/mdcloud/integrations/v4-migration-guide#sanitization-change)

The old endpoint for downloading the sanitized version of the file: **/v4/file/:fileId/sanitizedLink**

The new endpoint for downloading the sanitized version of the file starting with v4: **/v4/file/converted/:data_id/**

This was changed to match the MetaDefender API url.

### [IP Scanning Changes](/docs/mdcloud/integrations/v4-migration-guide#ip-scanning-changes)

The response format of IP scanning has changed:

Old format

JavascriptCopy{
"address": "1.1.1.1",
"start_time": "2019-03-11T09:50:58.645Z",
"detected_by": 0,
"scan_results": [
{
"source": "reputation.alienvault.com",
"results": [
{
"alternativeid": "",
"assessment": "",
"confident": "",
"detecttime": "",
"updatetime": "2019-03-11T09:50:58.707Z",
"result": "unknown"
}
]
},
{
"source": "danger.rulez.sk",
"results": [
{
"alternativeid": "",
"assessment": "",
"confident": "",
"detecttime": "",
"updatetime": "2019-03-11T09:50:58.707Z",
"result": "unknown"
}
]
},
{
"source": "feodotracker.abuse.ch",
"results": [
{
"alternativeid": "",
"assessment": "",
"confident": "",
"detecttime": "",
"updatetime": "2019-03-11T09:50:58.707Z",
"result": "unknown"
}
]
},
{
"source": "malc0de.com",
"results": [
{
"alternativeid": "",
"assessment": "",
"confident": "",
"detecttime": "",
"updatetime": "2019-03-11T09:50:58.707Z",
"result": "unknown"
}
]
},
{
"source": "malwaredomainlist.com",
"results": [
{
"alternativeid": "",
"assessment": "",
"confident": "",
"detecttime": "",
"updatetime": "2019-03-11T09:50:58.707Z",
"result": "unknown"
}
]
},
{
"source": "phishtank.com",
"results": [
{
"alternativeid": "",
"assessment": "",
"confident": "",
"detecttime": "",
"updatetime": "2019-03-11T09:50:58.707Z",
"result": "unknown"
}
]
},
{
"source": "spamhaus.org",
"results": [
{
"alternativeid": "",
"assessment": "",
"confident": "",
"detecttime": "",
"updatetime": "2019-03-11T09:50:58.707Z",
"result": "unknown"
}
]
},
{
"source": "zeustracker.abuse.ch",
"results": [
{
"alternativeid": "",
"assessment": "",
"confident": "",
"detecttime": "",
"updatetime": "2019-03-11T09:50:58.707Z",
"result": "unknown"
}
]
}
],
"geo_info": {
"ip": "1.1.1.1",
"country_name": "Australia",
"country_code": "AU",
"region_name": "",
"region_code": "",
"city": "",
"latitude": -27,
"longitude": 133
}
}

New format

*Note that in addition to the new format, the "confident" field has also been removed.*

JavascriptCopy{
"address": "101.200.81.187",
"lookup_results": {
"start_time": "2019-03-11T09:30:37.094Z",
"detected_by": 1,
"sources": [
{
"provider": "zeustracker.abuse.ch",
"assessment": "botnet, zeus",
"detect_time": "2019-03-08T09:33:58.303966Z",
"update_time": "2019-03-08T09:33:58.560775",
"status": 3
},
{
"provider": "reputation.alienvault.com",
"assessment": "",
"detect_time": "",
"update_time": "2019-03-11T09:30:37.146Z",
"status": 0
},
{
"provider": "danger.rulez.sk",
"assessment": "",
"detect_time": "",
"update_time": "2019-03-11T09:30:37.146Z",
"status": 0
},
{
"provider": "feodotracker.abuse.ch",
"assessment": "",
"detect_time": "",
"update_time": "2019-03-11T09:30:37.146Z",
"status": 0
},
{
"provider": "malc0de.com",
"assessment": "",
"detect_time": "",
"update_time": "2019-03-11T09:30:37.146Z",
"status": 0
},
{
"provider": "malwaredomainlist.com",
"assessment": "",
"detect_time": "",
"update_time": "2019-03-11T09:30:37.146Z",
"status": 0
},
{
"provider": "phishtank.com",
"assessment": "",
"detect_time": "",
"update_time": "2019-03-11T09:30:37.146Z",
"status": 0
},
{
"provider": "spamhaus.org",
"assessment": "",
"detect_time": "",
"update_time": "2019-03-11T09:30:37.146Z",
"status": 0
}
]
},
"geo_info": {
"continent": {
"code": "AS",
"name": "Asia"
},
"country": {
"code": "CN",
"name": "China"
},
"city": {
"code": "",
"name": "Hangzhou"
},
"location": {
"latitude": 30.2936,
"longitude": 120.1614
},
"registered_country": {
"code": "CN",
"name": "China"
},
"subdivisions": [
{
"code": "33",
"name": "Zhejiang Sheng"
}
]
}
}
### [Other Changes](/docs/mdcloud/integrations/v4-migration-guide#other-changes)

V3 response included a "success" key in the JSON, and the rest of the response was in the "data" key. Now both of these keys have been removed and the response contains the content from the "data" key.
