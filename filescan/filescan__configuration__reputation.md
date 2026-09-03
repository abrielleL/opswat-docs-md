<!-- source: https://www.opswat.com/docs/filescan/configuration/reputation -->

# Reputation

The Admin **Panel > Setting > Configurations > Reputation** section allows for fine-tuning of the external reputation like MetaDefender Cloud or MetaDefender Sandbox Community.

### [Configuration options](/docs/filescan/configuration/reputation#configuration-options)

| Field | Description |
| --- | --- |
| `REPUTATION_MDCLOUD_THRESHOLD_MALICIOUS` | The threshold at which we consider a result malicious for MD Cloud. For example, if this is 0.3, we consider something malicious if it's detected by 30% of the MD Cloud engines. |
| `REPUTATION_MDCLOUD_THRESHOLD_LIKELY_MALICIOUS` | The threshold at which we consider a result likely malicious for MD Cloud. |
| `REPUTATION_MDCLOUD_THRESHOLD_SUSPICIOUS` | The threshold at which we consider a result suspicious for MD Cloud. |
| `REPUTATION_MDCLOUD_THRESHOLD_DAYS_OLD` | If the MD Cloud lookup result is very old, it might show false results. For example, a file previously labeled as Benign may later be identified as Malicious. This setting allows old results not to be taken into account. The value represents days. |
| `REPUTATION_COMMUNITY_THRESHOLD_MALICIOUS` | The threshold at which we consider a result malicious for Community votes. |
| `REPUTATION_COMMUNITY_THRESHOLD_LIKELY_MALICIOUS` | The threshold at which we consider a result likely malicious for Community votes. |
| `REPUTATION_COMMUNITY_THRESHOLD_SUSPICIOUS` | The threshold at which we consider a result suspicious for Community votes. |
| `REPUTATION_COMMUNITY_THRESHOLD_VOTENUMBER` | Threshold value for community votes. It is advisable to consider multiple votes. |
| `REPUTATION_BULK_LIMIT` | Limit on how many hashes or IOCs you can search for at once in a bulk lookup scenario. |
| `IOC_REPORTS_REPUTATION_REPORTS_LIMIT` | The report limit determines the maximum number of reports used to calculate the IOC's reputation verdict. |
| `IOC_REPORTS_REPUTATION_DAYS_LIMIT` | The days limit specifies the maximum number of days of reports used to calculate the IOC's reputation verdict. |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
