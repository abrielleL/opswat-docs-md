<!-- source: https://www.opswat.com/docs/filescan/3.1.1/integrations/splunk-soar -->

# Splunk SOAR

Splunk SOAR (Cloud) delivers the benefits of SOAR as a cloud-based service. With Splunk SOAR (Cloud), you gain the functionality of a security orchestration, automation, and response (SOAR) system that is delivered as a software-as-a-service (SaaS) solution hosted and managed by Splunk. By integrating **MetaDefender Sandbox** (previously known as OPSWAT Filescan Sandbox) with Splunk SOAR, security teams can automate the process of scanning files for malware and other security threats. This integration allows security teams to quickly and easily scan files for potential threats, and take immediate action to mitigate any risks that are identified.

Utilizing this integration, you can send a file or URL scan request from Splunk SOAR to any sandbox instance, as well as search for previously scanned reports and perform a quick file, ip, domain or URL reputation lookup.

You can find more information about Splunk SOAR [here](https://www.splunk.com/en_us/products/splunk-security-orchestration-and-automation.html).

MetaDefender Sandbox integration in Splunkbase marketplace available [here](https://splunkbase.splunk.com/app/6942).

## [Installation](/docs/filescan/3.1.1/integrations/splunk-soar#installation)

You can install MetaDefender Sandbox from Splunkbase or from Splunk SOAR directly.

#### [Install from Splunk SOAR](/docs/filescan/3.1.1/integrations/splunk-soar#install-from-splunk-soar)

In Splunk SOAR go to Apps and select "New Apps".

Then search for MetaDefender Sandbox and Install it:

#### [Install from Splunkbase](/docs/filescan/3.1.1/integrations/splunk-soar#install-from-splunkbase)

Download MetaDefender Sandbox from Splunkbase: <https://splunkbase.splunk.com/app/6942>

And in Splunk under Apps select "Insall App":

After that drag and drop the downloaded app. And click to "Install"

## [Configuration](/docs/filescan/3.1.1/integrations/splunk-soar#configuration)

After installed, you can find MetaDefender Sandbox app under the "Unconfigured Apps" list:

Under 'CONFIGURE NEW ASSET' fill the required fileds.

Under *Asset Info* tab, please fill the asset name and description:

After this, configure the connection under *Asset Settings* tab:

Note

MetaDefender Sandbox API key is required to use the integration.

You can use the Activation Key that you received from your OPSWAT Sales Representative, and follow the instructions on the [License Activation](https://docs.opswat.com/filescan/installation/license-activation) page or you can create an API key on the [Community site](https://www.filescan.io/users/profile) under API Key tab.

You need to add your API key, and if you have on-prem version of MetaDefender Sandbox, you can add your own server's URL. The default URL is the Filescan.io free community.

After saving the settings you can use the asset.

### [Testing the asset](/docs/filescan/3.1.1/integrations/splunk-soar#testing-the-asset)

You can test the connection of your asset under the view menu:

For that, select Actions -> test connectivity at left and on the right side select your asset. After clicking on '*Test Action*' button a message will appear. The following message indicates that the setup was successful:

`[USERNAME] API key has been set successfully`

## [Available actions](/docs/filescan/3.1.1/integrations/splunk-soar#available-actions)

### [detonate url](/docs/filescan/3.1.1/integrations/splunk-soar#detonate-url)

Scan URL resource with Sandbox POST - Scan URL

#### [Parameters](/docs/filescan/3.1.1/integrations/splunk-soar#parameters)

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| url | The URL to submit |  | yes |
| password | Custom password, in case uploaded archive is protected |  |  |
| is private | If file should not be available for download by other users |  |  |
| description | Uploaded file/url description |  |  |

Example outputCopy{
"identifier": "detonate_url",
"result_data":
[
{
"data":
[
{
"finalVerdict":
{
"verdict": "BENIGN",
"threatLevel": -1,
"confidence": 1
},
"allTags":
[
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "e3c06909f3ed9d87e05ded9be95b4d990734bdb6a002201e3d84b4df3ee3a9a5",
"isRootTag": true,
"tag":
{
"name": "html",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "e3c06909f3ed9d87e05ded9be95b4d990734bdb6a002201e3d84b4df3ee3a9a5",
"isRootTag": true,
"tag":
{
"name": "vbs",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
}
],
"overallState": "success_partial",
"taskReference":
{
"name": "transform-file",
"additionalInfo":
{
"submitName": "https://www.google.com",
"submitTime": 1686050320059,
"digests":
{
"SHA-256": "ac6bb669e40e44a8d9f8f0c94dfc63734049dcf6219aac77f02edf94b9162c09"
}
},
"ID": "fab3fbea-9dc2-409b-8a69-fef821bbb306",
"state": "SUCCESS",
"resourceReference":
{
"type": "TRANSFORM_FILE",
"name": "file",
"ID": "231172d3-3bdb-4dae-95f4-2ac95a115d37"
},
"opcount": 1,
"processTime": 18201
},
"subtaskReferences":
[
{
"name": "osint",
"additionalInfo": "231172d3-3bdb-4dae-95f4-2ac95a115d37",
"ID": "8a7e8007-28cc-4f90-998b-c449d84abad9",
"state": "SUCCESS",
"resourceReference":
{
"type": "OSINT",
"name": "osint",
"ID": "090209d7-0c41-431a-b0a8-7733c8ee8068"
},
"opcount": 4,
"processTime": 1007
},
{
"name": "url-render",
"additionalInfo": 1,
"ID": "384b3aa7-8b65-4014-a7e0-e2f1fdab8325",
"state": "SUCCESS",
"resourceReference":
{
"type": "URL_RENDER",
"name": "url-render",
"ID": "d09599d7-3983-41c9-b801-b4dd63985106"
},
"opcount": 1,
"processTime": 15055
},
{
"name": "domain-resolve",
"additionalInfo": 11,
"ID": "b6b027d4-25e8-44ab-a108-000841637187",
"state": "SUCCESS",
"resourceReference":
{
"type": "DOMAIN_RESOLVE",
"name": "domain-resolve",
"ID": "1eb5ac64-0831-4960-9081-b29f97c65b78"
},
"opcount": 10,
"processTime": 3595
},
{
"name": "file-download",
"additionalInfo": 17,
"ID": "c7450844-acc5-45af-826d-60e0ed12a028",
"state": "SUCCESS_PARTIAL",
"resourceReference":
{
"type": "FILE_DOWNLOAD",
"name": "file-download",
"ID": "88885ea4-6a75-4ac1-98c4-871053939b1d"
},
"opcount": 11,
"processTime": 54680
},
{
"name": "osint-ex",
"additionalInfo": "URL",
"ID": "eeadea1d-c7a9-4839-8ca3-257653355375",
"state": "SUCCESS",
"resourceReference":
{
"type": "OSINT",
"name": "osint",
"ID": "9d31cf5a-2d87-4e92-981a-92eef3e59a47"
},
"opcount": 32,
"processTime": 1022
},
{
"name": "osint-ex",
"additionalInfo": "DOMAIN",
"ID": "612fc915-ae5c-462a-a145-c193f047600e",
"state": "SUCCESS",
"resourceReference":
{
"type": "OSINT",
"name": "osint",
"ID": "13e975c8-7ca3-4c1f-953d-773d4433c764"
},
"opcount": 0,
"processTime": 10
},
{
"name": "osint-fuzzyhash",
"additionalInfo": "231172d3-3bdb-4dae-95f4-2ac95a115d37",
"ID": "d5f24362-bc61-451a-81e0-1d238d1e0fee",
"state": "SUCCESS",
"resourceReference":
{
"type": "OSINT",
"name": "osint",
"ID": "fcad21a0-2586-4592-9397-715c7873aacd"
},
"opcount": 2,
"processTime": 1007
}
],
"allSignalGroups":
[
{
"identifier": "S007",
"description": "Found a Windows desktop utility string artifact",
"averageSignalStrength": 0.1,
"peakSignalStrength": 0.1,
"finalSignalStrength": 0.1,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"services\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "938c9153d8e4a251571b8aff2d7e7b18c262a532c8227ed656d5c1801386ab6d"
},
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"print\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "938c9153d8e4a251571b8aff2d7e7b18c262a532c8227ed656d5c1801386ab6d"
}
]
},
{
"identifier": "D001",
"description": "Found a domain referencing a social media service",
"averageSignalStrength": 0.1,
"peakSignalStrength": 0.1,
"finalSignalStrength": 0.1,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found domain \"facebook.com\"",
"originPath": "file.extractedDomains.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "938c9153d8e4a251571b8aff2d7e7b18c262a532c8227ed656d5c1801386ab6d"
},
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found domain \"instagram.com\"",
"originPath": "file.extractedDomains.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "938c9153d8e4a251571b8aff2d7e7b18c262a532c8227ed656d5c1801386ab6d"
},
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found domain \"linkedin.com\"",
"originPath": "file.extractedDomains.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "938c9153d8e4a251571b8aff2d7e7b18c262a532c8227ed656d5c1801386ab6d"
},
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found domain \"twitter.com\"",
"originPath": "file.extractedDomains.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "938c9153d8e4a251571b8aff2d7e7b18c262a532c8227ed656d5c1801386ab6d"
}
]
},
{
"identifier": "S049",
"description": "Found a base64 encoded http(s) URL prefix",
"averageSignalStrength": 0.25,
"peakSignalStrength": 0.25,
"finalSignalStrength": 0.25,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.2,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"aHR0cHM6Ly93d3c\" in string \"EyA8ACAaIBAhADIhcAAQIDBAUGBwgJCgsMDQ4PEBESExQVFjDoAjisAko2Y3Jpc2lzX2FtYmllbnRfYWxlcnRzX2luX2FsbF96b29tc19mb3JfdGVzdGluZ19vdmVybG (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "59374c3caafda4ec5f4572f49d0d08a017769ad327d1aa81e8224f64cdff4e3b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"aHR0cHM6Ly93d3c\" in string \"N0YXRpYy5jb20vbWFwcy9yZXMvQ29tcGFjdExlZ2VuZC1Sb2FkbWFwU2F0ZWxsaXRlLWEyYjkxYzk4YmYwMTk4MjdkMWNkZmQ2ZWU3OGUxMmNkEmQIAhJgaHR0cHM6Ly (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "59374c3caafda4ec5f4572f49d0d08a017769ad327d1aa81e8224f64cdff4e3b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"aHR0cHM6Ly93d3c\" in string \"ZlZTc4ZTEyY2QSZQgJEmFodHRwczovL3d3dy5nc3RhdGljLmNvbS9tYXBzL3Jlcy9Db21wYWN0TGVnZW5kLVJvYWRtYXBBbWJpYWN0aXZlLWEyYjkxYzk4YmYwMTk4Mj (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "59374c3caafda4ec5f4572f49d0d08a017769ad327d1aa81e8224f64cdff4e3b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"aHR0cHM6Ly93d3c\" in string \"dCaXQtYTJiOTFjOThiZjAxOTgyN2QxY2RmZDZlZTc4ZTEyY2QSZggREmJodHRwczovL3d3dy5nc3RhdGljLmNvbS9tYXBzL3Jlcy9Db21wYWN0TGVnZW5kLU5hdmlnYX (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "59374c3caafda4ec5f4572f49d0d08a017769ad327d1aa81e8224f64cdff4e3b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"aHR0cHM6Ly93d3c\" in string \"ovL3d3dy5nc3RhdGljLmNvbS9tYXBzL3Jlcy9Db21wYWN0TGVnZW5kLUJhc2VtYXBFZGl0aW5nU2F0ZWxsaXRlLWEyYjkxYzk4YmYwMTk4MjdkMWNkZmQ2ZWU3OGUxMm (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "59374c3caafda4ec5f4572f49d0d08a017769ad327d1aa81e8224f64cdff4e3b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"aHR0cHM6Ly93d3c\" in string \"NkZmQ2ZWU3OGUxMmNkEl8IIRJbaHR0cHM6Ly93d3cuZ3N0YXRpYy5jb20vbWFwcy9yZXMvQ29tcGFjdExlZ2VuZC1Sb2FkbWFwRGFyay1hMmI5MWM5OGJmMDE5ODI3ZD (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "59374c3caafda4ec5f4572f49d0d08a017769ad327d1aa81e8224f64cdff4e3b"
}
]
},
{
"identifier": "D006",
"description": "Found an unusual long domain part",
"averageSignalStrength": 0.25,
"peakSignalStrength": 0.25,
"finalSignalStrength": 0.25,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.2,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found domain part \"u003d78c11b69-98fe-41ed-b729-b88f8cff0efc\" in \"u003d78c11b69-98fe-41ed-b729-b88f8cff0efc.streamplease.net\"",
"originPath": "file.extractedDomains.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "59374c3caafda4ec5f4572f49d0d08a017769ad327d1aa81e8224f64cdff4e3b"
}
]
},
{
"identifier": "S049",
"description": "Found a base64 encoded http(s) URL prefix",
"averageSignalStrength": 0.25,
"peakSignalStrength": 0.25,
"finalSignalStrength": 0.25,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.2,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"aHR0cDovL3d3dy\" in string \"etween;padding:0 24px 14px}.HUYFt .hXs2T,.HUYFt .M2nKge{line-height:48px}@media all and (min-width:601px){.HUYFt{padding-left:0; (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "c4492654b5345619c304d01adcc1de60df68a74d20d7dacac42a1940f600c783"
}
]
},
{
"identifier": "S050",
"description": "Contains a HTTP refresh header",
"averageSignalStrength": 0.25,
"peakSignalStrength": 0.25,
"finalSignalStrength": 0.25,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.2,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"meta http-equiv=\"refresh\"\" in string \"/*# sourceURL=/_/mss/boq-identity/_/ss/k=boq-identity.AccountsSignInUi.u0mxmDVVd1k.L.W.O/am=BznH4QMAFP8BAhBAoEABAAAAAAAAAAAIw1KA (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "c4492654b5345619c304d01adcc1de60df68a74d20d7dacac42a1940f600c783"
}
]
},
{
"identifier": "S049",
"description": "Found a base64 encoded http(s) URL prefix",
"averageSignalStrength": 0.25,
"peakSignalStrength": 0.25,
"finalSignalStrength": 0.25,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.2,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"aHR0cDovL3d3dy\" in string \"x-wrap:wrap;font-size:12px;justify-content:space-between;padding:0 24px 14px}.HUYFt .hXs2T,.HUYFt .M2nKge{line-height:48px}@medi (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "7c6cd686499f07979f17e803733cc7341cca0f20363f00a853b6ef7d6923234b"
}
]
},
{
"identifier": "S050",
"description": "Contains a HTTP refresh header",
"averageSignalStrength": 0.25,
"peakSignalStrength": 0.25,
"finalSignalStrength": 0.25,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.2,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found artifact \"meta http-equiv=\"refresh\"\" in string \"s intuitive, efficient, and useful. 15 GB of storage, less spam, and mobile access.\\\"><noscript><meta http-equiv=\\\"refresh\\\" conten (..)\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "7c6cd686499f07979f17e803733cc7341cca0f20363f00a853b6ef7d6923234b"
}
]
},
{
"identifier": "S007",
"description": "Found a Windows desktop utility string artifact",
"averageSignalStrength": 0.25,
"peakSignalStrength": 0.25,
"finalSignalStrength": 0.25,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.2,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"find\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"help\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"sort\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"finger\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"find\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"change\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
},
{
"strength": 0.25,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found string artifact \"shadow\"",
"originPath": "file.strings.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
}
]
},
{
"identifier": "D001",
"description": "Found a domain referencing a social media service",
"averageSignalStrength": 0.1,
"peakSignalStrength": 0.1,
"finalSignalStrength": 0.1,
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found domain \"facebook.com\"",
"originPath": "file.extractedDomains.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
},
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found domain \"instagram.com\"",
"originPath": "file.extractedDomains.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
},
{
"strength": 0.1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "Found domain \"twitter.com\"",
"originPath": "file.extractedDomains.references",
"originType": "EXTRACTED_FILE",
"originIdentifier": "f876eb760ae069b97785d6fc3476b2850a0624533be839de46d21b39b1b2ea1b"
}
]
}
],
"file":
{
"name": "https://www.google.com",
"hash": "ac6bb669e40e44a8d9f8f0c94dfc63734049dcf6219aac77f02edf94b9162c09",
"type": "other"
},
"filesDownloadFinished": false,
"postprocessIocs":
[
"url"
],
"created_date": "06/06/2023, 11:18:39",
"estimatedTime": "8",
"estimated_progress": 1.0
}
],
"extra_data":
[],
"summary":
{
"total_benign": 1,
"total_unknown": 0,
"total_informational": 0,
"total_suspicious": 0,
"total_likely_malicious": 0,
"total_malicious": 0,
"total_rejected": 0,
"rejected_reasons":
[],
"flow_id": "647f160ee407f2e1dc0fccf4"
},
"status": "success",
"message": "Total benign: 1, Total unknown: 0, Total informational: 0, Total suspicious: 0, Total likely malicious: 0, Total malicious: 0, Total rejected: 0, Rejected reasons: [], Flow id: 647f160ee407f2e1dc0fccf4",
"parameter":
{
"url": "https://www.google.com",
"is_private": false
},
"context":
{}
}
],
"result_summary":
{
"total_objects": 1,
"total_objects_successful": 1
},
"status": "success",
"message": "1 action succeeded",
"exception_occured": false,
"action_cancelled": false
}
### [detonate file](/docs/filescan/3.1.1/integrations/splunk-soar#detonate-file)

