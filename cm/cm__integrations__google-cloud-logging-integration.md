<!-- source: https://www.opswat.com/docs/cm/integrations/google-cloud-logging-integration -->

# Google Cloud Logging Integration

My OPSWAT Central Management offers an SIEM (Security Information Event Management) integration that can be found under **Settings > Integrations > Google Cloud Logging**.

When enabled, My OPSWAT Central Management utilizes the established GCP buckets through Google Cloud (set up by the administrator) for log storage to collect analytical data about the associated account and to alert the administrators about any triggered events selected in the integration. By using the integration, administrators can track and monitor any patterns of activity that can become a potential threat to their infrastructure.

Before you begin, make sure that:

- You have an active **Google Account** with access to Google Cloud services.
- Your **My OPSWAT Central Management** account has the **Google Cloud Logging** feature enabled.

## Create a Google Cloud Project

- Go to [Google Cloud Console](https://console.cloud.google.com/).
- Click **Select a project** → **New Project**.
- Enter your project name and other details.
- Click **Create** to finish.

## Create a Service Account Key

- In the same project, go to **IAM & Admin → Service Accounts**.
- Click **Create Service Account**.
- Enter the service account name and description → **Create and continue**.
- Assign a role:
  - **Owner** or **Editor** for write permissions.
  - **Viewer** or **Browser** for read-only access → Click **Continue**.
- (Optional) Add users under *Grant access to this service account*.
- Click **Done**.

## Create the Private Key

- In the Service Accounts list, select your new account.
- Click **Actions → Manage Keys → Add Key → Create New Key**.
- Choose **JSON** → **Create**.
- A `.json` key file will be downloaded automatically — **keep it safe**, as you’ll need it later.

## Integrate with My OPSWAT Central Management

- Log in to [My OPSWAT Central Management](https://my.us.opswat.com/).
- Go to **Settings → Integrations → Google Cloud Logging**.

![](https://uploads.developerhub.io/prod/97qW/c8t1occm65nkhkd5b7icou5hwi6pzzwrbr4az99yf5gijb1yhrkt7aq2g4o8kkij.png)

- Enable the integration.
- Fill in the configuration fields:

| Field | Description |
| ---- | ---- |
| Project ID | Your Google Cloud Project ID was created earlier |
| Log Name | Unique name for the log (defines where and what type of log it is) |
| Severity | Classifies the importance of each event |
| Service Account Key | Upload the JSON file you downloaded earlier |

- Click **Test Connection**.
  - If the test is successful → your integration setup is complete!

![](https://uploads.developerhub.io/prod/97qW/ox05nw4yjwo02v1de4uj9f1vc8rowun2qwp55yh3bplvggzxdk7azn3arys9239p.png)

## Configure Trigger Events

- Choose the log format: **JSON** or **SYSLOG**.
- Select which events will trigger logging.
- Click **Save**.

Once configured, logs will automatically be sent to Google Cloud Logging.

![](https://uploads.developerhub.io/prod/97qW/td2ajrx9g1knoreaeualgkr4scjbz4xauj2n1x7je61725zsg9zydrrw7j8y8qyn.png)

## Receiving Logs

- Go to [Google Cloud Console → Log Explorer](Google Cloud Console → Log Explorer).
- Select your project.
- Choose the **Log Name** configured in OCM.
- View and analyze log entries.

#### JSON

```javascript
{
	"admin_name": "admin",
	"log_type": "config",
	"admin_email": "admin@opswat.com",
	"timestamp": "2025-10-22T10:54:28.941+00:00",
	"event": "Configuration Change",
	"type": "Account",
	"details": "Administrator admin changed Settings - Integrations - Google Cloud Logging Storage"
}
{
    "timestamp": "2025-10-21T10:39:37.568+00:00",
    "details": "Daily malware found",
    "device_id": "DEB-id1761042895",
    "device_group": "DEB-V61761042895-1711423509228",
    "device_username": "N/A",
    "device_name": "DEB-V61761042895_KA",
    "log_type": "process_scan_infection_found",
    "last_seen": "2025-10-21T10:38:58.338+00:00",
    "type": "Device"
  }
```

#### Syslog

```javascript
"log_type":"config","details":"Administrator admin (admin@opswat.com) changed Settings - Integrations - Google Cloud Logging Storage","admin_name":"son ngo","type":"Account","event":"Configuration Change","admin_email":"admin@opswat.com","timestamp":"2025-10-22T10:48:14.227+00:00"

"log_type":"process_scan_infection_found","device_name":"MacPer-name1761042880","device_id":"MacPer-id1761042880","last_seen":"2025-10-21T10:37:09.477+00:00","device_group":"MacPer-name1761042880-1619076505417","details":"Daily malware found","type":"Device","device_username":"AnhBui","timestamp":"2025-10-21T10:38:51.972+00:00"
```

#### Check Result on Google Cloud

Once the events are triggered, Central Management will forward the logs to GCP. As an administrator, you can review the results in GCP as shown below.

![](https://uploads.developerhub.io/prod/97qW/17t2kfuq8k433wf0qk2rrucu25mn4pscfi7burwzb5dk843xpdrnb3weo6hqlwio.png)

![](https://uploads.developerhub.io/prod/97qW/unbf1f6yfjmhlhmr0tw07jqrci0dtv3pgpwzn00rcb855zn3btuqww6cbkigk8bi.png)
