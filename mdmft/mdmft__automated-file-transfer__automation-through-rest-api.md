<!-- source: https://www.opswat.com/docs/mdmft/automated-file-transfer/automation-through-rest-api -->

# Automation through REST API

Summarize Page    Connect to Cursor Connect to VS Code

This section outlines the REST API calls compatible with MetaDefender Managed File Transfer. Using the application's interface, any third-party application can seamlessly interact and communicate with MetaDefender Managed File Transfer. This integration enables MetaDefender Managed File Transfer to be incorporated into automated workflows.

### [Authentication](/docs/mdmft/automated-file-transfer/automation-through-rest-api#authentication)

#### [User-Level Authentication](/docs/mdmft/automated-file-transfer/automation-through-rest-api#user-level-authentication)

Retrieve the authentication key by invoking the [Request an API Key](/docs/mdmft/metadefender-mft#getrequest-an-api-key) endpoint. Bear in mind that these keys have a finite lifespan and should be periodically refreshed to comply with the expiration policy. Their duration can also be managed through [Session Settings](/docs/mdmft/configuration/session-settings).

#### [API Keys](/docs/mdmft/automated-file-transfer/automation-through-rest-api#api-keys)

Newly created API keys, restricted to administrator-level access, can be utilized for all API endpoints calls. Further details on API key generation can be found by referring to the provided [API Keys](/docs/mdmft/configuration/api-keys).

### [Authorization](/docs/mdmft/automated-file-transfer/automation-through-rest-api#authorization)

Authorization via the **Authorization header** is required for all API endpoints expect the authentication endpoint. Users can choose an API key to bypass the authentication process for accessing the API endpoints.

Info

When making API requests, the "Authorization" header must include a bearer token, such as:

'Authorization': 'Bearer [API_Key]'

#### [Permissions](/docs/mdmft/automated-file-transfer/automation-through-rest-api#permissions)

The API offers flexible access options, supporting both user-level and admin-level (API key) permissions. This flexibility ensures secure interactions that are tailored to specific authorization requirements.

### [Response Codes (Status Codes)](/docs/mdmft/automated-file-transfer/automation-through-rest-api#response-codes-status-codes)

The Metadefender Managed Transfer File API provides data in valid JSON format.

#### [2xx Status Codes](/docs/mdmft/automated-file-transfer/automation-through-rest-api#2xx-status-codes)

All responses with 2xx status codes in the Metadefender Managed Transfer File API include a JSON body containing relevant keys and associated data.

JsonCopy{
"message": null,
"ui_message_key": null,
}
#### [4xx Status Codes](/docs/mdmft/automated-file-transfer/automation-through-rest-api#4xx-status-codes)

Here are some of the commonly encountered 4xx class status codes when interacting with the MetaDefender Managed File Transfer API.

- **400 - Bad Request**: A 400 status code means there's an issue with the request sent to the server, such as missing parameters, incorrect data, or the way you formed the request.
- **401 - Unauthorized:** A 401 status code indicates that the request lacks proper authentication credentials or that the provided credentials are insufficient.
- **403 - Forbidden:** A 403 status code means you are authenticated, but don't have permission to access the resource.
- **404 - Not Found:** A 404 status code means that the server couldn't find the requested resource This could be due to a mistyped URL, the resource being moved or deleted, or simply because the server doesn't recognize the endpoint you specified.

#### [5xx Status Codes](/docs/mdmft/automated-file-transfer/automation-through-rest-api#5xx-status-codes)

5xx errors indicate server-side issues due to unexpected errors or temporary unavailability. These errors require server administrator attention to resolve the underlying problems and restore proper functionality.

- **500 - Internal Server Error**

  - The 500 status code indicates an unforeseen and generic server-side error, reflecting a failure to fulfill the request.
- **503 - Service Unavailable**

  - A 503 status code signals that the server is temporarily unable to handle the request, possibly due to maintenance, overload, or other transient issues.

### [Deprecation](/docs/mdmft/automated-file-transfer/automation-through-rest-api#deprecation)

MetaDefender Managed File Transfer adheres to strict deprecation guidelines for its APIs. Developers must stay informed about the deprecation process and any API modifications. The deprecation period typically spans two releases for a given endpoint and is clearly communicated in the MetaDefender Managed File Transfer API Reference. It is crucial to exercise caution during product development to prevent complications stemming from deprecated endpoints.

Info

While some deprecated endpoints may still function, they will no longer receive new features or updates.