Scan file resource with Sandbox POST - Scan File

#### [Parameters](/docs/filescan/3.1.1/integrations/splunk-soar#parameters)

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| vault id | Vault ID of file to detonate |  | yes |
| password | Custom password, in case uploaded archive is protected |  |  |
| is private | If file should not be available for download by other users |  |  |
| description | Uploaded file/url description |  |  |

Example outputCopy{
"identifier": "detonate_file",
"result_data":
[
{
"data":
[
{
"finalVerdict":
{
"verdict": "MALICIOUS",
"threatLevel": 1,
"confidence": 1
},
"allTags":
[
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f",
"isRootTag": true,
"tag":
{
"name": "txt",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "OSINT_LOOKUP",
"sourceIdentifier": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f",
"tag":
{
"name": "virus",
"synonyms":
[
"Virus RAT"
],
"descriptions":
[],
"verdict":
{
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
}
}
],
"overallState": "success",
"taskReference":
{
"name": "transform-file",
"additionalInfo":
{
"submitName": "eicar.txt",
"submitTime": 1686054391159,
"digests":
{
"SHA-256": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f"
}
},
"ID": "ef3ed039-2f1e-44c3-af8c-e4110f39e823",
"state": "SUCCESS",
"resourceReference":
{
"type": "TRANSFORM_FILE",
"name": "file",
"ID": "492b4683-d6ac-489f-aab9-5a9cb4a921f3"
},
"opcount": 1,
"processTime": 399
},
"subtaskReferences":
[
{
"name": "visualization",
"additionalInfo": "8d228363-ae45-499f-9310-b6512bbdd2a8",
"ID": "1083a544-8b4c-4c7d-b648-d0f825949228",
"state": "SUCCESS",
"resourceReference":
{
"type": "VISUALIZATION",
"name": "visualization",
"ID": "8d228363-ae45-499f-9310-b6512bbdd2a8"
},
"opcount": 1,
"processTime": 35
},
{
"name": "osint",
"additionalInfo": "492b4683-d6ac-489f-aab9-5a9cb4a921f3",
"ID": "8be48ff9-65c1-4538-8337-8d0b7a2f7fa1",
"state": "SUCCESS",
"resourceReference":
{
"type": "OSINT",
"name": "osint",
"ID": "0338b8ed-9bbd-4163-ab5f-60f4ee03f949"
},
"opcount": 4,
"processTime": 1009
},
{
"name": "osint-fuzzyhash",
"additionalInfo": "492b4683-d6ac-489f-aab9-5a9cb4a921f3",
"ID": "01857894-2a7e-4689-81ee-dbcb0d6d104b",
"state": "SUCCESS",
"resourceReference":
{
"type": "OSINT",
"name": "osint",
"ID": "f450eb64-35b0-42ab-b703-607b66bac62f"
},
"opcount": 2,
"processTime": 1006
}
],
"allSignalGroups":
[
{
"identifier": "Y002",
"description": "Matched a malicious YARA rule",
"averageSignalStrength": 1,
"peakSignalStrength": 1,
"finalSignalStrength": 1,
"verdict":
{
"verdict": "MALICIOUS",
"threatLevel": 1,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 1,
"isStrictlyBasedOnInputData": true,
"signalReadable": "Matched YARA rule \"SUSP_Just_EICAR\" with strength \"1\"",
"additionalInfo": "SUSP_Just_EICAR",
"originPath": "file.yaraMatches",
"originType": "INPUT_FILE",
"originIdentifier": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f"
}
]
},
{
"identifier": "I000",
"description": "OSINT source detected malicious resource",
"averageSignalStrength": 1,
"peakSignalStrength": 1,
"finalSignalStrength": 1,
"verdict":
{
"verdict": "MALICIOUS",
"threatLevel": 1,
"confidence": 1
},
"allTags":
[],
"signals":
[
{
"strength": 1,
"isStrictlyBasedOnInputData": false,
"signalReadable": "OSINT provider \"OPSWAT_REPUTATION\" detected resource \"275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f\" as \"MALICIOUS\"",
"additionalInfo": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f",
"originPath": "osint.results.verdict",
"originType": "INPUT_FILE",
"originIdentifier": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f"
}
]
}
],
"file":
{
"name": "eicar.txt",
"hash": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f",
"type": "other"
},
"filesDownloadFinished": true,
"created_date": "06/06/2023, 12:26:31",
"estimatedTime": "14",
"estimated_progress": 0.6291428634098598
}
],
"extra_data":
[],
"summary":
{
"total_benign": 0,
"total_unknown": 0,
"total_informational": 0,
"total_suspicious": 0,
"total_likely_malicious": 0,
"total_malicious": 1,
"total_rejected": 0,
"rejected_reasons":
[],
"flow_id": "647f25f6610a6a2dfbb78269"
},
"status": "success",
"message": "Total benign: 0, Total unknown: 0, Total informational: 0, Total suspicious: 0, Total likely malicious: 0, Total malicious: 1, Total rejected: 0, Rejected reasons: [], Flow id: 647f25f6610a6a2dfbb78269",
"parameter":
{
"vault_id": "3395856ce81f2b7382dee72602f798b642f14140",
"is_private": false
},
"context":
{}
}
],
"result_summary":
{
"total_objects": 1,
"total_objects_successful": 1
},
"status": "success",
"message": "1 action succeeded",
"exception_occured": false,
"action_cancelled": false
}
### [search](/docs/filescan/3.1.1/integrations/splunk-soar#search)

