<!-- source: https://www.opswat.com/docs/macloud-sdp/siem-integrations/inputs -->

# Inputs

The MetaDefender IT-OT Access Add-on for Splunk ingests MetaDefender IT-OT Access Logs to the MetaDefender IT-OT Access:Logs sourcetype and other API inputs to MetaDefender IT-OT Access:API sourcetype.

The Add-on provides **Get Admin Logs, Get Device Logs, Get Vulnerabilities, Get Account Details, and Get Devices** inputs OOTB. All of the inputs are disabled by default as per Splunk’s best practices. Once a user configures an account and has the appropriate index ready, these inputs should be edited to include the desired account and index before enabling them. Alternatively, you can clone the original inputs and edit the cloned inputs. Attempting to delete the inputs provided OOTB will result in an error. This is because the configuration of these inputs is provided within the default directory, instead of the local directory like user-created inputs. To delete these inputs, you must open the default/inputs.conf configuration file in a text editor, locate the stanza of the desired input, and remove it. After saving the default/inputs.conf file, you must restart Splunk to apply the change.

You can follow the below steps to configure a new input:

1. Login to the Splunk Web UI.
2. Go to the **Inputs** page of the OPSWAT MetaDefender IT-OT Access Add-on.
3. Click on the Create New Input button and select the appropriate input type for your needs.

4. Fill in the appropriate details in the dialog.

Details for each input can be found below.

## [MetaDefender IT-OT Access Logs](/docs/macloud-sdp/siem-integrations/inputs#metadefender-it-ot-access-logs)

MetaDefender IT-OT Access Logs input collects logs from a MetaDefender IT-OT Access account with a defined category such as Admin Events, Device Events, or Webhook events and filters.

The below table explains meaning of each field when you create/update a MetaDefender IT-OT Access Logs input.

| **Input Name** | **Required** | **Description** |
| --- | --- | --- |
| Name | Yes | Appropriate unique name for the Input you are creating. This box will not accept the space in name |
| Interval (seconds) | Yes | Frequency at which Splunk makes an API call to fetch the latest logs. **The default value of 300 seconds is recommended for** **MetaDefender IT-OT Access** **logs API**. Intervals less than 60 seconds are NOT permitted and will generate an error when saving the input. |
| Index | Yes | Select the appropriate Index from the dropdown for this input. |
| Global Account | Yes | Select the Account (that you have created in previous steps) from the drop-down menu. |
| API Endpoint | Yes | Specify an endpoint of Get Logs API to retrieve event logs. Default value: “/o/api/v3.1/logs”. This Add-on is tested with [MetaAccess Get Logs v3.1](/docs/macloud-sdp/developer-guide/get-logs-v3-1) only. |
| Event Category | Yes | Select any of 3 possible event categories for MetaDefender IT-OT Access logs   - Device: device event logs - Admin: administrator event logs - Webhook: webhook event logs - Device Report: device report trail logs. MetaDefender IT-OT Access records an event logs for each device reports even the device doesn't change status or no new issues found. This trail log is only available through API and requires special license. |
| Number of Days Back | Yes | Enter the number of days prior to configuration day to collect log events.   - The value can be 1 to 30. - Default value: 7. |
| Filter | No | Specify any additional filters that you want to pass on to the Logs API call. Refer to [the MetaAccess Get Logs v3.1 API documentation](/docs/macloud-sdp/developer-guide/get-logs) to learn how to apply filters. |

**Get Logs Filter Example**

{
    "events": [
        "access_granted",
        "access_revoked",
        "compliance_check"
    ],
    "agent_types": [
        0,
        2
    ]
}

MetaDefender IT-OT Access Logs input Example.

## [MetaDefender IT-OT Access Device Logs](/docs/macloud-sdp/siem-integrations/inputs#metadefender-it-ot-access-device-logs)

MetaDefender IT-OT Access Device Logs input collects device event logs as well as additional device data such as device details and vulnerabilities from a MetaDefender IT-OT Access account.

The below table explains meaning of each field when you create/update a MetaDefender IT-OT Access Logs input.

