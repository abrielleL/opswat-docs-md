<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/engine-config-osint-lookups -->

# OSINT Lookups

**Step #1 - Open** `/home/sandbox/sandbox/transform.cfg` **in a text editor**

**Step #3 - Save the file and restart the** `sandbox` **service**

## [Enable OSINT](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#enable-osint)

To enable reputation lookups and external tools, use the following settings.

transform.cfgCopyrunOSINTLookups=true
runExtendedOSINTLookups=false
runOSINTLookupsOnExtractedFiles=false
runOSINTLookupsTimeoutMs=60000

| Property name | Default value | Description |
| --- | --- | --- |
| runOSINTLookups | true | Main switch to enable reputation lookups and external tool integrations on the input sample |
| runExtendedOSINTLookups | false | Enable execution for extracted IOCs |
| runOSINTLookupsOnExtractedFiles | false | Enable execution for extracted files |
| runOSINTLookupsTimeoutMs | 1 minute | Execution timeout |

## [Enable OSINT lookups exclusively on the input file hash](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#enable-osint-lookups-exclusively-on-the-input-file-hash)

To enable reputation lookups to exclusively only perform OSINT lookups on the input file hash, use the following settings.

transform.cfgCopyrunOSINTLookups=true
runExtendedOSINTLookups=false
runOSINTLookupsOnExtractedFiles=false
runOSINTLookupsRestrictedResourceTypes=FILE_HASH_SHA256
enableFuzzyHashLookup=false
calculateFuzzyFsioHash=false

| Property name | Default value | Description |
| --- | --- | --- |
| runOSINTLookups | true | Main switch to enable reputation lookups and external tool integrations on the input sample |
| runExtendedOSINTLookups | false | Enable execution for extracted IOCs |
| runOSINTLookupsOnExtractedFiles | false | Enable execution for extracted files |
| runOSINTLookupsRestrictedResourceTypes | FILE_HASH_ SHA256, URL, DOMAIN | Type of resource is being looked up during an OSINT query |
| enableFuzzyHashLookup | true | Enable to perform any lookups based on fuzzy hashing |
| calculateFuzzyFsioHash | true | Enable the calculation of fuzzy hashes for files during its lookups |

## [OPSWAT Reputation](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#opswat-reputation)

