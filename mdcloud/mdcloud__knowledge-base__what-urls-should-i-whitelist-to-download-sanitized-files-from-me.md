<!-- source: https://www.opswat.com/docs/mdcloud/knowledge-base/what-urls-should-i-whitelist-to-download-sanitized-files-from-me -->

# What URLs should I whitelist to download sanitized files from MetaDefender Cloud?

This article is applied to MetaDefender Cloud.

**Issue:** Users may be unable to download sanitized files from MetaDefender Cloud if the appropriate regional URLs are not allowed through firewall or security settings. These download URLs vary based on the region where the API call is made.

**Resolution:** To ensure successful downloads of sanitized files, whitelist the following URLs according to the region where the MetaDefender Cloud API request is initiated:

- **North America (United States, West coast)** `https://s3.us-west-2.amazonaws.com/sanitized.files.metadefender.com/*` `https://s3.us-east-2.amazonaws.com/sanitized.files.metadefender.com-useast2/*`
- **Europe Central (Germany)** `https://s3.eu-central-1.amazonaws.com/sanitized.files.metadefender.com-eucentral1/*`
- **Canada (Montreal)** `https://s3.ca-central-1.amazonaws.com/sanitized.files.metadefender.com-cacentral1/*`
- **Australia (Sydney)** `https://s3.ap-southeast-2.amazonaws.com/sanitized.files.metadefender.com-apsoutheast2/*`
- **Japan (Tokyo)** `https://prod-mdc-platform-sanitized-files-apnortheast1.s3.ap-northeast-1.amazonaws.com/*`
- **India (Mumbai)** `https://prod-mdc-platform-sanitized-files-apsouth1.s3.ap-south-1.amazonaws.com/*`

Make sure that **Port 443 (HTTPS)** is open for outbound connections to the above domains. All downloads are conducted securely over HTTPS.

If your network uses additional security layers such as web proxies, content filters, or intrusion prevention systems, be sure to allow these URLs through those as well.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