| **Input Name** | **Required** | **Description** |
| --- | --- | --- |
| Name | Yes | Appropriate unique name for the Input you are creating. This box will not accept the space in name |
| Interval (seconds) | Yes | Frequency at which Splunk makes an API call to fetch the latest logs. **The default value of 300 seconds is recommended for** **MetaDefender IT-OT Access** **Device logs API**. Intervals less than 60 seconds are NOT permitted and will generate an error when saving the input. |
| Index | Yes | Select the appropriate Index from the dropdown for this input. |
| Global Account | Yes | Select an Account (that you have created in previous steps) from the drop-down menu. |
| API Endpoint | Yes | Specify an endpoint of the Get Logs API to retrieve device event logs. Default value: “/o/api/v3.1/logs” The Add-on is tested with [MetaAccess Get Logs v3.1](/docs/macloud-sdp/developer-guide/get-logs) only. |
| Number of Days Back | Yes | Enter the number of days prior to configuration day to collect device event logs. However, these event logs won’t trigger extra API calls for device details or vulnerabilities   - The value can be 1 to 30. - Default value: 7. |
| Filter | No | Apply any additional filters that you want to pass on to the Get Logs API call. Refer to the [Get Logs](/docs/macloud-sdp/developer-guide/get-logs) API to learn how to apply filters. |
| Event Triggers | Yes | Select events that should trigger additional API calls to collect device details and/or Device Vulnerabilities. Default value: events that a device became non-compliant or reported issues. |
| Retrieve Device Details | No | Enable this setting if you would like to retrieve device details when an event is in Event Triggers. The device details information will be inserted into Splunk along with *event* and *event_timestamp* to identify what event triggered this call. |
| Device Details Endpoint | Yes | Specify an endpoint of Device Details API to retrieve device details information when selected event triggers are met. Default value: “/o/api/v3.3/devices/detail” |
| Device Details Body | No | Specify any additional filters to device details API through Body parameter. The recommended value is *{"verbose": {"system_info": 1, "categories": 1, "unclassified": 0, "mobile_apps": 0, "detected_processes": 0, "detected_packages": 0, "detected_patches": 0}}.* to retrieve a device system information and issues on compliance categories based on a policy. Refer to the API documentation page [here](/docs/macloud-sdp/developer-guide/device-details) to learn how to apply filters. |
| Retrieve Device CVEs | No | Enable this setting if you would like to retrieve vulnerabilities of a device when an event is in Event Triggers. The device CVEs will be separated and inserted into Splunk along with device_username, *event* and *event_timestamp* to identify what event triggered this call. |
| Device CVEs Endpoint | Yes | Specify an endpoint of Get Vulnerabilities of a device API to retrieve vulnerabilities of a device. Default value: “/o/api/v3/get_cves”. |
| Device CVEs Body | No | Specify any additional filters to Get Vulnerabilities of a device endpoint through Body parameter. The recommended value is *{"verbose": 0}* to retrieve only CVE-ID, score, and severity_._ Refer to the API documentation page [here](/docs/macloud-sdp/developer-guide/get-vulnerabilities-of-a-device) to learn how to apply filters. |

Info

Device Details/Get Vulnerabilities of a device (Device CVEs) API returns the current data of a device. With that being said, the Add-on only triggers a Device Details/Device CVEs API call for the most recent event for a device. In other words, if a device has multiple device events in an interval, only the last event will trigger a Device Details/Device CVEs call.

**Get Logs Filter Example**

{
    "events": [
        "access_granted",
        "access_revoked",
        "compliance_check"
    ],
    "agent_types": [
        0,
        2
    ]
}

MetaDefender IT-OT Access Device Logs input Example.

## [MetaDefender IT-OT Access API](/docs/macloud-sdp/siem-integrations/inputs#metadefender-it-ot-access-api)

The MetaDefender IT-OT Access API input allow Splunk administrator to collect data from a MetaDefender IT-OT Access account.

The below table explains meaning of each field when you create/update a MetaDefender IT-OT Access Logs input.

| **Input Name** | **Required** | **Description** |
| --- | --- | --- |
| Name | Yes | Appropriate unique name for the Input you are creating. This box will not accept the space in name |
| Interval (seconds) | Yes | Frequency at which Splunk makes an API call to fetch the latest logs. **Please be mindful of the interval you set for the Input as smaller value of interval for some less frequently updated APIs can ingest duplicate data at each run and counts against the Splunk License quota also.** For ex: Vulnerability details doesn’t get updated that frequently so running Get Vulnerability API every 60 second will end up ingesting duplicate data every 60 seconds. Intervals less than 60 seconds are NOT permitted and will generate an error when saving the input. |
| Index | Yes | Select the appropriate Index from the dropdown for this input. |
| Global Account | Yes | Select the Account (that you have created in previous steps) from the drop-down menu. |
| API Endpoint | Yes | Specify an endpoint of a MetaDefender IT-OT Access API you would like to retrieve information from an account. Refer to the API Documentation [here](/docs/macloud-sdp/developer-guide/apis) get the valid endpoint values. |
| HTTP Request Method | Yes | Select a HTTP request method (GET or POST) depending on the API endpoint you have chosen. For example: If you use [Get Devices](/docs/macloud-sdp/developer-guide/get-devices) API, HTTP Method should be POST. |
| Body | No | Specify any additional parameters in JSON format that you want to pass to the API request body. |

**MetaDefender IT-OT Access API input - Body Example**

{
"filter": {
"severity": [
"critical",
"important"
]
},
"sort": {
"order": "desc",
"field": "opswat_score"
}
}

**MetaDefender IT-OT Access API Input Configuration Example**
