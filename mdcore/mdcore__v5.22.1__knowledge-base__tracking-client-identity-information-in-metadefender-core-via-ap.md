<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap -->

# Tracking Client Identity Information in MetaDefender Core via API

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems from version v5.14.2

## [Overview](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#overview)

The **Client Identity** capability in **MetaDefender Core (MD Core)** lets integrators attach *source/client metadata* to scan requests. This allows administrators to identify **which client system or integration** submitted a file for scanning and improves traceability in multi-client deployments.

### [Why This Matters](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#why-this-matters)

In environments where multiple systems connect to a shared MD Core instance (for example, Kiosks, MFT workflows, or API gateways), it is often necessary to:

- Track the originating client for each request
- Improve auditability of scan traffic
- Speed up troubleshooting and reporting

## [About the `client-identity` Header](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#about-the-client-identity-header)

`client-identity` is an optional header designed to carry identification context for scan requests.

In a chained workflow (example: MetaDefender Kiosk → MetaDefender MFT → MetaDefender Core), this metadata can represent one or more client hops and helps MD Core log who/what initiated the scan.

### [Typical Metadata Included](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#typical-metadata-included)

The header can contain details such as:

- Client/system name
- Client hostname
- User name associated with the request
- Deployment ID (unique identifier for the client site/instance)
- Timestamp captured at the client side (when the file/request was received)
- Client product/version information

### [Scan Workflows That Support Client Identity](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#scan-workflows-that-support-client-identity)

Client identity metadata can be submitted with common scan flows, including:

- Synchronous analysis
- Asynchronous analysis
- Local scan
- Scan from link
- Batch scanning
- Multipart upload sessions

### [Common API Operations Where Client Identity Applies](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#common-api-operations-where-client-identity-applies)

Client identity information can be used with the scan request and later retrieved/validated through API calls such as:

- **Fetch / Status Requests**

  - Fetch analysis result
  - Fetch analysis result by hash
  - Retrieve batch analysis status
- **Submission Requests**

  - Submit file for analysis (async)
  - Submit file for analysis (sync)
  - Create/initiate batch
  - Create multipart upload session

### [Where You Can View Client Identity Information](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#where-you-can-view-client-identity-information)

Once submitted, client identity details can be reviewed from multiple sources:

- **MetaDefender Core Web Console**

  - View scan request details through the UI (Processing History → View Client Identity).
- **Processing Result JSON**

  - The client identity payload is included as part of the processing result output.
- **My OPSWAT Central Management (MOCM)**

  - MD Core forwards client identity as part of scan reporting for centralized monitoring and reporting.

### [Example JSON Payload](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#example-json-payload)

- **Standard Example**

JsonCopy{
"clients": [
{
"deployment_id": "abcdef1234567890",
"user_name": "Gemini",
"product_type": "MetaDefender Kiosk",
"version": "1.0.0",
"host": "client.example.com",
"timestamp": 1744949754890
}
]
}

- **Example Used in Testing**

JsonCopy{
"clients": [
{
"deployment_id": "Test123",
"user_name": "Test-User",
"product_type": "PostMan",
"version": "1.0.0",
"host": "test.com",
"timestamp": 1761658500000
}
]
}
### [Parameter Description](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#parameter-description)

| Field | Type | Description | Key Types |
| --- | --- | --- | --- |
| **deployment_id** | String | Unique identifier for the originating client deployment. | REQUIRED |
| **user_name** | String | User identity associated with the scan request. | REQUIRED |
| **product_type** | String | Client integration/product name (e.g., Kiosk, MFT, Postman). | REQUIRED |
| **version** | String | Client product version sending the request. | OPTIONAL |
| **host** | String | Hostname or domain of the client source system. | OPTIONAL |
| **timestamp** | Number | Unix timestamp (milliseconds) captured for the request at the client side. | REQUIRED |

## [Implementation Steps](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#implementation-steps)

1. Include the `clients` object in the scan request payload sent to MD Core.
2. Add the `client-identity` header (if required by your integration approach).
3. Submit the scan request using Postman or your application.
4. Open Processing History in the MD Core UI and select View Client Identity.

## [Verification](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#verification)

Validate that the values shown match what was sent from the client.

## [Screenshots:](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#screenshots)

**PostMan/API Client:**

**MD Core:**

Or:

## [Notes / Best Practices](/docs/mdcore/v5.22.1/knowledge-base/tracking-client-identity-information-in-metadefender-core-via-ap#notes--best-practices)

- Use consistent naming conventions for `deployment_id`, `host`, and `product_type` across all integrations.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
