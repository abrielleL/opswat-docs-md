<!-- source: https://www.opswat.com/docs/filescan/3.1.1/adminguide/scan-file-APIc3v -->

# Upload file with API

For the following examples we used [Postman](https://www.postman.com/) which is an API platform for building and using APIs.

## [Using the default settings](/docs/filescan/3.1.1/adminguide/scan-file-APIc3v#using-the-default-settings)

### [Step 1 - Start a new request and select "POST"](/docs/filescan/3.1.1/adminguide/scan-file-APIc3v#step-1---start-a-new-request-and-select-post)

### Step 2 - Paste the Filescan URL to the "Enter request URL" field: <https://www.filescan.io/api/scan/file>

### [Step 3 - Upload the file and set parameters](/docs/filescan/3.1.1/adminguide/scan-file-APIc3v#step-3---upload-the-file-and-set-parameters)

Under Body tab select form-data.

Add a "file" key and change the type to "File".

Under the value filed select the target file.

Give some additional parameters if you want.

### [Step 4 - Send the request with "Send" button](/docs/filescan/3.1.1/adminguide/scan-file-APIc3v#step-4----send-the-request-with-send-button)

### [Step 5 - Copy the "flow_id"](/docs/filescan/3.1.1/adminguide/scan-file-APIc3v#step-5---copy-the-flow_id)

If your request was success, you will get a similar answer:

JsonCopy{
"flow_id": "63f633075dc36d90676259c6",
"priority": {
"applied": 100,
"max_possible": 100
}
}

Copy the "flow_id" which is neccessary to polling the scan result.

### [Step 6 - Get the result](/docs/filescan/3.1.1/adminguide/scan-file-APIc3v#step-6---get-the-result)

Open a new request page and select the "GET" method (it's the default).

For the URL paste *[__*[*https://www.filescan.io/api/scan/_63f633075dc36d90676259c6*](https://www.filescan.io/api/scan/_63f633075dc36d90676259c6)/report_](<https://www.filescan.io/api/scan/63f633075dc36d90676259c6/report>)*.*

Important!

Change the id beween scan/ and /report to your flow_id!

Click on Send button.

If the scan has not finished yet, you should get a similar result:

JsonCopy{
"flowId": "63f633075dc36d90676259c6",
"allFinished": false,
"allFilesDownloadFinished": false,
"reportsAmount": 1,
"priority": "max",
"pollPause": 5,
"fileSize": 13370880,
"fileReadProgressBytes": 13370880,
"reports": {
"d59e12bb-f599-4dfa-b682-253a5dacf564": {
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
"name": "bad_file.exe",
"hash": "834d1dbfab8330ea5f1844f6e905ed0ac19d1033ee9a9f1122ad2051c56783dc",
"type": null
},
"filesDownloadFinished": false,
"created_date": "02/22/2023, 16:01:29",
"estimatedTime": "2",
"estimated_progress": 1.0
}
}
}

The overallState field in the reports field tells you whether the scan has been completed or not. Wait some seconds and try to get the answer again by clicking the "Send" button. Repeat it until you get "success" state.

JsonCopy{
"flowId": "63f63c57a6ba2f75a97a1f81",
"allFinished": true,
"allFilesDownloadFinished": true,
"reportsAmount": 1,
"priority": "max",
"pollPause": 5,
"fileSize": 13370880,
"fileReadProgressBytes": 13370880,
"reports": {
"d59e12bb-f599-4dfa-b682-253a5dacf564": {
"overallState": "success",
"positionInQueue": 0,
"finalVerdict": {
"verdict": "MALICIOUS",
"threatLevel": 1,
"confidence": 1
},
"vtRate": -1,
"file": {
"name": "bad_file.exe",
"hash": "834d1dbfab8330ea5f1844f6e905ed0ac19d1033ee9a9f1122ad2051c56783dc",
"type": "pe"
},
"filesDownloadFinished": true,
"created_date": "02/22/2023, 16:01:29",
"estimatedTime": "2",
"estimated_progress": 1.0
}
}
}

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