Search for reports. Finds reports and uploaded files by various tokens. It uses GET - Search Report endpoint and the 'query' field.

#### [Parameters](/docs/filescan/3.1.1/integrations/splunk-soar#parameters)

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| query | The query string |  | yes |
| limit | Number of total results. Maximum 50. (If page and page_size was also provided, then it will be ignored.) | 10 |  |
| page | Page number, starting from 1 |  |  |
| page_size | Page size. Can be 5, 10 or 20 |  |  |

Example outputCopy{
"identifier": "search",
"result_data":
[
{
"data":
[
{
"id": "7c3fa024-f5c3-42f4-89d7-890a3ba102a2",
"file":
{
"name": "https://docs.google.com/forms/d/e/1FAIpQLSc8HvIVUybHXItl8riDYykGP4bo5HfBXbEm0TGDk8GUmTogeQ/viewform?usp=sf_link",
"mime_type": "text/html",
"short_type": "html",
"sha256": "eb34f32ada377246548f53e8394b3e4830dde4b89c51c1c97f2b693f0a61f4ff",
"link": "https://docs.google.com/forms/d/e/1FAIpQLSc8HvIVUybHXItl8riDYykGP4bo5HfBXbEm0TGDk8GUmTogeQ/viewform?usp=sf_link"
},
"scan_init":
{
"id": "647f2805441a7404ef542e1a"
},
"state": "success_partial",
"verdict": "suspicious",
"original_verdict": null,
"tags":
[
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "7c07c2bc6a6eec42f32fd999becb343cab1308b2ebfbaf6bfe0fc3b2cb66b349",
"isRootTag": true,
"tag":
{
"name": "html",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "7c07c2bc6a6eec42f32fd999becb343cab1308b2ebfbaf6bfe0fc3b2cb66b349",
"isRootTag": true,
"tag":
{
"name": "png",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "7c07c2bc6a6eec42f32fd999becb343cab1308b2ebfbaf6bfe0fc3b2cb66b349",
"isRootTag": true,
"tag":
{
"name": "txt",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "7c07c2bc6a6eec42f32fd999becb343cab1308b2ebfbaf6bfe0fc3b2cb66b349",
"isRootTag": true,
"tag":
{
"name": "javascript",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "7c07c2bc6a6eec42f32fd999becb343cab1308b2ebfbaf6bfe0fc3b2cb66b349",
"isRootTag": true,
"tag":
{
"name": "vbs",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
}
],
"date": "06/06/2023, 12:35:20",
"matches":
[
{
"origin":
{
"sha256": "7c07c2bc6a6eec42f32fd999becb343cab1308b2ebfbaf6bfe0fc3b2cb66b349",
"filetype": "html",
"mime_type": "text/html",
"relation": "source"
},
"matches":
{
"domain":
[
{
"value": "google.com"
}
]
}
}
],
"updated_date": "06/06/2023, 12:35:46"
},
{
"id": "f5861fdf-d1eb-4cf2-a63f-702d3c4bf9cd",
"file":
{
"name": "CLIPStudio.exe",
"mime_type": "application/x-msdownload",
"short_type": "peexe",
"sha256": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"link": null
},
"scan_init":
{
"id": "647f27205864876b264242c9"
},
"state": "success_partial",
"verdict": "malicious",
"original_verdict": null,
"tags":
[
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": true,
"tag":
{
"name": "peexe",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": true,
"tag":
{
"name": "html",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": true,
"tag":
{
"name": "xml",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "YARA_RULE",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": false,
"tag":
{
"name": "rat",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
}
},
{
"source": "SIGNAL",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": false,
"tag":
{
"name": "keylogger",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
}
},
{
"source": "SIGNAL",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": false,
"tag":
{
"name": "packed",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
}
},
{
"source": "SIGNAL",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": false,
"tag":
{
"name": "greyware",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "SUSPICIOUS",
"threatLevel": 0.5,
"confidence": 1
}
}
},
{
"source": "SIGNAL",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": false,
"tag":
{
"name": "overlay",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "SUSPICIOUS",
"threatLevel": 0.5,
"confidence": 1
}
}
},
{
"source": "SIGNAL",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": false,
"tag":
{
"name": "shell32.dll",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "SUSPICIOUS",
"threatLevel": 0.5,
"confidence": 1
}
}
},
{
"source": "SIGNAL",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": false,
"tag":
{
"name": "lolbin",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.2,
"confidence": 1
}
}
},
{
"source": "SIGNAL",
"sourceIdentifier": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"isRootTag": false,
"tag":
{
"name": "crypto",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
}
],
"date": "06/06/2023, 12:31:33",
"matches":
[
{
"origin":
{
"sha256": "480b8c56b61893d8bfa1fc93fb6cf68feb190f2eaf8e12e36150533e5df51375",
"filetype": "peexe",
"mime_type": "application/x-dosexec",
"relation": "source"
},
"matches":
{
"domain":
[
{
"value": "google.com"
}
]
}
}
],
"updated_date": "06/06/2023, 12:32:03"
},
{
"id": "51cf730b-ac26-4c45-b9ae-e878107c7d83",
"file":
{
"name": "SecuriteInfo.com.Trojan.Linux.Mirai.1.3984.28786.elf",
"mime_type": "application/x-executable",
"short_type": "elf",
"sha256": "1a7191c2386e589559e7badb04bec8022f8eeefac29ca458de3c4726507284dc",
"link": null
},
"scan_init":
{
"id": "647f26cd7c11a6632cb82e86"
},
"state": "success",
"verdict": "malicious",
"original_verdict": null,
"tags":
[
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "1a7191c2386e589559e7badb04bec8022f8eeefac29ca458de3c4726507284dc",
"isRootTag": true,
"tag":
{
"name": "elf",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "1a7191c2386e589559e7badb04bec8022f8eeefac29ca458de3c4726507284dc",
"isRootTag": true,
"tag":
{
"name": "html",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "MEDIA_TYPE",
"sourceIdentifier": "1a7191c2386e589559e7badb04bec8022f8eeefac29ca458de3c4726507284dc",
"isRootTag": true,
"tag":
{
"name": "xml",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "INFORMATIONAL",
"threatLevel": 0.1,
"confidence": 1
}
}
},
{
"source": "OSINT_LOOKUP",
"sourceIdentifier": "1a7191c2386e589559e7badb04bec8022f8eeefac29ca458de3c4726507284dc",
"tag":
{
"name": "mirai",
"synonyms":
[
"linux/mirai"
],
"descriptions":
[
{
"description": "Mirai (Japanese for \"the future\") is malware that turns computer systems running Linux into remotely controlled \"bots\", that can be used as part of a botnet in large-scale network attacks. It primarily targets online consumer devices such as remote cameras and home routers. The Mirai botnet has been used in some of the largest and most disruptive distributed denial of service (DDoS) attacks, including an attack on 20 September 2016 on computer security journalist Brian Krebs's web site, an attack on French web host OVH and the October 2016 Dyn cyberattack.",
"cluster":
{
"type": "tool",
"authors":
[
"Alexandre Dulaunoy",
"Florian Roth",
"Timo Steffens",
"Christophe Vandeplas",
"Dennis Rand",
"raw-data"
]
}
},
{
"description": "Mirai (Japanese for \"the future\", 未来) is a malware that turns networked devices running Linux into remotely controlled \"bots\" that can be used as part of a botnet in large-scale network attacks. It primarily targets online consumer devices such as IP cameras and home routers. The Mirai botnet was first found in August 2016 by MalwareMustDie, a whitehat malware research group, and has been used in some of the largest and most disruptive distributed denial of service (DDoS) attacks, including an attack on 20 September 2016 on computer security journalist Brian Krebs's web site, an attack on French web host OVH, and the October 2016 Dyn cyberattack.",
"cluster":
{
"type": "botnet",
"authors":
[
"Various"
]
}
}
],
"verdict":
{
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
}
},
{
"source": "SIGNAL",
"sourceIdentifier": "1a7191c2386e589559e7badb04bec8022f8eeefac29ca458de3c4726507284dc",
"isRootTag": false,
"tag":
{
"name": "anti-debug",
"synonyms":
[],
"descriptions":
[],
"verdict":
{
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
}
}
],
"date": "06/06/2023, 12:30:11",
"matches":
[
{
"origin":
{
"sha256": "1a7191c2386e589559e7badb04bec8022f8eeefac29ca458de3c4726507284dc",
"filetype": "elf",
"mime_type": "application/x-executable",
"relation": "source"
},
"matches":
{
"domain":
[
{
"value": "google.com"
}
]
}
}
],
"updated_date": "06/06/2023, 12:30:26"
}
],
"extra_data":
[],
"summary":
{
"total_benign": 0,
"total_unknown": 0,
"total_informational": 0,
"total_suspicious": 1,
"total_likely_malicious": 0,
"total_malicious": 2,
"available_report_count": 963
},
"status": "success",
"message": "Total benign: 0, Total unknown: 0, Total informational: 0, Total suspicious: 1, Total likely malicious: 0, Total malicious: 2, Available report count: 963",
"parameter":
{
"query": "google.com",
"limit": 3
},
"context":
{}
}
],
"result_summary":
{
"total_objects": 1,
"total_objects_successful": 1
},
"status": "success",
"message": "1 action succeeded",
"exception_occured": false,
"action_cancelled": false
}
### [file reputation](/docs/filescan/3.1.1/integrations/splunk-soar#file-reputation)

Get the reputation for one given hash (returns with the last 10 sandbox reports). It uses GET - Get Reputation endpoint.

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| sha256 | SHA256 value of the file |  | yes |

Example outputCopy{
"identifier": "file_reputation",
"result_data":
[
{
"data":
[
{
"sha256": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f",
"overall_verdict": "malicious",
"fuzzyhash":
{
"hash": "07307bf492161daaeb78fdc27dae1fdb0b246f6f4d4dec3d0f6bbc3b2d5146d6",
"verdict": "unknown"
},
"mdcloud":
{
"total_av_engines": 32,
"detected_av_engines": 25,
"scan_time": "2023-06-06T04:58:30.513000"
},
"community":
{
"vote_malicious": 0,
"vote_benign": 0
},
"filescan_reports":
[
{
"verdict": "malicious",
"report_date": "12/31/2022, 01:15:32",
"report_id": "211baaf5-801a-4279-88f5-7958e130d7db",
"flow_id": "63af8afe0e926711fd75e445"
},
{
"verdict": "malicious",
"report_date": "12/29/2022, 01:05:26",
"report_id": "bb5355a7-4a98-4cd1-ba9e-9b3010372390",
"flow_id": "63ace7c70fdf1633326c6c27"
},
{
"verdict": "malicious",
"report_date": "12/26/2022, 04:59:45",
"report_id": "bfb9c4ed-357e-4af8-b2f0-727effbaef87",
"flow_id": "63a92a3ea70bef46551b7782"
},
{
"verdict": "malicious",
"report_date": "12/25/2021, 01:07:54",
"report_id": "8220c0f7-03a2-4931-a582-fbc33dfc5d5a",
"flow_id": "61c66e3fec6c6c14a9f07c07"
},
{
"verdict": "malicious",
"report_date": "12/25/2021, 01:06:05",
"report_id": "469be5e9-c1f9-48f6-83c0-39c8c8cd9f13",
"flow_id": "61c66e488991ba72b39679d1"
},
{
"verdict": "malicious",
"report_date": "12/23/2022, 03:21:36",
"report_id": "9ed67cf6-a2b5-46ee-9e98-58aad27cd9e8",
"flow_id": "63a4ff0c779e491a53b2de1f"
},
{
"verdict": "malicious",
"report_date": "12/23/2022, 01:29:49",
"report_id": "b3536665-de06-462d-b92f-846d1c6bf642",
"flow_id": "63a4fef0276b548f03d80572"
},
{
"verdict": "malicious",
"report_date": "12/22/2022, 12:22:48",
"report_id": "3c08ebac-5687-4d3b-a305-3a01dccfa3d7",
"flow_id": "63a44c17673d3bcb5ee0b6cf"
},
{
"verdict": "malicious",
"report_date": "12/22/2022, 01:05:29",
"report_id": "112979f1-04cc-4d7b-b3d3-4a78616aa79c",
"flow_id": "63a3ad3f3b408c3d4c8a8b67"
},
{
"verdict": "malicious",
"report_date": "12/21/2022, 13:48:10",
"report_id": "f457f97a-4a1b-4d66-a971-ff01249980f2",
"flow_id": "63a2e41134212f6643b94e22"
}
]
}
],
"extra_data":
[],
"summary":
{
"verdict": "malicious"
},
"status": "success",
"message": "Verdict: malicious",
"parameter":
{
"sha256": "275a021bbfb6489e54d471899f7db9d1663fc695ec2fe2a2c4538aabf651fd0f"
},
"context":
{}
}
],
"result_summary":
{
"total_objects": 1,
"total_objects_successful": 1
},
"status": "success",
"message": "1 action succeeded",
"exception_occured": false,
"action_cancelled": false
}
### [ioc reputation](/docs/filescan/3.1.1/integrations/splunk-soar#ioc-reputation)

Get the reputation for one given hash (returns with the last 10 sandbox reports). It uses GET - Get Reputation Ioc endpoint.

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| type | Type of the ioc. It should be ip, domain or url. |  | yes |
| value | The value |  |  |

Example outputCopy{
"identifier": "ioc_reputation",
"result_data":
[
{
"data":
[
{
"ioc_type": "domain",
"ioc_value": "google.com",
"overall_verdict": "informational",
"mdcloud":
{
"scan_time": "2023-06-06T13:38:07.488000",
"detected": 0
},
"community":
{
"vote_malicious": 0,
"vote_benign": 0
},
"filescan_reports":
[
{
"verdict": "informational",
"report_date": "06/02/2023, 22:34:34",
"report_id": "00401cd7-438e-4c80-883e-5feef914c837",
"flow_id": "647a6e797868b55bc44d05e8"
},
{
"verdict": "informational",
"report_date": "05/17/2023, 01:11:54",
"report_id": "004bc195-de97-4654-8e58-fcd948c326f3",
"flow_id": "646428403102425a10e17dcd"
},
{
"verdict": "informational",
"report_date": "05/22/2023, 20:28:17",
"report_id": "006e7299-c27c-448b-a3b4-a0b32721a5d2",
"flow_id": "646bd05b495591a75df50d0e"
},
{
"verdict": "suspicious",
"report_date": "05/21/2023, 22:25:04",
"report_id": "0070d24e-9d2e-4e79-a2b5-8f6bf1bde6b7",
"flow_id": "646a9a3af6613382080cc2a0"
},
{
"verdict": "informational",
"report_date": "05/26/2023, 16:49:28",
"report_id": "007c2b34-228c-4f93-9a13-0d7accac4bdb",
"flow_id": "6470e30f6abf73674178bbd5"
},
{
"verdict": "informational",
"report_date": "05/14/2023, 01:25:14",
"report_id": "0082c1da-904c-4225-818f-8c63ac6c9ec0",
"flow_id": "646039eca20ec3c5cf1f8717"
},
{
"verdict": "malicious",
"report_date": "06/02/2023, 03:45:35",
"report_id": "00ad13fe-7245-4253-b03c-f90e0ebe8cfb",
"flow_id": "647965dfe794f9b5b39e21a5"
},
{
"verdict": "malicious",
"report_date": "06/02/2023, 06:39:06",
"report_id": "00b960c0-421a-4d20-ac5c-71996150416a",
"flow_id": "64798e88e794f9b5b39e283f"
},
{
"verdict": "informational",
"report_date": "05/26/2023, 16:49:28",
"report_id": "00c9584d-0935-4149-a0bc-aec0d8dd59db",
"flow_id": "6470e30f6abf73674178bbd5"
},
{
"verdict": "malicious",
"report_date": "05/22/2023, 09:34:41",
"report_id": "00ea6aba-6e5a-4176-b814-784624755666",
"flow_id": "646b372d0f421fdacd9cd97e"
}
]
}
],
"extra_data":
[],
"summary":
{
"verdict": "informational"
},
"status": "success",
"message": "Verdict: informational",
"parameter":
{
"type": "domain",
"value": "google.com"
},
"context":
{}
}
],
"result_summary":
{
"total_objects": 1,
"total_objects_successful": 1
},
"status": "success",
"message": "1 action succeeded",
"exception_occured": false,
"action_cancelled": false
}
## [Compatibility](/docs/filescan/3.1.1/integrations/splunk-soar#compatibility)

| Version | Sandbox 1.9.* | Sandbox 2.0.0 - 2.1.0 |
| --- | --- | --- |
| **≤** 1.2.0 | Yes | No |
| 1.2.1 | Yes | Yes |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
