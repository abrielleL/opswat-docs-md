<!-- source: https://www.opswat.com/docs/filescan/3.1.1/adminguide/scan-url-API3l3 -->

# Scan URL with API

For the following examples we used [Postman](https://www.postman.com/) which is an API platform for building and using APIs.

## [Using the default settings](/docs/filescan/3.1.1/adminguide/scan-url-API3l3#using-the-default-settings)

### [Step 1 - Start a new request and select "POST"](/docs/filescan/3.1.1/adminguide/scan-url-API3l3#step-1---start-a-new-request-and-select-post)

### [Step 2 - Paste the Filescan URL](/docs/filescan/3.1.1/adminguide/scan-url-API3l3#step-2---paste-the-filescan-url)

Paste the Filescan URL to the "Enter request URL" field: <https://www.filescan.io/api/scan/url>

### [Step 3 - Add the target URL](/docs/filescan/3.1.1/adminguide/scan-url-API3l3#step-3---add-the-target-url)

Under Body tab select form-data.

Add the "url" key and under the value filed paste the URL you want to scan.

Give some additional parameters if you want.

### [Step 4 - Send the request with "Send" button](/docs/filescan/3.1.1/adminguide/scan-url-API3l3#step-4---send-the-request-with-send-button)

### [Step 5 - Copy the "flow_id"](/docs/filescan/3.1.1/adminguide/scan-url-API3l3#step-5---copy-the-flow_id)

If your request was success, you will get a similar answer:

JsonCopy{
"flow_id": "6405c213bfec0852a68fac4b",
"priority": {
"applied": 100,
"max_possible": 100
}
}

Copy the "flow_id" which is neccessary to polling the scan result.

### [**Step 6** - Get the result](/docs/filescan/3.1.1/adminguide/scan-url-API3l3#step-6---get-the-result)

Open a new request page and select the "GET" method (it's the default).

For the URL paste [*https://www.filescan.io/api/scan/63f633075dc36d90676259c6/report*](https://www.filescan.io/api/scan/63f633075dc36d90676259c6/report)*.*

Important!

Change the id beween scan/ and /report to your flow_id!

Click on Send button.

If the scan has not finished yet, you should get a similar result:

JsonCopy{
"flowId": "6405c3f993921fa04236c304",
"allFinished": false,
"allFilesDownloadFinished": false,
"reportsAmount": 1,
"priority": "max",
"pollPause": 5,
"reports": {
"5e50519e-a02c-4c84-ad17-8fe12c09f5ae": {
"overallState": "in_progress",
"positionInQueue": 0,
"finalVerdict": {
"verdict": "UNKNOWN",
"threatLevel": 0,
"confidence": 1
},
"filter_errors": [
"Path not found: ['vtRate']"
],
"file": {
"name": "https://www.google.com",
"hash": "ac6bb669e40e44a8d9f8f0c94dfc63734049dcf6219aac77f02edf94b9162c09",
"type": null
},
"filesDownloadFinished": false,
"created_date": "03/06/2023, 10:44:11",
"estimatedTime": "9",
"estimated_progress": 0.5002222326066759
}
}
}

The overallState field in the reports field tells you whether the scan has been completed or not. Wait some seconds and try to get the answer again by clicking the "Send" button. Repeat it until you get "success" state.

JsonCopy{
"flowId": "6405c213bfec0852a68fac4b",
"allFinished": true,
"allFilesDownloadFinished": true,
"reportsAmount": 1,
"priority": "max",
"pollPause": 5,
"reports": {
"30176f14-3202-4f38-8873-fe9340ca6c11": {
"overallState": "success_partial",
"positionInQueue": 0,
"finalVerdict": {
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
},
"vtRate": -1,
"file": {
"name": "https://www.google.com",
"hash": "ac6bb669e40e44a8d9f8f0c94dfc63734049dcf6219aac77f02edf94b9162c09",
"type": "other"
},
"filesDownloadFinished": true,
"created_date": "03/06/2023, 10:36:04",
"estimatedTime": "9",
"estimated_progress": 1.0
}
}
}

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
