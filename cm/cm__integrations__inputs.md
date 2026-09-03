<!-- source: https://www.opswat.com/docs/cm/integrations/inputs -->

# Inputs

The Add-on provides **Get Admin Logs, Get Device Logs, Get Vulnerabilities, Get Account Details, Get Devices and Get Product Reports** inputs OOTB (fresh install). All of the inputs are disabled by default as per Splunk’s best practices. Once a user configures an account and has the appropriate index ready, these inputs should be edited to include the desired account and index before enabling them. Alternatively, you can clone the original inputs and edit the cloned inputs. Attempting to delete the inputs provided OOTB will result in an error. This is because the configuration of these inputs is provided within the default directory, instead of the local directory like user-created inputs. To delete these inputs, you must open the default/inputs.conf configuration file in a text editor, locate the stanza of the desired input, and remove it. After saving the default/inputs.conf file, you must restart Splunk to apply the change.

> **Info**
>
> The add-on for Splunk ingests data MetaAccess Logs to the MetaAccess:Logs sourcetype and other MetaAccess API inputs to MetaAccess:API sourcetype.

You can follow the steps below to configure a new input:

1. Log in to the Splunk Web UI.
2. Go to the **Inputs** page of the My OPSWAT Central Management Add-on.
3. Click on the Create New Input button and select the appropriate input type for your needs.

