<!-- source: https://www.opswat.com/docs/mdcloud/operation/retrieving-scan-results-via-webhooks -->

# Retrieving Scan Results Via Webhooks

When uploading a file, please send the 'callbackurl' header with the URL where MetaDefender Cloud should send the results once scanning is complete.

Immediately after the scan finishes, our servers will send an HTTP POST to the URL specified in the header with the value that would have been retrieved from the data ID lookup (found here: [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Fetch analysis result)). This method is useful for avoiding long polling processes and can be integrated into asynchronous scanning workflows.

For testing the functionality without having a dedicated URL that can receive HTTP POST requests, we recommend using a service such as <https://webhook.site/> with an API client such as postman:

The callback URL should receive data within a few seconds:

The callback URL will be called no matter what scan results have been produced and even if we encountered an error.
