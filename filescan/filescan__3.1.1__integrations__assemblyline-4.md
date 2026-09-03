<!-- source: https://www.opswat.com/docs/filescan/3.1.1/integrations/assemblyline-4 -->

# Assemblyline 4

[Assemblyline 4](https://github.com/CybercentreCanada/assemblyline) is a scalable file triage and malware analysis system integrating some of the cyber security community's tools.

With the integration, you can send a file or URL scan request from [Assemblyline 4](https://github.com/CybercentreCanada/assemblyline) to [MetaDefender Sandbox](https://docs.opswat.com/filescan/datasheet).

The source code of the integration is available [here](https://github.com/OPSWAT/assemblyline-service-metadefender-sandbox).

The docker image is available [here](https://hub.docker.com/r/opswat/assemblyline-service-metadefender-sandbox).

## [Installation](/docs/filescan/3.1.1/integrations/assemblyline-4#installation)

In Assemblyline4 go to Administration -> Services and click on the green plus button (add service):

Paste the [service manifest](https://github.com/OPSWAT/assemblyline-service-metadefender-sandbox/blob/main/service_manifest.yml) on the pup-up window:

Service manifest for 4.5.1.dev0Copy# Name of the service
name: MetaDefender_Sandbox
# Version of the service
version: 4.5.1.dev0
description: This Assemblyline service interfaces with the MetaDefender Sandbox -previously known as OPSWAT Filescan Sandbox-, detonating files and URLs. This integration was developed by OPSWAT. (C) OPSWAT, Inc.
accepts: .*
rejects: empty
stage: CORE
category: Dynamic Analysis
file_required: true
timeout: 600
# is the service enabled by default
enabled: true
uses_metadata: true
# -1000: safe
# 0 - 299: informational
# 300 - 699: suspicious
# 700 - 999: highly suspicious
# >= 1000: malicious
heuristics:
- description: MetaDefender Sandbox determined that the file is benign.
filetype: "*"
heur_id: 1
name: MetaDefender Sandbox verdict is benign.
score: -1000
- description: MetaDefender Sandbox signal group is benign.
filetype: "*"
heur_id: 2
name: Benign threat indicators
score: -1000
- description: MetaDefender Sandbox determined that the file is informational/no threat.
filetype: "*"
heur_id: 3
name: MetaDefender Sandbox verdict is no threat.
score: 150
- description: MetaDefender Sandbox signal group is informational/no threat.
filetype: "*"
heur_id: 4
name: Informational threat indicators
score: 150
- description: MetaDefender Sandbox determined that the file is unknown.
filetype: "*"
heur_id: 5
name: MetaDefender Sandbox verdict is unknown
score: 299
- description: MetaDefender Sandbox signal group is unknown.
filetype: "*"
heur_id: 6
name: Unknown threat indicators
score: 299
- description: MetaDefender Sandbox determined that the file is suspicious.
filetype: "*"
heur_id: 7
name: MetaDefender Sandbox verdict is suspicious
score: 500
- description: MetaDefender Sandbox signal group is suspicious.
filetype: "*"
heur_id: 8
name: Suspicious threat indicators
score: 500
- description: MetaDefender Sandbox determined that the file is likely malicious.
filetype: "*"
heur_id: 9
name: MetaDefender Sandbox verdict is likely malicious
score: 850
- description: MetaDefender Sandbox signal group is likely malicious.
filetype: "*"
heur_id: 10
name: Likely malicious threat indicators
score: 850
- description: MetaDefender Sandbox determined that the file is malicious.
filetype: "*"
heur_id: 11
name: MetaDefender Sandbox verdict is malicious
score: 1000
- description: MetaDefender Sandbox signal group is malicious.
filetype: "*"
heur_id: 12
name: Malicious threat indicators
score: 1000
# Docker configuration block which defines:
# - the name of the docker container that will be created
# - CPU and ram allocation by the container
docker_config:
image: ${REGISTRY}opswat/assemblyline-service-metadefender-sandbox:4.5.1.dev0
cpu_cores: 1.0
ram_mb: 1024
allow_internet_access: true
config:
api_key: ""
host: "https://www.filescan.io"
poll_interval: 2
timeout: 60
submission_params:
- default: ""
name: api_key
type: str
value: ""
- default: 2
name: poll_interval
type: int
value: 2
- default: 60
name: timeout
type: int
value: 60
- default: ""
name: description
type: str
value: ""
- default: ""
name: password
type: str
value: ""
- default: ""
name: is_private
type: bool
value: ""Note

If you use the yml file from github, please change the $SERVICE_TAG vaiable everywhere to the actual docker tag. (Now it's 4.5.1.dev0)

Click on Add button on the bottom left.

After installation, you will find the service within the loaded services. Ensure that it has been enabled:

## [Configuration](/docs/filescan/3.1.1/integrations/assemblyline-4#configuration)

On the service details panel you can set the submission parameters and the service variables.

### [Service variables](/docs/filescan/3.1.1/integrations/assemblyline-4#service-variables)

The service variables are the follows:

|  | Description | Default value | required |
| --- | --- | --- | --- |
| api-key | MetaDefender Sandbox api-key |  | yes |
| host | Sandbox host | <https://www.filescan.io> | yes |
| poll-interval | Submission polling interval | 2 |  |
| timeout | Submission polling timeout | 60 |  |

Note

A MetaDefender Sandbox API key is required to use the integration.

You can use the Activation Key that you received from your OPSWAT Sales Representative, and follow the instructions on the [License Activation](https://docs.opswat.com/filescan/installation/license-activation) page or you can create an API key on the [Community site](https://www.filescan.io/users/profile) under API Key tab.

You need to add your API key, and if you have on-prem version of MetaDefender Sandbox, you can add your own server's URL. The default URL is Filescan.io free community.

After saving the settings you can use the service.

### [Submission parameters](/docs/filescan/3.1.1/integrations/assemblyline-4#submission-parameters)

Important

To use the service, you must select the `MetaDefender_Sandbox` service under the settings menu when submitting a file or a URL. You can found it under the Dynamic Analysis section:

Under the Service Specific Parameters section you can set the Filescsan Sandbox submission parameters:

These parameters are:

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| Api-Key * | MetaDefender Sandbox api-key | Uses the service variable |  |
| Poll-Interval * | Submission polling interval | 2 |  |
| Timeout * | Submission polling timeout | 60 |  |
| Description | Uploaded file/URL description |  |  |
| Password | Custom password, in case uploaded archive is protected |  |  |
| Is Private | If file should not be available for download by other users |  |  |

*In case that you would like to use different value than it was set under the service variables.

## [Available actions](/docs/filescan/3.1.1/integrations/assemblyline-4#available-actions)

### [File scan](/docs/filescan/3.1.1/integrations/assemblyline-4#file-scan)

To scanning a file drag and drop the target file to the uploader area and click on 'UPLOAD AND SCAN' button:

### [URL/SHA256](/docs/filescan/3.1.1/integrations/assemblyline-4#urlsha256)

To scan an URL, write the URL address to the field and click on SCAN button

To scan a SHA256, copy the target file's SHA256 hash to the field.

Note

You can scan only that SHA256 what is exists in Assemblyline.

Result

After the scan is successfully performed, the main result will be visible with the most important informations:

A summary report of the scan can be found under MetaDefender Sandbox result (heuristic):

Indicators are added in a subsections for heuristics:

If any MITRE ATT&CK was identified, it can be found under the ATT&CK Matrix section:

If there were any parsable attributes in the result, they will appear under Attributions

IOCs were found under the Indicators of Compromise section:

A more detailed report on the file is available by clicking on the links in the Files section:

Here you can found the generated tags:

Furthermore, the link to the complete report is also available at your request below:

## [Compatibility](/docs/filescan/3.1.1/integrations/assemblyline-4#compatibility)

| Tag | Sandbox 1.9.* | Sandbox 2.0.* |
| --- | --- | --- |
| **≤** 4.5.1.dev0 | Yes | No |
| 4.5.1.dev1 | Yes | Yes |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
