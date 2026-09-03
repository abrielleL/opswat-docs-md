<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/siem-integration -->

# SIEM Integration

MetaDefender IT Access features an SIEM (Security Information Event Management) integration that can be found under **Settings > Integrations > SIEM Integration**.

When enabled, MetaDefender IT Access utilizes the established S3 buckets through AWS (set up by the administrator) for log storage to collect analytical data about the associated account and to alert the administrators about any triggered events selected in the integration. By using the integration, administrators can track and monitor any patterns of activity that can become a potential threat to their infrastructure.

## [Setting up the integration](/docs/macloud-sdp/configuration---management/siem-integration#setting-up-the-integration)

To set up the SIEM integration, administrators should proceed with the following steps:

- Sign into MetaDefender IT Access. Navigate to **Settings > Integrations > SIEM Integration.**
- Select **Enable Log Storage**.
- Fill in the required fields based on the associated AWS account (For more information on setting this up, please review [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-walkthroughs-managing-access-example1.html)).
- Select the desired format for the logs (JSON or SYSLOG).
- Select the events that will trigger an email notification. To save this configuration, it is required to select at least one event.
- When completed, select **Save**.

*Note: The sync of data between* *MetaDefender IT Access*_' databases and the S3 bucket is scheduled for every 5 minutes._

## [Receiving Logs](/docs/macloud-sdp/configuration---management/siem-integration#receiving-logs)

Once the initial setup is completed in MetaDefender IT Access, administrators will be able to access their logs from their S3 bucket after a triggered event. From the S3 bucket, administrators can download logs for reviewal, auditing, or historical purposes. As mentioned above, the logs from triggered events come in two formats: JSON and SYSLOG. Administrators can select based on their preference as the contents remain the same.

### [JSON](/docs/macloud-sdp/configuration---management/siem-integration#json)

JsonCopy{
"log_type": "exempt_all",
"device_name": "Cuong Ba",
"device_id": "cuongbavuacakhia1657786592",
"last_seen": "2022-07-15T08:55:12.279Z",
"device_group": "Default",
"details": "Device Cuong Ba was exempted by Phuong Phuong Phuong Phuong Phuong(phuongphweekly@gmail.com)24 hour(s)",
"type": "Device",
"device_username": "Wilfred Hoeger",
"timestamp": "2022-07-15T08:55:12.279Z"
}
{
"log_type": "unexempt",
"device_name": "Cuong Ba",
"device_id": "cuongbavuacakhia1657868171",
"last_seen": "2022-07-15T08:55:25.377Z",
"device_group": "Default",
"details": "Device Cuong Ba was unexempted by Phuong Phuong Phuong Phuong Phuong(phuongphweekly@gmail.com)",
"type": "Device",
"device_username": "Nicholas Roob",
"timestamp": "2022-07-15T08:55:25.377Z"
}
### [SYSLOG](/docs/macloud-sdp/configuration---management/siem-integration#syslog)

SyslogCopy"log_type":"config","details":"Administrator Phuong Phuong Phuong Phuong Phuong (phuongphweekly@gmail.com) changed Settings - Integrations - SIEM Integration ","admin_name":"Phuong Weekly 1","type":"Account","event":"Configuration Change","admin_email":"phuongphweekly@gmail.com","timestamp":"2022-07-15T11:19:41.629Z"
"log_type":"added","device_name":"Cuong Ba","device_id":"cuongbavuacakhia1657883993","last_seen":"2022-07-15T11:19:54.239Z","device_group":"Default","details":"OPSWAT Client (Version 7.6.586.1) Cuong Ba Installed$0","type":"Device","device_username":"Christy Stokes","timestamp":"2022-07-15T11:19:54.239Z"
## [Understanding Logs](/docs/macloud-sdp/configuration---management/siem-integration#understanding-logs)

Within these logs, there are key values that administrators can use when reviewing the data to further track down an affected device or account change.

### [Device](/docs/macloud-sdp/configuration---management/siem-integration#device)

| Key | Data Type | Description |
| --- | --- | --- |
| timestamp | string | timestamp when the event occurs |
| log_type | string | Log type :   - `compliant`: a device was considered as compliant - `noncompliant`: a device was considered as non-compliant - `allow_device_access`: allowed device access - `block_device_access`: blocked device access - `deleted`: a device was deleted by an admin - `added`: a device was enrolled to an account - `critical_found`: a device reported critical issues - `process_scan_infection_found`: a device reported threats - `critical_cleared`: a device reported no more critical issues - `report_no_threat`: a device reported no more threats - `exempt_all`: an admin exempted a device - unexempt: an admin unexempted a device - `access_granted`: a device was granted temporary access to a protected app - `access_revoked`: a device was revoked a temporary access to a protected app - `unknown_device_detected`: an unknown device detected - `unseen`: device deleted by unseen setting - `deleted_user`: device uninstalled by a user |
| details | string | Event details |
| device_id | string | ID of a device that the event occurred on |
| device_name | string | Name of device that the event occurred on |
| device_username | string | Name of user who logged into a device when the event occurred |
| device_group | string | A device's group name |

### [Account](/docs/macloud-sdp/configuration---management/siem-integration#account)

| Key | Data Type | Description |
| --- | --- | --- |
| timestamp | string | timestamp when the event occurs |
| event | string | Description of log type |
| details | string | Event details |
| admin_name | string | Name of an admin who is related to the event |
| admin_email | string | Email of an admin who is related to the event |
| log_type | string | Log type :   - `config`: an admin changed configuration - `logon`: an admin logged on - `logout`: and admin logged off - `license_left`: Account has [x] % license(s) left |
