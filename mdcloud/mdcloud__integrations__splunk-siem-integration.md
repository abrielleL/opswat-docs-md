<!-- source: https://www.opswat.com/docs/mdcloud/integrations/splunk-siem-integration -->

# Splunk SIEM Integration

### [**Overview**](/docs/mdcloud/integrations/splunk-siem-integration#overview)

The MetaDefender Cloud platform introduces a new Enterprise-only capability that enables direct SIEM integration with Splunk. This integration allows enterprise customers to automatically forward security logs related to file scanning and user activity from MetaDefender Cloud API’s Prevention Package to their Splunk instance. By doing so, organizations gain a centralized view of security events, enabling faster threat detection, improved compliance and better operational control.

### [**Technical Implementation**](/docs/mdcloud/integrations/splunk-siem-integration#technical-implementation)

The integration functions through a secure HTTP connection between MetaDefender Cloud and the customer’s Splunk environment. When security events occur, MetaDefender Cloud generates detailed logs, which in turn enable the customer’s security team to monitor threats in real time.

Data Flow Process

The system follows a structured data flow:

1. Users interact with MetaDefender Cloud, performing actions such as file scanning, DLP policy enforcement or CDR processing.
2. MetaDefender Cloud generates event logs. This integration only captures and forwards relevant security events from the Prevention Package, including:

- Multiscanning results.
- DLP violations (files flagged for containing sensitive data).
- CDR processing outcomes.
- User activity logs (e.g., users added to organizations / sub-organizations, users removed from organizations / sub-organizations, unauthorized user access to data, etc.)
- System configuration changes and policy updates.

3. Logs are processed into Splunk’s required format and transmitted securely in real-time.
4. Security teams gain full visibility into security events, allowing them to track infections, enforce policies and investigate potential threats.

### [**Technical Requirements**](/docs/mdcloud/integrations/splunk-siem-integration#technical-requirements)

To enable this integration, customers must have:

- A MetaDefender Cloud enterprise subscription.
- A properly configured Splunk instance with appropriate API access permissions.

### [**Data Security and Privacy**](/docs/mdcloud/integrations/splunk-siem-integration#data-security-and-privacy)

The integration maintains high security standards by:

- Encrypting log transmissions using secure channels.
- Enforcing authentication requirements for API access.
- Ensuring compliance with relevant data privacy regulations (e.g., GDPR, HIPAA, ISO 27001).

### [**Performance Impact**](/docs/mdcloud/integrations/splunk-siem-integration#performance-impact)

The log forwarding process is asynchronous, ensuring that it does not impact MetaDefender Cloud’s performance or cause delays in file scanning and security operations. This minimizes processing overhead while maintaining real-time visibility in Splunk.

### [**Scalability**](/docs/mdcloud/integrations/splunk-siem-integration#scalability)

The integration supports high-volume log transmission, making it suitable for organizations of all sizes. The architecture can scale dynamically to accommodate increasing log volume as customer usage grows.

### [**Future Developments**](/docs/mdcloud/integrations/splunk-siem-integration#future-developments)

While this initial release supports Splunk SIEM, the architecture is designed for future expansion. OPSWAT plans to extend support to additional SIEM platforms based on customer demand, ensuring broad compatibility across enterprise security environments.

### [**SIEM Enablement**](/docs/mdcloud/integrations/splunk-siem-integration#siem-enablement)

**To enable SIEM integration, please provide the following information:**

*Example for Splunk:*

- **Splunk HEC (HTTP Event Collector) Endpoint:** `https://splunk.yourdomain.com:8088`
- **HEC Token:** `XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`
