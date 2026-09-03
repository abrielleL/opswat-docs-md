<!-- source: https://www.opswat.com/docs/cm/patch-management/patch-notification -->

# Patch Notification

**Patch Notifications **alert you when a key patch event needs attention, such as a deployment finishing, a device failing, a ring waiting for your approval, or a patch about to miss its SLA due date, so you don't have to keep checking the dashboard or patch lists yourself.

![](https://uploads.developerhub.io/prod/97qW/jcvdnjgj0qeygvqedwrayibhl5qv9mcfyf09i7w3itf8duuula750y1i87i22g14.png)

## Enable Patch Notification for Your Account

### Step 1. Create a Notification Group

1. To create a notification group, navigate to **Settings > Notification Groups**
2. Select **Create New Group **to begin

![](https://uploads.developerhub.io/prod/97qW/915svo9avjszd1u9kn3oc96o5186vp4vk7t1n3pp6rt6jgl6pcm0ycmsgspuksen.png)

3. In the notification group creation page, fill in configuration fields

| Field | Details |
| ---- | ---- |
| **Fill in the group's details** | ** **Fill in the group's details, including group name, email format, and group member emails ![](https://uploads.developerhub.io/prod/97qW/rpjnp5ypl5nwyxiqushfw2t00adbhk51fz41cxq7v6z6up3kw8vlve22153leitv.png) |
| **Choose event triggers** | Select **Patch Management** from the dropdown, then select the checkbox for each event you want this group to receive. You must select at least one ![](https://uploads.developerhub.io/prod/97qW/mult7gds8ipkoc6fxc6dbxc6a4kwzl1qvorlaxbutvhnn1ckko7phpmpzzkmrk74.png) |

4. Select **Save**

### Step 2. Assign Notification Group to Account

A notification group only sends alerts once it's assigned to your account.

1. In the left navigation, select **Settings > Globa**l
2. Open the **Notifications **tab
3. Select **Assign Group**, then choose the notification group you created. See [Create a new email notification group](https://www.opswat.com/docs/cm/reports-and-notification/email-notifications#create-a-new-email-notification-group) for detailed instructions.

![](https://uploads.developerhub.io/prod/97qW/giwq6t4lmyu03o4sy092vplzbe8qims5si0kurob2noabp7bmsrd6edq0ieu48y6.png)

## Enable Patch Notification for Webhook and SIEM Integration

You can configure patch notification to send email alert to the external security and logging tools your team already monitors.

### Webhook

**Step 1**: Create a webhook. See [Webhook](https://www.opswat.com/docs/cm/integrations/webhook) guidelines.

**Step 2**: Create a Notification Group

1. Navigate to Setting > Integration, choose** Group **under **Webhook Integration** tab
2. Click Create New Group, then fill in Group Name
3. Under Triggers, select Patch Management from the dropdown, then select the checkbox for each event you want this group to receive. You must select at least one.
4. Select the group and assign it to the account

![](https://uploads.developerhub.io/prod/97qW/valoukj1fgqbc6yrczy1a4favbfghn3q6t5fqb5li4p7y65e9r6k37rib5f41pp0.png)

### S3 Log Storage, Syslog, or Google Cloud Logging

1. Navigate to** Setting > Integration**
2. Choose corresponding tabs
3. Click Enable checkbox
4. Select patch events under Patch Management section
5. Click Save

![](https://uploads.developerhub.io/prod/97qW/jn21lgo3u0yupppkrdwjxoulayzjm6fxftft399gcpxt4xo56in7431x7iuqn1bj.png)

## How Notifications Show Up

| Locations | What You'll See |
| ---- | ---- |
| In-app bell ![](https://uploads.developerhub.io/prod/97qW/vmw020v62r773ojgrgoadznlhztnzukmu783knvlaw09mmynnsnjlmj5e7mqml3w.png) | A card with the event title, message, and timestamp. Select it to jump straight to the relevant page |
| Email ![](https://uploads.developerhub.io/prod/97qW/lhvydlep3cn5tslbfd7i2o9x1jeapd8uzd2ro2kpakqcb1coa6nckkkkcim3v4l0.png) | Subject line is the event title. The body shows a simple Event, Details, Time table |
| Webhook | An HTTP POST to your configured callback URL |
| S3 Log Storage, Syslog, Google Cloud Logging | A structured log entry alongside your other My OPSWAT Central Management events |

## Sample Notification Contents

### Email

**Subject: **[My OPSWAT Central Management] New Missing OS Patches detected

**My OPSWAT Central Management has automatically generated the following notification:**

| Event | **New Missing OS Patches detected** |
| ---- | ---- |
| Details | 5058383 - Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.435.97.0) - Current Channel (Broad) - Important severity. |
| Time | 2026-08-03 02:07:04 UTC |

 If you wish to no longer receive this email, please log into the My OPSWAT Central Management console, and adjust your email notification settings at Settings > Global > Notifications

**JSON**

```json
{
  "eventTitle": "New Missing OS Patches detected",
  "message": "5058383 - Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.435.97.0) - Current Channel (Broad) - Important severity.",
  "productName": "My OPSWAT Central Management",
  "time": "2026-08-03 02:07:04 UTC"
}
```

### Webhook

```json
[
  {
    "event_code": "OS_MISSING",
    "title": "New Missing OS Patches detected",
    "message": "New Missing OS Patches detected - 5058383 - Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.435.97.0) - Current Channel (Broad) - Important severity.",
    "subject": {
      "kb_id": "5058383",
      "patch_id": "patch_987",
      "name": "Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.435.97.0) - Current Channel (Broad)",
      "severity": "Important"
    }
  }
]
```

### Syslog

**SYSLOG**

```plaintext
<14> Aug 03 02:07:04 OPSWAT New OS missing patch detected - New Missing OS Patches detected: 5058383 - Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.435.97.0) - Current Channel (Broad)
```

**Common Event Format (CEF)**

```plaintext
CEF:0|OPSWAT|MOCM|<cm10Version>|account_events.os_missing|New OS missing patch detected|2|dvchost=<hostname> msg=New Missing OS Patches detected: 5058383 - Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.435.97.0) - Current Channel (Broad)
```

### S3 Log Storage / Google Cloud Logging

```json
{
  "type": "Patch Management",
  "log_type": "os_missing",
  "timestamp": "2026-08-03T02:07:04Z",
  "details": "New Missing OS Patches detected: 5058383 - Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.435.97.0) - Current Channel (Broad)",
  "severity": "Important"
}
```
