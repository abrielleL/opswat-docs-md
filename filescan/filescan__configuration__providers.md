<!-- source: https://www.opswat.com/docs/filescan/configuration/providers -->

# Providers

At the **Admin Panel > Setting > Configurations > Providers** settings, you can specify numerous configurations related to [MetaDefender Cloud](https://docs.opswat.com/mdcloud).

These include the following:

### [Configuration options](/docs/filescan/configuration/providers#configuration-options)

| Field | Description |
| --- | --- |
| `MDCLOUD_API_URL` | MetaDefender Cloud API URL address. E.g: `https://api.metadefender.com`  MetaDefender Cloud also provides region-specific API endpoints that are listed here: <https://www.opswat.com/docs/mdcloud/compliance/locations>  *Disclaimer: By default, the region is selected automatically based on the user's geographic location. When performing reputation lookups, MetaDefender Cloud may also connect to external service providers that reside in different regions.* |
| `MDCLOUD_API_KEY` | Your MetaDefender Cloud API key. |
| `MDCLOUD_TTL_HOURS` | The TTL (Time-to-Live) of the locally stored reputation table, in hours. The table contains reputations coming from MD Cloud. |
| `MDCLOUD_REPUTATION_ENABLED` | Enable or Disable MetaDefender Cloud reputation. |
| `MDCLOUD_THREATINTEL_ENABLED` | Enable or Disable MetaDefender Cloud ThreatIntel. |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