![](https://uploads.developerhub.io/prod/97qW/eyswm13y6w2gi6n8lkikxouik0fgysz8jmhvtv85y8pb81y9s35ik5ydk05svgu7.png)

4. Fill in the appropriate details in the dialog.

Details for each input can be found below.

## Get Logs Input

Get Logs input collects logs from a My OPSWAT Central Management account with a defined category such as Admin Events, Device Events, or Webhook events and filters.

The below table explains meaning of each field when you create/update a Get Logs input.

| **Input Name** | **Required** | **Description** |
| ---- | ---- | ---- |
| Name | Yes | Appropriate unique name for the Input you are creating. This box will not accept the space in name |
| Interval (seconds) | Yes | Frequency at which Splunk makes an API call to fetch the latest logs. **The default value of 300 seconds is recommended for** **Get** **logs API**. Intervals less than 60 seconds are NOT permitted and will generate an error when saving the input. |
| Index | Yes | Select the appropriate Index from the dropdown for this input. |
| Global Account | Yes | Select the Account (that you have created in previous steps) from the drop-down menu. |
| API Endpoint | Yes | Specify an endpoint of Get Logs API to retrieve event logs. Default value: “/o/api/v3.2/logs”. This Add-on is tested with [Get Logs API](https://www.opswat.com/docs/cm/developer-guidelines/get-logs) only. |
| Event Category | Yes | Select any of 3 possible event categories - Device: device event logs - Admin: administrator event logs - Webhook: webhook event logs - Device Report: device report trail logs. MetaDefender IT Access records an event logs for each device reports even the device doesn't change status or no new issues found. This trail log is only available through API and requires special license. |
| Number of Days Back | Yes | Enter the number of days prior to configuration day to collect log events. - The value can be 1 to 30. - Default value: 7. |
| Filter | No | Specify any additional filters that you want to pass on to the Logs API call. Refer to  [the MetaAccess Get Logs v3.1 API documentation](https://www.opswat.com/docs/cm/developer-guide/get-logs) to learn how to apply filters. |

**Get Logs Filter Example**

```plaintext
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
```

Get Logs input Example.

![](https://uploads.developerhub.io/prod/97qW/d076j6ztc5pjek05uk67e2jvlxl5ciz1omvnh7a25km96tg4dt4eclitfmpccct1.png)

## Get Device Logs Input

Get Device Logs input collects device event logs as well as additional device data such as device details and vulnerabilities from a My OPSWAT Central Management account.

The below table explains meaning of each field when you create/update a Get Device Logs input.

| **Input Name** | **Required** | **Description** |
| ---- | ---- | ---- |
| Name | Yes | Appropriate unique name for the Input you are creating. This box will not accept the space in name |
| Interval (seconds) | Yes | Frequency at which Splunk makes an API call to fetch the latest logs. **The default value of 300 seconds is recommended for** **Device logs API**. Intervals less than 60 seconds are NOT permitted and will generate an error when saving the input. |
| Index | Yes | Select the appropriate Index from the dropdown for this input. |
| Global Account | Yes | Select an Account (that you have created in previous steps) from the drop-down menu. |
| API Endpoint | Yes | Specify an endpoint of the Get Logs API to retrieve device event logs. Default value: “/o/api/v3.2/logs” The Add-on is tested with [MetaAccess Get Logs v3.1](https://www.opswat.com/docs/cm/developer-guide/get-logs) only. |
| Number of Days Back | Yes | Enter the number of days prior to configuration day to collect device event logs. However, these event logs won’t trigger extra API calls for device details or vulnerabilities - The value can be 1 to 30. - Default value: 7. |
| Filter | No | Apply any additional filters that you want to pass on to the Get Logs API call. Refer to the [auto$](https://www.opswat.com/docs/cm/developer-guide/get-logs) API to learn how to apply filters. |
| Event Triggers | Yes | Select events that should trigger additional API calls to collect device details and/or Device Vulnerabilities. Default value: events that a device became non-compliant or reported issues. |
| Retrieve Device Details | No | Enable this setting if you would like to retrieve device details when an event is in Event Triggers. The device details information will be inserted into Splunk along with *event* and *event_timestamp* to identify what event triggered this call. |
| Device Details Endpoint | Yes | Specify an endpoint of Device Details API to retrieve device details information when selected event triggers are met. Default value: “/o/api/v3.4/devices/detail” |
| Device Details Body | No | Specify any additional filters to device details API through Body parameter. The recommended value is *{"verbose": {"system_info": 1, "categories": 1, "unclassified": 0, "mobile_apps": 0, "detected_processes": 0, "detected_packages": 0, "detected_patches": 0}}.* to retrieve a device system information and issues on compliance categories based on a policy. Refer to the API documentation page [here](https://www.opswat.com/docs/cm/developer-guide/device-details) to learn how to apply filters. |
| Retrieve Device CVEs | No | Enable this setting if you would like to retrieve vulnerabilities of a device when an event is in Event Triggers. The device CVEs will be separated and inserted into Splunk along with device_username, *event* and *event_timestamp* to identify what event triggered this call. |
| Device CVEs Endpoint | Yes | Specify an endpoint of Get Vulnerabilities of a device API to retrieve vulnerabilities of a device. Default value: “/o/api/v3/get_cves”. |
| Device CVEs Body | No | Specify any additional filters to Get Vulnerabilities of a device endpoint through Body parameter. The recommended value is *{"verbose": 0}* to retrieve only CVE-ID, score, and severity_._ Refer to the API documentation page [here](https://www.opswat.com/docs/cm/developer-guide/get-vulnerabilities-of-a-device) to learn how to apply filters. |

> **Info**
>
> Device Details/Get Vulnerabilities of a device (Device CVEs) API returns the current data of a device. With that being said, the Add-on only triggers a Device Details/Device CVEs API call for the most recent event for a device. In other words, if a device has multiple device events in an interval, only the last event will trigger a Device Details/Device CVEs call.

**Get Logs Filter Example**

```plaintext
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
```

Get Device Logs input Example.

![](https://uploads.developerhub.io/prod/97qW/fhspqml4vswtdkm7kvswu9nxxhhyujf1azuk5dsey05wels7sbtfd9dmk7qsipj4.png)

## Other APIs Input

The Other API input allow Splunk administrator to collect data from a My OPSWAT Central Management account.

The below table explains meaning of each field when you create/update a Other APIs input.

| **Input Name** | **Required** | **Description** |
| ---- | ---- | ---- |
| Name | Yes | Appropriate unique name for the Input you are creating. This box will not accept the space in name |
| Interval (seconds) | Yes | Frequency at which Splunk makes an API call to fetch the latest data. **Please be mindful of the interval you set for the Input as smaller value of interval for some less frequently updated APIs can ingest duplicate data at each run and counts against the Splunk License quota also.** For ex: Vulnerability details doesn’t get updated that frequently so running Get Vulnerability API every 60 second will end up ingesting duplicate data every 60 seconds. Intervals less than 60 seconds are NOT permitted and will generate an error when saving the input. |
| Index | Yes | Select the appropriate Index from the dropdown for this input. |
| Global Account | Yes | Select the Account (that you have created in previous steps) from the drop-down menu. |
| API Endpoint | Yes | Specify an endpoint of an API you would like to retrieve information from an account. Refer to the API Documentation [here](https://www.opswat.com/docs/cm/developer-guide/apis) get the valid endpoint values. |
| HTTP Request Method | Yes | Select a HTTP request method (GET or POST) depending on the API endpoint you have chosen. For example: If you use [auto$](https://www.opswat.com/docs/cm/developer-guide/get-devices) API, HTTP Method should be POST. |
| Body | No | Specify any additional parameters in JSON format that you want to pass to the API request body. |

**Body Example**

```plaintext
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
```

**Configuration Example**

![](https://uploads.developerhub.io/prod/97qW/agegd1ceuip346bfkk8jzr8g6m70rek9h2dfrz7r7qc3fiq1a5com6f4p8jf5wyz.png)

## **Product Reports Input**

Product Reports input collects reports from a My OPSWAT Central Management account.

The below table explains meaning of each field when you create/update a Product Reports input.

| Input Name | Required | Description |
| ---- | ---- | ---- |
| Name | Yes | Appropriate unique name for the Input you are creating. This box will not accept the space in name |
| Interval (seconds) | Yes | Frequency at which Splunk makes an API call to fetch the latest reports. **The default value of 300 seconds is recommended for** **the** **API**. Intervals less than 60 seconds are NOT permitted and will generate an error when saving the input. |
| Index | Yes | Select the appropriate Index from the dropdown for this input. |
| Global Account | Yes | Select the Account (that you have created in previous steps) from the drop-down menu. |
| API Endpoint | Yes | Specify an endpoint of Get Report API to retrieve reports. Values are: "/o/pmp/v1/reports", "/o/mdd/v1/reports", "/o/core/v1.1/reports" [Direct Instance Management - My OPSWAT Central Management](https://www.opswat.com/docs/cm/direct-instance-management#getpmpreports) [Direct Instance Management - My OPSWAT Central Management](https://www.opswat.com/docs/cm/direct-instance-management#getdrivereports) [Direct Instance Management - My OPSWAT Central Management](https://www.opswat.com/docs/cm/direct-instance-management#getcorereports) |
| Number of Days Back | Yes | Enter the number of days prior to configuration day to collect log events. - The value can be 1 to 30. - Default value: 7. |
| Filter | No | Specify any additional filters that you want to pass on to the Logs API call. Refer to <update later> to learn how to apply filters. |
| Retrieve Report Details | No | Enable this setting if you would like to retrieve report details when a report is received. The addon will make additional calling to get details information and it will be inserted into Splunk along with report. Default value: **No** |

**Get Report Filter Example**

```javascript
{
	"device_type": [
		"KIOSK"
	],
	"media_type": [
		"USB Device"
	],
	"issue_type": [
		"VUL", "COO"
	]
}
```

```javascript
{
	"scanned_host": [
		"qa-virtual-machine"
	],
	"scanned_by": [
		"MSCLyAWEbU6qKF8ULBXwKmj60WBvJsbnnByS"
	],
	"issue_type": [
		"VUL", "COO"
	]
}
```

```javascript
{
	"group_ids": [
		"group_id"
	],
	"status": [
		"Blocked"
	],
	"request_type": [
		"batch"
	]
}
```

Product Reports input Example.

![](https://uploads.developerhub.io/prod/97qW/n3o4ell0qx70cchnecn3q6v2oipjq81nlkhujjspluumjdeedvrgycez3j4p1nok.png)
