<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/url-capabilities -->

# What URL analysis capabilities are in MetaDefender Aether?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**MetaDefender Aether** (previously known as MetaDefender Sandbox) offers a variety of features around URL analysis. Here are the highlights:

- Full webpage rendering (Chrome), including capture of all GET/POST requests, Certificates and a Screenshot
- All potential IOCs captured during the webpage rendering phase are added to the main report and cross-checked against our real-time MD Cloud Reputation (includes 50B+ hashes, URLs, IPs, domains) service
- Machine Learning (ML) based image analysis for phishing detection
- Currently detects 339+ major brands
- Additional integrations with Google Safebrowsing

**Do you have an example API request/response?**

1. Submit a file using the `/api/scan/url` endpoint (Reference: <https://www.filescan.io/api/docs#/scan/scan_file_api_scan_url_post>) and obtain a flow_id
2. Using that flow_id, query the results using `/api/scan/<flow_id>/report` and apply at minimum the `ur%3ArenderResults` filter.

Example:

`https://www.filescan.io/api/scan/6437bf9d1f50fdcf669a0b60/report?filter=overallState&filter=finalVerdict&filter=allTags&filter=allSignalGroups&filter=ur%3ArenderResults`

The final verdict of the URL analysis can be obtained via the `finalVerdict` field, if the `overallState` field is set to SUCCESS (requires additional filters, see Example).

**Do you have documentation on the API fields returned?**

For all render related fields, please refer to the Chrome DevTools Protocol documentation, specifically Network Domain and related classes: <https://chromedevtools.github.io/devtools-protocol/tot/Network/>

Phishing detection related fields are present beneath the

JsonCopy"phishDetection": {
"brand": "Office365",
"category": 1,
}

Where the `category` field may be 0 (benign) or 1 (phishing detected). The `base64` field contains the rendered image.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
