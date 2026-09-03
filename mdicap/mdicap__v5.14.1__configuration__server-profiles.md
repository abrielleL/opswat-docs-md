<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/configuration/server-profiles -->

# Server profiles

Server profiles under **Library > Server profiles** help to organize services of one or more servers based on the service type.

Info

For example in case of security rules one or more MetaDefender Core servers are needed to scan requests. For this purpose a server inventory may be created collecting all available Core servers. Then at the rule itself simply this server profile needs to be selected.

Note

Currently MetaDefender ICAP Server uses and allows *MetaDefender Core* type server profiles only.

## [Properties](/docs/mdicap/v5.14.1/configuration/server-profiles#properties)

| Property | Description |
| --- | --- |
| Server profile type | Service type Supported service types are:   1. MetaDefender Core |
| Profile name | Unique identifier of the server profile |
| Server specifications (URI) | Service specifications in [URI syntax](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier). Multiple server specification may be added to a server profile. At least one server specification must exist in a server profile. Only the following URI components are used:   1. scheme 2. host 3. port   Example: <http://127.0.0.1:8008> In case of *MetaDefender Core* server profile types the very same URI will be used for the URLs of *View scan details* links on the *Request details* page under **Dashboard > ICAP history**. If the URI specified here is not reachable on the machine where the actual browsing of the Web Management Console happens (e.g. it is 127.0.0.1 and browsing happens on an other machine) then the *View scan details* link will be broken. See also the *Request details* section in [4.1. ICAP Dashboard](/docs/mdicap/v5.14.1/operating/icap-dashboard). |
| Enable Local Scan | When this option is enabled, the ICAP server will skip the file streaming from MetaDefender ICAP Server to MetaDefender Core In order for using Local Scan feature, belows conditions must be met:   - MetaDefender ICAP Server and MetaDefender Core are installed on same host machine, and both of them can access temp folder of MetaDefender ICAP Server (check "tempdirectory" key in [Configuration file](/docs/mdicap/v5.14.1/configuration/configuration-file)). - The MetaDefender Core's selected workflow rule must enable the setting "**ALLOW SCAN FILES ON SERVER"** for MetaDefender ICAP Server's temp folder. |
| Enable Webhook callback (BETA) | When this option is enable, MetaDefender Core will proactively send callback to MetaDefender ICAP Server's designated URL with full analysis result. Pooling method is disabled.  In order for using webhook callbacks feature incase both MetaDefender ICAP Server and MetaDefender Core are installed on difference host, the IP Address of MetaDefender ICAP Server must be set to *webhook_address*, for details see [Configuration file](/docs/mdicap/v5.14.1/configuration/configuration-file) |
| Server preference | Preference order in which servers are addressed for services Possible values:   - 1. FAILOVER: high availability order; first successfully addressed server in the list will do the service - 2. ROUND ROBIN: load balancing order; next successfully addressed server in the list will do the service - 3. DYNAMIC LOAD BALANCING: the scan request will priority distributed to the least busy base on the scan queue information and also combination with ROUND ROBIN (Support since MD ICAP Server version 5.11.0)       - MetaDefender Core version (5.16.0) or older are not fully compatible with the Dynamic Load Balancing feature. Recommend to use Metadefender Core version **5.16.1 or later** for optimal performance      - Default polling interval to update the scan queue status is 200ms, can be adjusted in **Settings > Global > Queue Size Polling Interval** |
| Certificate based client authentication | If the destination server requires certificate based client host authentication then this checkbox must be marked MetaDefender ICAP Server will use the actual deployment's digital ID, for details see [3.2 Configuring TLS](/docs/mdicap/v5.14.1/configuration/configuring-tls) |

## [Property validation](/docs/mdicap/v5.14.1/configuration/server-profiles#property-validation)

Some of the server profile properties have cross-dependencies and as so must match.

| Server profile type | Server specifications (URI) allowed schemes |
| --- | --- |
| MetaDefender Core | http |
| MetaDefender Core | https |

| Server specifications (URI) scheme | Transport level encryption allowed values |
| --- | --- |
| http | N/A |
| https | N/A If https scheme is specified then the HTTP connection is established over TLS. |

## [Testing the configuration](/docs/mdicap/v5.14.1/configuration/server-profiles#testing-the-configuration)

Clicking the *TEST* button will test the configuration. The test consists of two steps:

1. Syntactical validation of the values
2. Connection test

Note

If the test fails, then the server profile can not be added. Please verify the information entered and attempt the TEST again.

## [Syntactical validation](/docs/mdicap/v5.14.1/configuration/server-profiles#syntactical-validation)

The correctness of the provided values is validated:

1. PROFILE NAME must be unique
2. The SERVER SPECIFICATIONS (URI) values must conform with the URI syntax with the restriction that only the scheme, host and port values are allowed
3. Cross dependencies must match (see the [152617415](/docs/mdicap/v5.14.1/configuration/server-profiles#src-4864692) section)

## [Connection test](/docs/mdicap/v5.14.1/configuration/server-profiles#connection-test)

If the syntactical validation pass, then each server specification is tested for a successful connection.

## [Limitations](/docs/mdicap/v5.14.1/configuration/server-profiles#limitations)

Warning

Currently the connection is tested without using TLS (when configured at all).
