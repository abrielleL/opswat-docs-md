<!-- source: https://www.opswat.com/docs/filescan/integrations/cortex-xsoar -->

# Palo Alto - Cortex XSOAR

Palo Alto XSOAR is a security orchestration, automation and response (SOAR) platform, which allows security teams to automate and streamline security processes. By integrating **MetaDefender Aether** (previously known as MetaDefender Sandbox) with Palo Alto XSOAR, security teams can automate the process of scanning files for malware and other security threats. This integration allows security teams to quickly and easily scan files for potential threats, and take immediate action to mitigate any risks that are identified.

With the integration, you can send a file or URL scan request from XSOAR to Aether, or search for previously scanned reports in Aether.

You can find more information about XSOAR [here](https://www.paloaltonetworks.com/resources/datasheets/cortex-xsoar-overview).

MetaDefender Aether integration in the XSOAR marketplace available [here](https://cortex.marketplace.pan.dev/marketplace/details/OPSWATMetaDefenderAether/).

## [Installation](/docs/filescan/integrations/cortex-xsoar#installation)

**Step #1** - Search for *MetaDefender Aether* in the marketpla

**Step #2** - Click on the Install button in the top right corner.

Integration is then added to the basket. (The integration is free.)

**Step #3** - Add an instance.

For that go to Settings -> Integrations, search for '*OPSWAT*' and click on '*Add instance*' at the right side.

Note

An Aether API key is required to use the integration.

You can use the Activation Key that you received from your OPSWAT Sales Representative, and follow the instructions on the [License Activation](https://docs.opswat.com/filescan/installation/license-activation) page or you can create an API key on the [Community site](https://www.filescan.io/users/profile) under API Key tab.

You need to add your API key, and if you have on-prem version of MetaDefender Aether, you can add your own server's URL. The default URL is the Filescan.io free community.

You can validate it under the 'Test results':

## [Available commands](/docs/filescan/integrations/cortex-xsoar#available-commands)

### [Scan URL](/docs/filescan/integrations/cortex-xsoar#scan-url)

`metadefender-aether-scan-url`

Scan URL resource with Aether POST - Scan URL

#### [Command Arguments](/docs/filescan/integrations/cortex-xsoar#command-arguments)

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| url | The URL to submit |  | yes |
| timeout | The timeout for the polling in seconds | 600 |  |
| hide_polling_output | Hide polling output. | true |  |
| description | Uploaded file/url description |  |  |
| tags | Tags array to propagate |  |  |
| password | Custom password, in case uploaded archive is protected |  |  |
| is_private | If file should not be available for download by other users | false |  |

#### [Command example](/docs/filescan/integrations/cortex-xsoar#command-example)

`!metadefender-aether-scan-url url=https://github.com`

#### [Output example](/docs/filescan/integrations/cortex-xsoar#output-example)

### [Scan File](/docs/filescan/integrations/cortex-xsoar#scan-file)

`metadefender-aether-scan-file`

Scan file resource with Aether POST - Scan File

#### [Command Arguments](/docs/filescan/integrations/cortex-xsoar#command-arguments)

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| entry_id | The War Room entry ID of the file to submit. |  | yes |
| timeout | The timeout for the polling in seconds | 1200 |  |
| hide_polling_output | Hide polling output. | true |  |
| description | Uploaded file/url description |  |  |
| tags | Tags array to propagate |  |  |
| password | Custom password, in case uploaded archive is protected |  |  |
| is_private | If file should not be available for download by other users | false |  |

#### [Command example](/docs/filescan/integrations/cortex-xsoar#command-example)

`!metadefender-aether-scan-file entry_id=<paste your entry id here> retry-interval=1 password=infected`

#### [Output example](/docs/filescan/integrations/cortex-xsoar#output-example)

### [Search](/docs/filescan/integrations/cortex-xsoar#search)

`metadefender-aether-search-query`

Search for reports. Finds reports and uploaded files by various tokens. Use GET - Search Report endpoint.

#### [Arguments](/docs/filescan/integrations/cortex-xsoar#arguments)

|  | Description | Default value | Required |
| --- | --- | --- | --- |
| query | The query string |  | yes |
| page | Page number, starting from 1 |  |  |
| page_size | Page size. Can be 5, 10 or 20 |  |  |
| limit | Number of total results. Maximum 50. (If page and page_size was also provided, then it will be ignored.) | 10 |  |

#### [Command example](/docs/filescan/integrations/cortex-xsoar#command-example)

`!metadefender-aether-search-query query=https://theuselessweb.com/ limit=10`

#### [Output example](/docs/filescan/integrations/cortex-xsoar#output-example)

## [Compatibility](/docs/filescan/integrations/cortex-xsoar#compatibility)

| Integration name | Version | Sandbox 1.9.* | Sandbox 2.0.0 - 2.1.0 | Aether 1.0.0- |
| --- | --- | --- | --- | --- |
| OPSWAT-Filescan (deprecated) | `1.*.*` | Yes | No | No |
| OPSWAT-MetaDefender-Sandbox (deprecated) | 1.0.0 | Yes | No | No |
| OPSWAT-MetaDefender-Sandbox (deprecated) | 1.0.1 | Yes | Yes | Yes  *not recommended |
| MetaDefender Aether | 1.0.0 | No | Yes | Yes |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