Enable [OPSWAT Reputation lookups](https://docs.opswat.com/mdcloud/reputation/reputation)

transform.cfgCopyenableOpswatReputationAPI=true
opswatReputationAPIURL=https://api.metadefender.com/
opswatReputationAPIKey=API key

The API key can be configured by the user manually, or it can be part of the license file. A demo API key is used if not specified by the user or license.

| Property Name | Default Value | Description |
| --- | --- | --- |
| enableOpswatReputationAPI | true | Switch to enable / disable OPSWAT Reputation lookups |
| opswatReputationAPIURL | <https://api.metadefender.com/> | API URL |
| opswatReputationAPIKey |  | API key |

## [OPSWAT MultiScanning](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#opswat-multiscanning)

Enable OPSWAT MultiScanning with [MetaDefender Cloud](https://docs.opswat.com/mdcloud) or [MetaDefender Core](https://docs.opswat.com/mdcore)

transform.cfgCopyenableMetaDefenderAPI=false
metaDefenderUseCloudAPI=true
metaDefenderAPIURL=https://api.metadefender.com/
metaDefenderAPIKey=
metaDefenderScanRule=
metaDefenderScanTimeout=60

| Property Name | Default Value | Description |
| --- | --- | --- |
| enableMetaDefenderAPI | false | Switch to enable / disable OPSWAT MultiScanning |
| metaDefenderUseCloudAPI | true | If set to true, multiscan requests will be sent to MetaDefender Cloud If set to false, multiscan requests will be sent to MetaDefender Core |
| metaDefenderAPIURL | <https://api.metadefender.com/> | API URL (could also point to local instance of MDCore, e.g.: <http://10.0.0.5:8008/> ) |
| metaDefenderAPIKey |  | API key |
| metaDefenderScanRule |  | Workflow rule to use |
| metaDefenderScanTimeout | 1 minute | Execution timeout |

## [OPSWAT Fuzzy Hash Lookup](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#opswat-fuzzy-hash-lookup)

Fuzzy hashes are basically a SHA-256 of a long string that is built using a streamlined order, containing very high-level, but specific attributes of an input file. It is a proprietary algorithm and format developed by OPSWAT to enable detection of clusters of files / unknown malware. **MetaDefender Sandbox** (previously known as OPSWAT Filescan Sandbox) calculates FSIO Fuzzy hash for each appropriate input sample and looks for this hash in a specifically defined list.

**Fuzzy hash lookup results are displayed in OSINT Lookup section**

Please note, that you may not see result for every scanned malicious data.

The feature is enabled by default. To turn it off do the following steps:

transform.cfgCopyenableFuzzyHashLookup=false
## [URL Reputation Predictor](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#url-reputation-predictor)

Enable URL Reputation Predictor lookups based on .

Warning

This is an experimental feature, only enabled in offline mode by default.

transform.cfgCopyenableUrlReputationPredictor=false
## [Offline reputation](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#offline-reputation)

Enable Offline reputation lookup.

transform.cfgCopyenableOfflineReputationLookup=false
## [Virus Total](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#virus-total)

Enable [Virus Total](https://www.virustotal.com/) lookups

transform.cfgCopyenableVirusTotalLookups=false
virusTotalAPIKey=
virusTotalQueriesPerMinute=4
virusTotalDefaultMaliciousEngineCount=3

| Property Name | Default Value | Description |
| --- | --- | --- |
| enableVirusTotalLookups | false | Switch to enable / disable Virus Total lookups |
| virusTotalAPIKey |  | API key |
| virusTotalQueriesPerMinute | 4 | Rate limiter for Virus total API queries / second. Value '0' means no rate limit. |
| virusTotalDefaultMaliciousEngineCount | 3 | Malicious lookup verdict if at least the configured number of providers detected the input as malicious |

## [Broadcom Threat Intel Insight](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#broadcom-threat-intel-insight)

Enable [Broadcom Threat Intel Insights](https://apidocs.securitycloud.symantec.com/#/doc?id=insight_api) lookups

transform.cfgCopyenableBroadcomInsightAPI=false
broadcomInsightAPIURL=https://api.sep.eu.securitycloud.symantec.com/
broadcomInsightSecret=
broadcomNetworkConfidenceThreshold=80
broadcomNetworkMaliciousThreatLevel=9
broadcomSha256ConfidenceThreshold=80
broadcomInsightMaxRetry=2

| Property Name | Default Value | Description |
| --- | --- | --- |
| enableBroadcomInsightAPI | false | Switch to enable / disable Broadcom Threat Intel Insight lookups |
| broadcomInsightAPIURL | <https://api.sep.eu.securitycloud.symantec.com/> | API URL |
| broadcomInsightSecret |  | API key |
| broadcomNetworkConfidenceThreshold | 80 | Network related results are accepted when meeting the confidence threshold |
| broadcomNetworkMaliciousThreatLevel | 9 | Network related threat level threshold to meet for malicious or or likely malicious verdicts. In case confidence treshold is 80 or above the verdict is malicious, otherwise likely malicious. |
| broadcomSha256ConfidenceThreshold | 80 | File (SHA-256) related results are accepted when meeting the confidence threshold |
| broadcomInsightMaxRetry | 2 | Maximum number of retries for API requests |

## [Google Safe Browsing](/docs/filescan/3.1.1/configuration/engine-config-osint-lookups#google-safe-browsing)

Enable [Google Safe Browsing](https://developers.google.com/safe-browsing/) lookups

transform.cfgCopyenableSafebrowsingLookups=false
safebrowsingAPI=

| Property Name | Default Value | Description |
| --- | --- | --- |
| enableSafebrowsingLookups | false | Switch to enable / disable Safe Browsing lookups |
| safebrowsingAPI |  | API key |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
