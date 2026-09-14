<!-- source: https://www.opswat.com/docs/mdcloud/integrations/api-authentication-mechanisms -->

# API Authentication Mechanisms

MetaDefender Cloud APIs are protected by a Basic authentication mechanism.

*Basic authentication is a simple authentication scheme built into the HTTP protocol. The client sends HTTP requests with the Authorization header that contains the word Basic word followed by a space and a base64-encoded string username:password.*

All API users are required to include their apikey in the appropriate header when communicating with the public APIs. In order to obtain your apikey, follow the steps in our guide, [Onboarding Process for MetaDefender Cloud API Users](/docs/mdcloud/integrations/onboarding-process-for-metadefender-cloud-api-users).

## [Authentication Examples](/docs/mdcloud/integrations/api-authentication-mechanisms#authentication-examples)

MetaDefender Cloud v4 API uses the custom HTTP header **apikey.** Every request must send this header. Please see [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Analyze file) for more information on the apikey header.

## [Successful API Authentication Request](/docs/mdcloud/integrations/api-authentication-mechanisms#successful-api-authentication-request)

> curl -X POST https://api.metadefender.com/v4/file -H 'apikey: $YOUR_API_KEY' -H 'filename: file.zip' -d @file_name.txt
> POST /v4/file HTTP/1.1
> Host: api.metadefender.com
> User-Agent: curl/7.52.1
> Accept: */*
> apikey: YOUR_API_KEY
> filename: file.zip
> Content-Length: 1859
> Content-Type: application/x-www-form-urlencoded
> Expect: 100-continue
>
< HTTP/1.1 100 Continue
* We are completely uploaded and fine
< HTTP/1.1 200 OK
< Content-Type: application/json; charset=utf-8
< Date: Wed, 23 Aug 2017 18:47:45 GMT
< Vary: Accept-Encoding
< X-Authenticated: by apikey
< X-RateLimit-For: uploadFile
< X-RateLimit-Interval: 3600
< X-RateLimit-Limit: 100
< X-RateLimit-Remaining: 98
< X-RateLimit-Reset-In: 3294s
< X-RateLimit-Used: 1
< X-Response-Time: 123ms
< Content-Length: 122
< Connection: keep-alive
 
{
"data_id": "bzIwMDcyN3NEZGpiUUJyOGI4YVBndzMzaHBa",
"status": "inqueue",
"in_queue": 1,
"queue_priority": "normal",
"sha1": "68686873C9252995D1C805946D8D5304E6BC2BD2",
"sha256": "CF8DE586219B9CE7893846967A6219EAAA385F3C62290B771CFD15A84F257B63"
}
## [Failed API Authentication Request](/docs/mdcloud/integrations/api-authentication-mechanisms#failed-api-authentication-request)

In case you provide a nonexistent API key, MetaDefender Cloud APIs will respond with a **401 Invalid API key** request.

> curl -v -X POST https://api.metadefender.com/v4/file -H 'apikey: $NON_EXISTING_API_KEY' -H 'filename: file.zip' -H 'samplesharing: 0'
 
> POST /v4/file HTTP/1.1
> Host: api.metadefender.com
> User-Agent: curl/7.52.1
> Accept: */*
> apikey: NON_EXISTING_API_KEY
> filename: file.zip
> samplesharing: 0
>
< HTTP/1.1 401 Invalid API key
< Content-Type: text/plain; charset=utf-8
< Date: Wed, 23 Aug 2017 18:43:42 GMT
< Vary: Accept-Encoding
< Content-Length: 0
< Connection: keep-alive
<
* Curl_http_done: called premature == 0
* Connection #0 to host api.metadefender.com left intact
{"error":{"code":401006,"messages":["Invalid API key"]}}
