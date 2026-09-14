<!-- source: https://www.opswat.com/docs/mdcloud/integrations/throttling -->

# Throttling

Throttling refers to the practice of limiting requests to endpoints after a certain threshold is reached. Our throttling mechanism allows up to:

- 9 requests/hour for free users and a limit of 45 scans per day with a [personal license](https://metadefender.opswat.com/licensing?lang=en)
- 75 requests/minute for paid users with a [standard license](https://metadefender.opswat.com/licensing)
- 150 requests/minute for paid users with a [professional license](https://metadefender.opswat.com/licensing)
- 500+ requests/minute for paid users with an [enterprise license](https://metadefender.opswat.com/licensing)

There are certain endpoints in MetaDefender Cloud that can be throttled:

- [Scanning a file by file upload](/docs/mdcloud/metadefender-cloud-api-v4#file-upload)
- [Data Sanitization Request](/docs/mdcloud/metadefender-cloud-api-v4#file-sanitized)
- [Retrieving scan reports for multiple data hashes](/docs/mdcloud/metadefender-cloud-api-v4#hash-bulklookup)
- [Scanning list of IPs](/docs/mdcloud/metadefender-cloud-api-v4#ip-bulklookup)
- [Scanning list of URLs](/docs/mdcloud/metadefender-cloud-api-v4#url-bulklookup)
- [Scanning list of domains](/docs/mdcloud/metadefender-cloud-api-v4#domain-bulklookup)

To the above endpoints. If a user exceeds the allowed values, the requests will be blocked, and an HTTP response code of 429 will be returned.

"error": {
"name": "ClientError",
"messages": "Your request has been throttled, maximum requests per hour: 9 for free users",
"code": 429001,
"status": 429
}

In such cases, please limit the number of requests sent per minute.

If you have inadvertently reached the limit and need assistance in identifying the cause of being throttled, please contact [OPSWAT Support](https://www.opswat.com/support).
