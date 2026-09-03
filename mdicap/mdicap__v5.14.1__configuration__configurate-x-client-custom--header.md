<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/configuration/configurate-x-client-custom--header -->

# Custom ICAP Request Header

ICAP client is supported to send designated **custom encapsulated HTTP** **header(s)** (**not ICAP headers**) to MetaDefender ICAP server for its request tracking purpose.

Those custom headers with values will be tied to each ICAP request, and written on MetaDefender ICAP server log, as well as audited in MetaDefender Core backend server's corresponding JSON processing details in the `metadata` field.

That expects to help keep track of distinguished details tailored to every ICAP request sent to MetaDefender e.g. application source identifier.

## [How it works](/docs/mdicap/v5.14.1/configuration/configurate-x-client-custom--header#how-it-works)

This feature is not enabled by default

To enable that, changing relevant setting `enable_x_client_custom_parser` in MetaDefender ICAP server configuration is required. See details at [Configuration file](/docs/mdicap/v5.14.1/configuration/configuration-file)

Once enabled, ICAP client is supported to send `X-Client-Custom-xxxxxx` header(s) in encapsulated HTTP message for every ICAP request, whereas `xxxxxx` is at ICAP client's choice.

**For example:**

- `X-Client-Custom-SourceID` = `abc`
- `X-Client-Custom-RequestID` = `def`

In case of duplicated header name, then only one header (the first found valid one) is captured.

By default:

- Maximum number of custom headers is supported is 16.
- Maximum length (in bytes) of each custom header name (excluding `X-Client-Custom-` prefix) is 128.
- Maximum length (in bytes) of each custom header value is 128.

To adjust the limit, changing relevant settings max_number_x_client_custom and max_header_length_x_ client_custom in MetaDefender ICAP server configuration is required. See details at [Configuration file](/docs/mdicap/v5.14.1/configuration/configuration-file)

If the limit is exceeded, then expecting to hit "Bad request" response from MetaDefender ICAP server.

MetaDefender ICAP server will parse those custom request header and do following:

- Put altogether into metadata field (JSON format).
- Write that field into MetaDefender ICAP server log after the ICAP request is accepted (requestId is created) and begin to process further

`[INFO ] 2022.04.26 16:37:55.128: (icap.scanner) Attempting to scan, connectionId='5b5cc3f32a13497d9427657cc3223204',`**requestId='1e5f26129f554a0ea0378e64d35c39cd'**`, host='', url='`[www.test.com/test.txt](http://www.test.vn/abc.txt)`', clientAddress='1.1.1.1', coreAddress='`[',](http://10.40.50.189:80',/)`coreRule='File process', enabledLocalScan='false', enabledWebHook='false',`**metadata='{"SourceID":"abc","RequestID":"def"}'**`[msgid: 3680]`

- Submit a scan request to MetaDefender Core backend with entire metadata field.
- After the scan is finished on MetaDefender Core, expecting to see that metadata field is appended to that JSON scan details.

JsonCopy{
"data_id": "224296917dd44665a8a2aa347f05e989",
"dlp_info": {},
"extraction_info": {},
"file_info": {
"display_name": "test.txt",
"file_size": 10,
"file_type": "text/plain",
"file_type_description": "ASCII Text",
...
},
"metadata": {
"RequestID": "def",
"SourceID": "abc"
},
....Warning

By default, the custom header will not be absorbed

Set flag "*notify_modified_custom_header*" to **true** to absorb these headers out of HTTP header or ICAP header (See details at [Configuration file](/docs/mdicap/v5.14.1/configuration/configuration-file))
