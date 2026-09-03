<!-- source: https://www.opswat.com/docs/mdss/configuration/event-based-real-time-cloud-functions-examples -->

# Event-Based Real-Time Cloud Functions Examples

## [Google Cloud Function Setup](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples#google-cloud-function-setup)

1. Configure the Cloud Run with the `google.cloud.storage.object.v1.finalizedtrigger` to process newly added objects.
2. Python Function Example:

PythonCopyimport functions_framework
import json
import requests
import os
@functions_framework.cloud_event
def hello_gcs(cloud_event):
try:
name = cloud_event.data['protoPayload']['request']['insertObjectSpec']['resource']['name']
except KeyError as e:
print(f"Missing key in event data: {e}")
return
request_body = {
'storageClientId': os.getenv('STORAGECLIENTID'),
'metadata': json.dumps({'name': name})
}
requests.post(
os.getenv('APIENDPOINT'),
headers={'ApiKey': os.getenv('APIKEY')},
json=request_body
)

3. Requirements.txt example:

requirements.txtCopyfunctions-framework==3.*
requests
### [Alibaba Cloud Function Setup](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples#alibaba-cloud-function-setup)

1. Follow the official Alibaba Cloud documentation to create a compute function with an OSS trigger: <https://www.alibabacloud.com/help/en/function-compute/latest/configure-an-oss-trigger>
2. Specify the bucket to monitor and subscribe to the `oss:ObjectCreated:*` event.
3. Python Function Example:

PythonCopyimport oss2, json, os
import requests
def handler(event, context):
for eventRecord in json.loads(event)['events']:
requests.post(os.getenv('APIENDPOINT', ""), headers={'ApiKey':os.getenv('APIKEY', "")}, json = {'metadata': json.dumps(eventRecord), 'storageClientId': os.getenv('STORAGECLIENTID', "") })
### [Wasabi Function Setup](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples#wasabi-function-setup)

1. Follow the official Wasabi documentation to create an event notification: <https://docs.wasabi.com/v1/docs/event-notifications-bucket>
2. Establish a connection with a service capable of sending requests to MetaDefender Storage Security (MDSS).
3. The Wasabi documentation example uses AWS SNS, which can be integrated with AWS Lambda (see Amazon S3 Lambda Function Setup: [How do I configure Event Notifications on my Wasabi bucket using AWS SNS?](https://docs.wasabi.com/v1/docs/en/how-do-i-configure-event-notifications-on-my-wasabi-bucket-using-aws-sns?highlight=event%20notification)

### [S3 Compatible function setup](/docs/mdss/configuration/event-based-real-time-cloud-functions-examples#s3-compatible-function-setup)

- Event-based real-time processing configuration varies for different S3-compatible services.
- Most S3-compatible services offer event notification similar to Wasabi.
- The service must send a request to the MDSS endpoint: `http(s)://{baseurl}/api/webhook/realtime` with the appropriate request body:

JsonCopy{
"storageClientId": [Storage Client Id],
"metadata": "{'s3': { 'object': {'key': [Object Path] }}}"
}
