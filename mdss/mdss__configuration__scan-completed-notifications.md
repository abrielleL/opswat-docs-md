<!-- source: https://www.opswat.com/docs/mdss/configuration/scan-completed-notifications -->

# Scan completed notifications

## [Overview](/docs/mdss/configuration/scan-completed-notifications#overview)

Scan Completed webhook notifications allow you to receive real-time alerts whenever an Instant or Scheduled scan has finished running in MetaDefender Storage Security. This feature is useful if you need to:

- Track the completion status of scans for auditing and compliance.
- Monitor whether scans succeed, fail, or are cancelled.
- Integrate scan lifecycle events into external systems (e.g., scheduling dashboards, reporting tools, SIEM).
- Trigger automated follow-up processes once a scan has completed.

## [Setup](/docs/mdss/configuration/scan-completed-notifications#setup)

1. Go to **Settings > Notifications** in the MetaDefender Storage Security console.
2. Select **Upon Scan Completion** under the **Webhook Notifications** section.
3. Enter the **Destination Address** (your endpoint).
4. Select the **Request Type** (**POST** or **PUT**).
5. (Optional) Add any custom **HTTP headers**.
6. Save the configuration.

## [Configuration Details](/docs/mdss/configuration/scan-completed-notifications#configuration-details)

- **Destination address** – The URL of the receiving system (must accept HTTP requests).
- **Request type** – Either `POST` or `PUT`.
- **Headers** – Optional key-value pairs (e.g., `Authorization: Bearer <token>`).

## [Webhook Payload](/docs/mdss/configuration/scan-completed-notifications#webhook-payload)

When triggered, the webhook sends a JSON request body to your configured endpoint.

Webhook Notification PayloadCopy{
"ScanId":"01987f90-870a-7826-9115-18d96a1a4ae0",
"ScanName":"second-scan",
"StartTime":"2025-08-06T13:27:14.953181Z",
"StopTime":"2025-08-06T13:27:20.12684Z",
"Status":"Completed",
"WebhookNotificationType": "ScanCompleted"
}
## [Field Reference](/docs/mdss/configuration/scan-completed-notifications#field-reference)

| Field | Type | Example Value | Description |
| --- | --- | --- | --- |
| `ScanId` | string(UUID) | `01987f90-870a-7826-9115-18d96a1a4ae0` | Unique identifier of the scan. |
| `ScanName` | string | `second-scan` | Name of the scan as configured. |
| `StartTime` | datetime (UTC) | `2025-08-06T13:27:14.953181Z` | Time the scan started. |
| `StopTime` | datetime (UTC) | `2025-08-06T13:27:20.12684Z` | Time the scan finished. |
| `Status` | string | `Completed` /`Cancelled` /`Failed` | Final status of the scan. |
| `WebhookNotificationType` | string | `ScanCompleted` | Identifies the notification type. |

## [Delivery Behavior](/docs/mdss/configuration/scan-completed-notifications#delivery-behavior)

- Webhooks are delivered as standard HTTP requests.
- Delivery is **best-effort** → if the destination is invalid, the request is logged in the **Audit page**, but no retries are performed.
- Payload size is small (JSON only, no scan contents).

## [Security Considerations](/docs/mdss/configuration/scan-completed-notifications#security-considerations)

- Configure HTTPS endpoints to ensure data is transmitted securely.
- Use authentication headers (e.g., API tokens) to protect your webhook endpoint.
- Ensure your endpoint validates payloads before processing.

## [Troubleshooting](/docs/mdss/configuration/scan-completed-notifications#troubleshooting)

- **No webhook received** → Verify the endpoint URL and request type (POST/PUT).
- **Audit shows delivery failed** → Endpoint is invalid or unreachable. Fix and test again.
- **Authentication errors** → Confirm your endpoint accepts the headers you configured.
