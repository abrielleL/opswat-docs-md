<!-- source: https://www.opswat.com/docs/cm/integrations/s3-log-storage -->

# S3 Log Storage

My OPSWAT Central Management offers an SIEM (Security Information Event Management) integration that can be found under **Settings > Integrations > S3 Log Storage**.

When enabled, My OPSWAT Central Management utilizes the established S3 buckets through AWS (set up by the administrator) for log storage to collect analytical data about the associated account and to alert the administrators about any triggered events selected in the integration. By using the integration, administrators can track and monitor any patterns of activity that can become a potential threat to their infrastructure.

## Setting up the integration

To set up the SIEM integration, administrators should proceed with the following steps:

- Log into My OPSWAT Central Management. Navigate to **Settings > Integrations > S3 Log Storage.**
- Select **Enable AWS S3 Log Storage Endpoint**.
- Fill in the required fields based on the associated AWS account (For more information on setting this up, please review [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-walkthroughs-managing-access-example1.html)).
- Select the desired format for the logs (JSON or SYSLOG).
- Select the events that will trigger an email notification. To save this configuration, it is required to select at least one event.
- When completed, select **Save**.

*Note: The sync of data between* *My OPSWAT Central Management and the S3 bucket is scheduled for every 5 minutes.*

![](https://uploads.developerhub.io/prod/97qW/rg3vl7c7klhbeg7etc709b12dlo1rhslw7af9lkrhhlr2ks36xhmxpt3ktse31hb.png)

## Receiving Logs

Once the initial setup is completed in My OPSWAT Central Management, administrators will be able to access their logs from their S3 bucket after a triggered event. From the S3 bucket, administrators can download logs for reviewal, auditing, or historical purposes. As mentioned above, the logs from triggered events come in two formats: JSON and SYSLOG. Administrators can select based on their preference as the contents remain the same.

### JSON

```json
{
  "log_type": "exempt_all",
  "device_name": "LTES156H",
  "device_id": "LTES156H",
  "last_seen": "2022-07-15T08:55:12.279Z",
  "device_group": "Default",
  "details": "Device LTES156H was exempted by Alice (alice@company.com) 24 hour(s)",
  "type": "Device",
  "device_username": "Wilfred Hoeger",
  "timestamp": "2022-07-15T08:55:12.279Z"
}
```

### SYSLOG

```json
"log_type":"config","details":"Administrator Alice (alice@company.com) changed  Settings  - Integrations - SIEM Integration ","admin_name":"Alice Bob","type":"Account","event":"Configuration Change","admin_email":"alice@company.com","timestamp":"2022-07-15T11:19:41.629Z"
```

## Understanding Logs

Within these logs, there are key values that administrators can use when reviewing the data to further track down an affected device or account change.

### Device

| Key | Data Type | Description |
| ---- | ---- | ---- |
| timestamp | string | timestamp when the event occurs |
| log_type | string | Log type : - `compliant`: a device was considered as compliant - `noncompliant`: a device was considered as non-compliant - `allow_device_access`: allowed device access - `block_device_access`: blocked device access - `deleted`: a device was deleted by an admin - `added`: a device was enrolled to an account - `critical_found`: a device reported critical issues - `process_scan_infection_found`: a device reported threats - `critical_cleared`: a device reported no more critical issues - `report_no_threat`: a device reported no more threats - `exempt_all`: an admin exempted a device - unexempt: an admin unexempted a device - `access_granted`: a device was granted temporary access to a protected app - `access_revoked`: a device was revoked a temporary access to a protected app - `unknown_device_detected`: an unknown device detected - `unseen`: device deleted by unseen setting - `deleted_user`: device uninstalled by a user |
| details | string | Event details |
| device_id | string | ID of a device that the event occurred on |
| device_name | string | Name of device that the event occurred on |
| device_username | string | Name of user who logged into a device when the event occurred |
| device_group | string | A device's group name |

### Account

| Key | Data Type | Description |
| ---- | ---- | ---- |
| timestamp | string | timestamp when the event occurs |
| event | string | Description of log type |
| details | string | Event details |
| admin_name | string | Name of an admin who is related to the event |
| admin_email | string | Email of an admin who is related to the event |
| log_type | string | Log type : - `config`: an admin changed configuration - `logon`: an admin logged on - `logout`: and admin logged off - `license_left`:  Account has [x] % license(s) left |
