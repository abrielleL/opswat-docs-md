<!-- source: https://www.opswat.com/docs/mdcloud/integrations/errors -->

# Errors

## [Error response example](/docs/mdcloud/integrations/errors#error-response-example)

BashCopy{
error: {
code: 400022,
messages: [
"ValidatorError :: Path `data.file_info.loaded_components` is invalid (a)."
]
}
}
## [Error Codes Explained](/docs/mdcloud/integrations/errors#error-codes-explained)

| **Group** | **Error code** | **Description** | **HTTP Code** |
| --- | --- | --- | --- |
| **HTTP errors :: 400** | 400000 | Generic Error | **400** |
|  |  |  |  |
| **Generic errors** | 400001 | The caching strategy is not recognized | **400** |
|  | 400002 | The limit strategy is not supported | **400** |
|  | 400003 | The limit type is not supported | **400** |
|  | 400004 | The query params are not valid | **400** |
|  | 400005 | The URL params are not valid | **400** |
|  | 400006 | Domain is not a valid origin. | **400** |
|  |  |  |  |
| **Payload** | 400020 | Header is not valid | **400** |
|  | 400021 | Payload is not valid | **400** |
|  | 400022 | Payload validation has failed | **400** |
|  | 400023 | Headers are not correct | **400** |
|  | 400024 | Headers are missing | **400** |
|  | 400025 | Payload is missing or empty | **400** |
|  | 400026 | Hash in the url doesn't match the hash value in the body | **400** |
|  | 400027 | Offset should be a positive integer | **400** |
|  | 400028 | Limit should be a positive integer less than 10000 | **400** |
|  | 400029 | Rescan is not available for sanitized files | **400** |
|  | 400030 | Rescan is not available | **400** |
|  | 400031 | Resource already exists | **400** |
|  |  |  |  |
| **Routing errors** | 400040 | The requested path is not valid | **400** |
|  | 400041 | The version is required | **400** |
|  | 400042 | The version does not exist | **400** |
|  | 400043 | The requested path does not exist | **400** |
|  | 400044 | Method does not exist | **400** |
|  | 400045 | The route was not properly setup | **400** |
|  | 400046 | The requested route does not exist | **400** |
|  | 400047 | This route is available only on development environments | **400** |
|  | 400048 | This route is deactivated | **400** |
|  |  |  |  |
| **Hash errors** | 400060 | The `hash` field in body is required | **400** |
|  | 400061 | The `hash` field is not an array | **400** |
|  | 400062 | The `hash` field is empty | **400** |
|  | 400063 | Exceeded maximum allowed | **400** |
|  | 400064 | The hash value is not valid | **400** |
|  | 400065 | The header has to be either 0 or 1. | **400** |
|  | 400066 | The header has to be either 0 or 1. | **400** |
|  | 400067 | Hash update failed | **400** |
|  |  |  |  |
| **Top hash URL errors** | 400080 | Limit must be positive | **400** |
|  | 400081 | Type must be one of `clean` / `infected` | **400** |
|  | 400082 | Period must be one of `day` / `week` / `month` | **400** |
|  | 400083 | Threshold must be one of 1, 2, 3, 4, 5, 6 | **400** |
|  |  |  |  |
| **App info** | 400100 | The field `device_info.os_info.device_identity` is required | **400** |
|  | 400101 | The fields `file_info.sha1`, `file_info.file_property.file_location`, `file_info.file_property.file_name` are required | **400** |
|  | 400102 | Failed to save appinfo. Please try again later. | **400** |
|  |  |  |  |
| **Top detection errors** | 400120 | The header `x-exclude-empty-file-id` has to be either 0 or 1 | **400** |
|  | 400121 | The header `x-exclude-data` has to be either 0 or 1 | **400** |
|  | 400122 | The header `x-threshold` must be one of 1, 2, 3, 4, 5, 6 | **400** |
|  | 400123 | Packages should be one of m1, m4, m8, m12, m16, m20, mmax, mcl, mem, isv | **400** |
|  | 400124 | Number of hashes must be one of 10, 100, 1000, 10000 | **400** |
|  |  |  |  |
| **Upload errors** | 400140 | The file upload has failed. | **400** |
|  | 400141 | The header has to be either 0 or 1. | **400** |
|  | 400142 | The header has to be either 0, 1 or 2. | **400** |
|  | 400143 | Private scanning not enabled for the provided API key. | **400** |
|  | 400144 | Exceeded maximum file size allowed. | **400** |
|  | 400145 | Request body is empty. Please send a binary file. | **400** |
|  | 400146 | Provided download url is not valid or inaccessible. | **400** |
|  | 400147 | Rescan Failed. Requested file is missing from our servers. | **400** |
|  | 400148 | Requested file is a private one and cannot be rescanned. | **400** |
|  | 400149 | Could not update the rescan count. | **400** |
|  | 400150 | The `file_ids` field array in body is required | **400** |
|  | 400151 | The `file_ids` field is not an array | **400** |
|  | 400152 | The `file_ids` field is empty | **400** |
|  | 400153 | Exceeded maximum allowed | **400** |
|  | 400154 | Exceeded maximum allowed files in archive | **400** |
|  | 400155 | Redirect urls are not supported | **400** |
|  | 400156 | Workflow rule not available for your account | **400** |
|  |  |  |  |
| **API key** | 400160 | The apikey you are trying to add already exists | **400** |
|  | 400161 | The apikey could not be removed | **400** |
|  | 400162 | The apikey was not updated | **400** |
|  | 400163 | The body is invalid | **400** |
|  | 400164 | Please choose another nickname, as this one is too long | **400** |
|  | 400165 | No apikey specified | **400** |
|  | 400166 | Please provide a valid email address | **400** |
|  | 400167 | Please provide a valid body | **400** |
|  | 400168 | Please choose another nickname, as this one contains profanities | **400** |
|  | 400169 | File type not allowed for vulnerability submission | **400** |
|  |  |  |  |
| **User reputation** | 400170 | The user's reputation could not be updated | **400** |
|  |  |  |  |
| **IP-Domain errors** | 400180 | Invalid format of the input. Provide IPv4 or IPv6 | **400** |
|  | 400181 | The `address` field in the body is required | **400** |
|  | 400182 | The `address` field is not an array | **400** |
|  | 400183 | The `address` field is empty | **400** |
|  | 400184 | Exceeded maximum allowed | **400** |
|  | 400185 | The address is a not a routable IP | **400** |
|  | 400186 | No response | **400** |
|  |  |  |  |
| **Stats** | 400200 | The number of days requested must be a positive integer | **400** |
|  | 400201 | Invalid objectId | **400** |
|  | 400202 | Invalid date | **400** |
|  | 400203 | Invalid outbreak report filter | **400** |
|  |  |  |  |
| **Status** | 400210 | Param type must be one of `prevention_api` / `reputation_api` / `feed_api` | **400** |
|  |  |  |  |
| **Coupons** | 400220 | Code not found | **400** |
|  | 400221 | Code is inactive | **400** |
|  | 400222 | This promotion has ended | **400** |
|  | 400223 | Coupon update failed | **400** |
|  | 400224 | Coupon already used | **400** |
|  | 400225 | User already has an active coupon | **400** |
|  | 400226 | Can not activate a coupon on a paid apikey | **400** |
|  |  |  |  |
| **Repo** | 400240 | Invalid `source` value | **400** |
|  | 400241 | Invalid repository | **400** |
|  |  |  |  |
| **Salesforce** | 400250 | Salesforce connectivity error | **400** |
|  | 400251 | There is no record | **400** |
|  |  |  |  |
| **Feed** | 400260 | You are allowed to query up to 30 days in the past | **400** |
|  | 400261 | Invalid category. Please use: A, D, E, G, M, N, O, P, T, Z | **400** |
|  |  |  |  |
| **Cognito** | 400262 | App client name not provided | **400** |
|  | 400263 | App client id not provided | **400** |
|  | 400264 | Maximum number of app clients reached | **400** |
|  | 400265 | App client could not be created | **400** |
|  | 400266 | No client ids associated with current customer | **400** |
|  | 400267 | Client id is not associated with current customer | **400** |
|  | 400268 | Information about current app client could not be retrieved | **400** |
|  | 400269 | App client could not be removed | **400** |
|  |  |  |  |
| **HTTP errors :: 401** | 401000 | Authentication has failed | **401** |
|  | 401001 | Authentication strategy is invalid | **401** |
|  | 401002 | Authentication strategy is not implemented | **401** |
|  | 401003 | Authorization strategy is not supported for this endpoint | **401** |
|  | 401004 | Authentication token has expired | **401** |
|  | 401005 | Authentication token is invalid | **401** |
|  | 401006 | Invalid API key | **401** |
|  | 401007 | You are not authorized | **401** |
|  | 401008 | You are not authorized to download this file | **401** |
|  |  |  |  |
| **HTTP errors :: 403** | 403000 | Access Forbidden | **403** |
|  | 403001 | Requested resource doesn't match your API key | **403** |
|  | 403002 | Your IP is blocked because of abuse and will be automatically unblocked in one hour. This is for preventing brute-force attacks. | **403** |
|  | 403003 | Insufficient privileges | **403** |
|  |  |  |  |
| **HTTP errors :: 404** | 404000 | Endpoint not found | **404** |
|  | 404001 | Entity was not found | **404** |
|  | 404002 | There are no entries found | **404** |
|  | 404003 | The hash was not found | **404** |
|  | 404004 | The data_id was not found | **404** |
|  | 404005 | The hash information was not found | **404** |
|  | 404006 | There is no data for selected date | **404** |
|  | 404007 | Requested file id does not exist in our records | **404** |
|  | 404008 | The apikey was not found | **404** |
|  | 404009 | Requested CVE does not exist in our records | **404** |
|  | 404010 | Unsupported file type | **404** |
|  | 404011 | This hash was scanned as a private file and we do not store the file | **404** |
|  | 404012 | File was archived | **404** |
|  | 404013 | This API version is no longer maintained. Please use V4 API <https://onlinehelp.opswat.com/mdcloud/6._V4_API.html> | **404** |
|  |  |  |  |
| **HTTP errors :: 406** | 406000 | Content-Type header & payload has to be json | **406** |
|  | 406001 | Payload data missing or error | **406** |
|  |  |  |  |
| **HTTP errors :: 408** | 408000 | Request timeout. It has reached the 60 seconds limit | **408** |
|  |  |  |  |
| **HTTP errors :: 429** | 429000 | Rate limit exceeded, retry after the limit is reset. | **429** |
|  | 429001 | Your request has been throttled, maximum requests per minute | **429** |
|  | 429002 | Too many connections, try again later | **429** |
|  |  |  |  |
| **HTTP errors :: 500** | 500000 | Scan request has failed permanently. | **500** |
|  | 500001 | Internal Server Error | **500** |
|  |  |  |  |
| **HTTP errors :: 503** | 503000 | External service is not reachable | **503** |
|  | 503001 | External service is not reachable | **503** |
|  | 503002 | Server is not accessible | **503** |
