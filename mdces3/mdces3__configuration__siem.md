<!-- source: https://www.opswat.com/docs/mdces3/configuration/siem -->

# SIEM

Summarize Page

**MetaDefender Cloud Email Security ™** allows integration with external SIEM systems. Follow the steps below to configure a provider.

## [Supported Integrations](/docs/mdces3/configuration/siem#supported-integrations)

### [Elasticsearch](/docs/mdces3/configuration/siem#elasticsearch)

Use this option to forward events directly to an Elasticsearch cluster.

#### [Configuration Steps](/docs/mdces3/configuration/siem#configuration-steps)

1. **Select** ***Elasticsearch*** under *Service Selection*.
2. **Endpoint URL** Enter the Elasticsearch endpoint, for example: `https://<host>:9200`
3. **Authentication Type** Select **Basic Authentication**.
4. **Authentication Details**

   - **Username**: Enter the Elasticsearch username.
   - **Password**: Enter the corresponding password.
5. **Filters**

   - Enable **Send Events** to forward events.
   - Select one or more **Statuses**, such as:

     - Closed Without Action
     - Deleted
     - Delivered
     - Failed to Deliver
     - Investigating
     - Quarantined
     - Released
     - Rescanning
   - Select one or more **Verdicts**, such as:

     - Malicious
     - Suspicious
     - Sanitized
     - No threat detected
     - Encrypted content
     - Unsupported file type
     - Invalid file structure
     - Failure to analyze
     - Skipped
     - Sanitization policy error
6. **Audit Log Filters**

   - Enable **Send Audit Logs** to forward administrative activity.
   - Select **Event Types**, such as:

     - Authentication
     - Configuration
7. Click **Save Changes** to apply the configuration.

### [Generic HTTP](/docs/mdces3/configuration/siem#generic-http)

Use this option to forward events to a custom HTTP endpoint or third-party SIEM service.

#### [Configuration Steps](/docs/mdces3/configuration/siem#configuration-steps)

1. **Select** ***HTTP*** under *Service Selection*.
2. **Endpoint URL** Enter the destination service endpoint, for example: `https://<host>:8080`
3. **API Key** Specify the API key required by the destination service.
4. **Filters**

   - Enable **Send Events** to forward events.
   - Configure **Status** and **Verdict** filters as needed.
5. **Audit Log Filters**

   - Enable **Send Audit Logs** to forward audit events.
   - Select relevant **Event Types** (for example, Authentication or Configuration).
6. Click **Save Changes** to apply the configuration.

IP ranges

See [Locations](/docs/mdces3/compliance/locations) for the list of IP addresses from which **MetaDefender Cloud Email Security ™** sends SIEM data.

## [JSON Output Reference](/docs/mdces3/configuration/siem#json-output-reference)

### [Common Fields](/docs/mdces3/configuration/siem#common-fields)

### [Event Fields](/docs/mdces3/configuration/siem#event-fields)

#### [Processing Details](/docs/mdces3/configuration/siem#processing-details)

#### [Metadata](/docs/mdces3/configuration/siem#metadata)

#### [Overall Scan Result](/docs/mdces3/configuration/siem#overall-scan-result)

#### [Parts](/docs/mdces3/configuration/siem#parts)

#### [Audit History](/docs/mdces3/configuration/siem#audit-history)

### [Audit Fields](/docs/mdces3/configuration/siem#audit-fields)

### [Connection Test Fields](/docs/mdces3/configuration/siem#connection-test-fields)
