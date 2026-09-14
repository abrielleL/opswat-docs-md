<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-use-getlastscantime-method-with-trend-micro-deep-security -->

# How to use GetLastScanTime method with Trend Micro Deep Security Agent?

This article is applied to MetaDefender Endpoint Security SDK **on Windows** with Trend Micro Deep Security Agent integrations.

## [Overview](/docs/mdsdk/knowledge-base/how-to-use-getlastscantime-method-with-trend-micro-deep-security#overview)

The **GetLastScanTime** method is supported for **Trend Micro Deep Security Agent** (signature 618), but, unlike other products, you will need to provide the `token` value, which is an API Key obtained from the **Trend Cloud One** platform.

If the method is called using the standard `json_in` structure without the `token`, it will return an error **WAAPI_ERROR_INVALID_INPUT_ARGS**. This is expected behavior, as the vendor requires the Trend Cloud One to be queried with an **API Token** in order to retrieve scan data.

## [Retrieving the API Token from Trend Cloud One](/docs/mdsdk/knowledge-base/how-to-use-getlastscantime-method-with-trend-micro-deep-security#retrieving-the-api-token-from-trend-cloud-one)

1. Log in to the [Trend Cloud One™ dashboard](https://cloudone.trendmicro.com/home) and select **Endpoint & Workload Security**.
2. Go to **Administration.**

3. Navigate to **API Key** → **New.**

---

## [Invoking GetLastScanTime](/docs/mdsdk/knowledge-base/how-to-use-getlastscantime-method-with-trend-micro-deep-security#invoking-getlastscantime)

When using the **GetLastScanTime** method with Trend Micro Deep Security Agent, please note that the method call:

- **Requires** administrator rights.
- **Requires** an API token ([Retrieving the API Token from Trend Cloud One](/docs/mdsdk/knowledge-base/how-to-use-getlastscantime-method-with-trend-micro-deep-security#retrieving-the-api-token-from-trend-cloud-one)).
- Output **returns only** `unspecified` for `scan_type` field.

json_inCopy{
"input": {
"method": 1004,
"signature": 618,
"scan_type": string,
// any inputs "default", "full", and "path" for scan_type all produce the same output: "unspecified"
"token": string
}
}Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
