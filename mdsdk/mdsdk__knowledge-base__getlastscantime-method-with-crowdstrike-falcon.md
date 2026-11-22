<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon -->

# How to use GetLastScanTime method with CrowdStrike Falcon?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Check Your Version

This article applies to MetaDefender Endpoint Security SDK 4.3.6139.0 and later on Windows, for CrowdStrike Falcon (signature `2866`).

## [Overview](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#overview)

The `GetLastScanTime` method (method `1004`) returns the time of the most recent on-demand scan for CrowdStrike Falcon. Falcon keeps on-demand scan history in the CrowdStrike cloud rather than on the endpoint, so the SDK reads it from the CrowdStrike Falcon API using API client credentials that you pass in `json_in`.

api_url and credentials are required for CrowdStrike Falcon

The general `GetLastScanTime` reference lists `api_url` and `credentials` as optional input. For CrowdStrike Falcon they are **required**. If either is missing, the SDK cannot query the Falcon API and the call fails.

## [Prerequisites](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#prerequisites)

Before you call `GetLastScanTime`, make sure that:

- The CrowdStrike Falcon sensor is installed on the endpoint.
- Your CrowdStrike Falcon subscription includes on-demand scanning.
- You have a Falcon console role that can create API clients.

Then set up an API client:

1. In the CrowdStrike Falcon console, open **API clients and keys** and create a new API client.

CrowdStrike Falcon console, API client management

2. Grant the API client the **On-demand scans (ODS)** scope with **Read** access.

Create API client dialog

3. Save the generated **Client ID** and **Client Secret**. The secret is shown only once.
4. Note the CrowdStrike Falcon API base URL for your cloud region, for example:

   - `https://api.crowdstrike.com` (US-1)
   - `https://api.us-2.crowdstrike.com` (US-2)
   - `https://api.eu-1.crowdstrike.com` (EU-1)

The method does not require administrator privileges on the endpoint.

## [Input format](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#input-format)

Pass the parameters through the `json_in` argument. The highlighted lines are specific to CrowdStrike Falcon.

{
"input": {
"method": 1004,
"signature": 2866,
"scan_type": "path",
"api_url": "https://api.us-2.crowdstrike.com",
"credentials": {
"client_id": "<YOUR_CLIENT_ID>",
"client_secret": "<YOUR_CLIENT_SECRET>"
}
}
}

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `input.method` | Integer | Yes | Method ID of `GetLastScanTime`. Use `1004`. |
| `input.signature` | Integer | Yes | Signature ID of CrowdStrike Falcon. Use `2866`. |
| `input.scan_type` | String | No | Scan type to query (`default`, `full`, or `path`). For CrowdStrike Falcon, the scan type in the result is always `unspecified`, whichever value you pass. See [Scan type](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#scan-type). |
| `input.api_url` | String | Yes | CrowdStrike Falcon API base URL for your cloud region. |
| `input.credentials.client_id` | String | Yes | Client ID of the Falcon API client created in [Prerequisites](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#prerequisites). |
| `input.credentials.client_secret` | String | Yes | Client secret of the Falcon API client created in [Prerequisites](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#prerequisites). |

## [Expected behavior](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#expected-behavior)

When the request is configured correctly, the SDK:

1. Authenticates to the CrowdStrike Falcon API with the supplied credentials.
2. Reads the on-demand scan history for the endpoint.
3. Returns the time of the most recent completed on-demand scan.

If a scan is still running when you call the method, the SDK checks the five most recent scans and returns the time of the latest one that has completed. If no completed on-demand scan exists, no scan time is returned.

### [Scan type](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#scan-type)

The scan type in the result is always `unspecified`. CrowdStrike Falcon records every on-demand scan as a scan of a location, such as a drive (`C:\`) or a folder (`C:\Users\`), including scans started with the **Scan System Drive** option. A Falcon scan record therefore cannot be mapped reliably to an SDK scan type such as `full`, `default`, or `path`.

## [Troubleshooting](/docs/mdsdk/knowledge-base/getlastscantime-method-with-crowdstrike-falcon#troubleshooting)

| Error code or symptom | Possible cause | Recommended resolution |
| --- | --- | --- |
| `WAAPI_ERROR_INVALID_INPUT_ARGS` (`-20`) | The JSON is malformed, `api_url` or `credentials` is missing, or `api_url` is not a valid URL. | Check the JSON syntax and confirm that `api_url`, `client_id`, and `client_secret` are present and correctly formatted. |
| Connection or authentication error, such as `WAAPI_ERROR_NO_CONNECTION` (`-17`) | The SDK could not get scan data from the Falcon API. Common causes are no network access to `api_url`, an `api_url` that does not match your Falcon cloud region, a wrong or revoked client ID or secret, or an API client without **On-demand scans (ODS)** Read access. | Check network access to `api_url` and confirm the URL matches your Falcon cloud region. In the Falcon console, confirm the API client is active and has the **On-demand scans (ODS)** scope with Read access. Reset the secret or create a new API client if needed. |
| No scan time returned | No completed on-demand scan exists for the endpoint, or the only recent scans are still running. | Run an on-demand scan from the Falcon console, wait for it to complete, then call the method again. |

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
